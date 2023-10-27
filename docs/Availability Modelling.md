# Availability Modelling

## Introduction

TBD

## Model Parameters

| **Parameter**           | **Symbol** | **Description**                                                                                                                                                                                               |
|-------------------------|------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Performance Time        | $t_p$      | The average time a T-Stick performance lasts given in hours.                                                                                                                                                  |
| Performance Intensity   | $j_p$      | The intensity of the performance, rough indicator of the impact of a performance on the reliability of certain components                                                                                     |
| Performance Frequency   | $p_f$      | The average amount of performances per month. It can be used along side **maintenance time between performance**, and **technician availability** to compute the interruption percentage. **SIMULATION ONLY** |
| Technician Availability | $A_{tech}$ | The average amount of hours a technician/luthier is available to fix any issues an artist can’t fix with their instrument per month. **SIMULATION ONLY**                                                      |
| Technician Turnaround   | $t_{tech}$ | The average amount of business days it takes for the technician/luthier to return the instrument to the artist/musician. **SIMULATION ONLY** |
## Model Inputs

| **Inputs**                               | **Symbol** | **Description**                                                                                               |
|------------------------------------------|------------|---------------------------------------------------------------------------------------------------------------|
| Maintenance Time between performances    | $t_m$      | The amount of time an artist/musician spends maintaining the T-Stick in between performances, given in hours. |
| MTTR for T-Stick Components              | $MTTR_c$   | Mean time to repair/replace for T-Stick components in hours.                                                  |
| MTTF for T-Stick Components              | $MTTF_c$   | Mean time between failure of T-Stick components in hours.                                                     |
| Maintenance actions between performances | $MA$       | The actions the artist/musicians take when maintaining their instrument.                                      |
| Available tools                          | $T$        | The available equipment an artist has on hand for maintaining and fixing their instrument.                    |

## Compute Practice Interruption Rate (PIR)

### 1. Computing MTBF and failure rate of T-Stick

To compute the Practice interruption rate we must first compute the failure rate of the T-Stick ($ \lambda_{tstick}$). We do this by adding the failure rate of each component.

$$
\begin{equation}
\lambda_{tstick} = \lambda_{esp32} + \lambda_{fsr}+\lambda_{imu}+\lambda_{button}+\lambda_{capsense}+\lambda_{resistor}+\lambda_{touchsensor}+\lambda_{battery}+\lambda_{connectors}
\end{equation}
$$

where $\lambda_i$ is the failure rate of component $i$.

The failure rates for several components such as:

* FSR
* Resistor
* IMU
* Capsense Board
* ESP32 Board
* Battery

can be estimated using a combination of the [FIDES reliability prediction too](https://www.fides-reliability.org/)l, the [MIL-217F Handbook](https://drive.google.com/file/d/1QNUiTOAwJebwC-bk0FJWB0jD3I6XFxFi/view?usp=drive_link), and the [NPRD-91](https://drive.google.com/file/d/1QPMqClW2nHY4U9tmMO5Lzc11RDF2Oeoc/view?usp=sharing). The MTBF of the connectors is taken from the performance model.

We compute the MTBF of the t stick by taking the reciprocal of the failure rate.

$$
\begin{equation}
MTBF_{tstick} = \frac{1}{\lambda_{tstick}}
\end{equation}
$$

### 3. Compute Mean Performances between failure (MPBF)

We can then compute the mean performances between failure ($MTBF_{tstick}$) by dividing the $MTBF_{tstick}$ by the performance time ($t_P$)

$$
\begin{equation}
MPBF = \frac{MTBF_{tstick}}{t_p}
\end{equation}
$$

### 4. Compute PIR

We calculate the practice interruption rate by taking the reciprocal of $MPBF$.

$$
\begin{equation}
PIR = \frac{1}{MPBF}
\end{equation}
$$

Using Eq.3 and Eq.6 we can simplify the PIR expression.

$$
\begin{align*}
PIR &= t_p(\frac{1}{MTBF_{tstick}}) \tag{Using Eq.3}\\
 &= t_p(\lambda_{tstick}) \tag{Using Eq.6} \\
\end{align*}
$$

Hence an alternative expression for the Practice Interruption rate is:

$$
\begin{equation}
PIR = t_p(\lambda_{tstick})
\end{equation}
$$

In simple words the **Practice Interruption Rate** is the:

$$
\text{average performance time} \times \text{failure rate of the t-stick}
$$

## Compute Performance/Maintenance Ratio (PMR)

Computing the Performance/Maintenance Ratio (PMR) is a matter of taking the $MTBF_{tstick}$ computed in the PIR model and dividing that by the average maintenance time.

### Computing Average Maintenance time ($$T_m$$)

To compute average maintenance time we consider the mean time to repair ($MTTR_c$) of each component and the failure rate of each component ($\lambda_c$). We can then take a weighted average of all the repair by taking into account each components contribution to the total failure rate.

$$
\begin{equation}
T_m =  \sum_{c=0}^n \frac{\lambda_c}{\lambda_{tstick}}(MTTR_c)
\end{equation}
$$

### Compute PMR

To compute PMR we divide the $MTBF_{tstick}$ by the average maintenance time ($T_m$).

$$
\begin{equation}
PMR = \frac{MTBF_{tstick}}{T_m}
\end{equation}
$$

## Compute Direct Maintenance Costs (DMC)

We can also look at the direct maintenance cost of the T-Stick which we define as the dollars spent on maintaining the T-Stick per performance hour.

### Compute Mean Repair Cost of the T Stick

The mean repair cost of the T-Stick ($MRC_{tstick}$) is computed the same way the average maintenance time, by using a weighted average of the mean repair cost of each component.

$$
\begin{equation}
MRC_{tstick} = \sum_{c=0}^n \frac{\lambda_c}{\lambda_{tstick}}(MRC_c)
\end{equation}
$$

### Compute DMC

To compute DMC we divide the mean repair cost by the mean time between failure of the T-Stick ($MTBF_{tstick}$)

$$
\begin{equation}
DMC = \frac{MRC_{tstick}}{MTBF_{tstick}}
\end{equation}
$$


