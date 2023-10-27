# Puara Gestures

Note: Article still a Work in Progress

## High-Level gesture vocabulary for the T-Stick

Presented codes are arduino compatible.

### Summary:

- [Puara Gestures](#puara-gestures)
  - [High-Level gesture vocabulary for the T-Stick](#high-level-gesture-vocabulary-for-the-t-stick)
    - [Summary:](#summary)
    - [Signal structures and global variables:](#signal-structures-and-global-variables)
    - [functions](#functions)
    - [/instrument](#instrument)
      - [/instrument/touch/](#instrumenttouch)
        - [/instrument/touch/all (InstrumentData.touchAll)](#instrumenttouchall-instrumentdatatouchall)
        - [/instrument/touch/top (InstrumentData.touchTop)](#instrumenttouchtop-instrumentdatatouchtop)
        - [/instrument/touch/body (InstrumentData.touchBody)](#instrumenttouchbody-instrumentdatatouchbody)
        - [/instrument/touch/middle (InstrumentData.touchMiddle)](#instrumenttouchmiddle-instrumentdatatouchmiddle)
        - [/instrument/touch/bottom (InstrumentData.touchBottom)](#instrumenttouchbottom-instrumentdatatouchbottom)
      - [/instrument/brush](#instrumentbrush)
        - [/instrument/brush/up /down](#instrumentbrushup-down)
        - [/instrument/brush/amplitude (brush)](#instrumentbrushamplitude-brush)
        - [/instrument/brush/energy (rub)](#instrumentbrushenergy-rub)
        - [/instrument/amplitude /roll /tilt](#instrumentamplitude-roll-tilt)
        - [/instrument/shake /jerk](#instrumentshake-jerk)
        - [/instrument/jab (INCOMPLETE)](#instrumentjab-incomplete)

### Signal structures and global variables:

```
byte touchByteSize = 2; // bytes necessary to represent all the stripes (1-bit per stripe) = 2 for the sopranino
byte touchSizeAll = touchByteSize * 8 ; // total amount of T-Stick stripes (8 bits per byte)
byte touchSizeEdge = 4; // amount of T-Stick stripes for top and bottom portions of the T-Stick (arbitrary)
float leakyConstant = 0.05;
float shakeArray[5] = {0,0,0,0,0};
byte shakeArrayindex = 0;
float jabArray[5] = {0,0,0,0,0};
byte jabArrayindex = 0;
float shakeAccum = 0;
float cartopolAmplitude = 0;
float cartopolAngle = 0;

struct RawDataStruct { // initialized as RawData
  byte touch[touchByteSize]; // /raw/capsense, i..., 0--255, ... (1 int per 8 capacitive stripes -- 8 bits)
  float fsr; // /raw/fsr, i, 0--4095
  float piezo; // /raw/piezo, i, 0--1023
  float accl[3]; // /raw/accl, fff, +/-16, +/-16, +/-16 (g linear acceleration full scale), converted from sensor data with range +/-32767 (integers)
  float gyro[3]; // /raw/gyro, fff, +/-2000, +/-2000, +/-2000 (dps angular rate full scale), converted from sensor data with range +/-34.90659 (floats)
  float magn[3]; // /raw/magn, iii, fff, +/-16, +/-16, +/-16 (gauss magnetic full scale), converted from sensor data with range +/-32767 (integers)
  float raw[9]; // /raw (IMU data to be send to callibration app)
  float quat[4]; // /raw/quat, ffff, ?, ? ,? ,?
  float ypr[3]; // /raw/ypr, fff, ?, ? ,?
};
```

```
struct NormDataStruct { // initialized as NormData
  float fsr; // /norm/fsr, f, 0--1
  float piezo; // /norm/piezo, f, 0--1
  float accl[3]; // /norm/accl, fff, +/-1, +/-1, +/-1
  float gyro[3]; // /norm/gyro, fff, +/-1, +/-1, +/-1
  float magn[3]; // /norm/magn, fff, +/-1, +/-1, +/-1
};
```

```
struct LastStateDataStruct { // initialized as LastStateData
  byte touch[touchByteSize]; // last state of /raw/capsense
  byte brushUp;
  byte brushDown;
  float shake;
  float shakeAccum;
};
```

```
struct InstrumentDataStruct { // initialized as InstrumentData
  byte touchAll[touchByteSize]; // surface contact
  byte touchTop;
  byte touchBody[touchByteSize-1];
  byte touchMiddle[touchByteSize-2];
  byte touchBottom;
  byte brushUp;
  byte brushDown;
  byte brushAmplitude;
  byte energy;
  float amplitude;
  float roll;
  float tilt;
  float shake;
  float jerk;
};
```

### functions

* Implement bit read/write function (not needed for arduino, bitRead and bitWrite function is already included):

```
bool bitRead(byte target, byte index){
    return ((target >> index) & 1U);
}

void bitWrite(byte destiny, byte index, byte origin){
    if (bitRead(destiny, index) != bitRead(origin, index)) {
        destiny.flip(index);
    }
}
```

* Implement function to calculate mean for a given bit range

```
float bitMean (byte capsense_array[], byte first_bit, byte last_bit) { // calculates mean for a given bit range
    float mean = 0;
    For ( i = first_bit; i < last_bit; i++ ) {
        byte array_index = i/8;
        byte target_index = i - (8 * array_index);
        If ( bitRead(capsense_array[array_index], target_index) ) { // read each bit ...
        mean += 1/ (last_bit - first_bit); // ... and add if its high
        }
    }
    return mean;
}
```

* Leaky integrator:

```
float leakyIntegrator (float reading, float old_value,float leak) {
  return reading + (old_value * leak)
}
```

* Windowed Extrema (getting max and min values out of a window). Dont forget to populate `shakeArray`

```
float windowedExtremaMax (float array[]) {
  float result = 0;
  For ( i=0; i < sizeof(array)/sizeof(array[0]); i++ ) {
    result = max(result, array[i]);
  }
  return result;
}

float windowedExtremaMin (float array[]) {
  float result = 0;
  For ( i=0; i < sizeof(array)/sizeof(array[0]); i++ ) {
    result = min(result, array[i]);
  }
  return result;
}
```

* 1st order IIR filter for sensor data:

```
float lowPassFilter (data,olddata,k) {
  return olddata + ((data - olddata)/k)
}
```

### /instrument

#### /instrument/touch/

##### /instrument/touch/all (InstrumentData.touchAll)

* InstrumentData.touchAll: get the "amount of touch" normalized between 0 and 1

```
InstrumentData.touchAll = bitMean(RawData.touch, 0, touchSizeAll);
```

##### /instrument/touch/top (InstrumentData.touchTop)

* InstrumentData.touchTop: similar to /instrument/touch/all, but applied only to the "top" region of the capsense

```
InstrumentData.touchTop = bitMean(RawData.touch, 0, touchSizeEdge);
```

##### /instrument/touch/body (InstrumentData.touchBody)

* InstrumentData.touchBody: similar to /instrument/touch/all, but applied only to the "body" region of the capsense

```
InstrumentData.touchBody = bitMean(RawData.touch, touchSizeEdge, touchSizeAll);
```

##### /instrument/touch/middle (InstrumentData.touchMiddle)

* InstrumentData.touchMiddle: similar to /instrument/touch/middle, but applied only to the "middle" region of the capsense

```
InstrumentData.touchMiddle = bitMean(RawData.touch, touchSizeEdge, (touchSizeAll - touchSizeEdge) );
```

##### /instrument/touch/bottom (InstrumentData.touchBottom)

* InstrumentData.touchBottom: similar to /instrument/touch/all, but applied only to the "top" region of the capsense

```
InstrumentData.touchBottom = bitMean(RawData.touch, (touchSizeAll - touchSizeEdge), touchSizeAll);
```

#### /instrument/brush

##### /instrument/brush/up /down

```
operation_up = (LastStateData.brushUp & RawData.touch)
operation_down = (LastStateData.brushDown & RawData.touch)

For ( i = 0; i < number_of_touch; i++ ) {
    if ( bitRead(operation_up, i) ) { 
        InstrumentData.brushUp = (number_of_touch - i) / number_of_touch;
        mean_up += 1/ number_of_touch;
        }
    if ( bitRead(operation_down, i) ) {
        InstrumentData.brushDown = (number_of_touch - i) / number_of_touch;
        mean_down += 1/ number_of_touch;
        }
}
```

##### /instrument/brush/amplitude (brush)

```
InstrumentData.brushAmplitude = InstrumentData.brushDown - InstrumentData.brushUp
```

##### /instrument/brush/energy (rub)

```
if (InstrumentData.brushUp > InstrumentData.brushDown) {
  InstrumentData.energy = InstrumentData.brushUp
}
else {
  InstrumentData.energy = InstrumentData.brushDown
}
```

##### /instrument/amplitude /roll /tilt

(range +/- 2 ?)

```
cartopolAmplitude = sqrt( pow((((RawData.accl[1] * 2) - 128) * -1),2) + pow((((RawData.accl[2] * 2) - 128) * -1)) )
cartopolAngle = tan-1 ( (((RawData.accl[2] * 2) - 128) * -1) / (((RawData.accl[1] * 2) - 128) * -1) )
InstrumentData.amplitude = sqrt( pow(cartopolAmplitude) + pow(((RawData.accl[0] * 2) - 128)) )
InstrumentData.roll = cartopolAngle + 3.14159
InstrumentData.tilt = tan-1 ( ((RawData.accl[0] * 2) - 128) / cartopolAmplitude)
```

##### /instrument/shake /jerk

```
// populating shakeArray each loop)
shakeArray[shakeArrayindex] = InstrumentData.amplitude;
if (shakeArrayindex < 5) {
  shakeArrayindex += 1; 
}
else {
  shakeArrayindex = 0;
}

shakeAccum = -(windowedExtremaMax(shakeArray[]) - windowedExtremaMin(shakeArray[]));
shakeAccum = leakyIntegrator(shakeAccum,LastStateData.shakeAccum,leakyConstant);
InstrumentData.shake = lowPassFilter(shakeAccum,LastStateData.shake,20);

InstrumentData.jerk = shakeAccum - InstrumentData.shake;
```

##### /instrument/jab (INCOMPLETE)

```
// populating jabArray each loop)
shakeArray[jabArrayindex] = InstrumentData.jab;
if (jabArrayindex < 5) {
  jabArrayindex += 1; 
}
else {
  jabArrayindex = 0;
}

InstrumentData.jab = windowedExtremaMax(jabArray[]) - windowedExtremaMin(jabArray[]);



RawData.accl[0]


Andrew

thrust
shake
spin
frame (populated inside?)
rest vs effort

Travis

Jab
eggbeater
eggwhip
tilt
hold
squeez

#### Update Last State Values
LastStateData.brushUp = (RawData.touch << 1) & (~ RawData.touch) LastStateData.brushDown = (RawData.touch >> 1) & (~ RawData.touch)
```


