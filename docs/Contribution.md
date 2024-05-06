# Contribution Guide

The guide offers general rules and guidelines for pushing changes to the documentation site. We accept pull requests on [github](https://github.com/IDMIL/tstick-docs) for new pages/sections and major/minor edits to existing pages. The site is powered by Material for MkDocs. We recommend reading their [documentation](https://squidfunk.github.io/mkdocs-material/) for an understanding of how it works. Each page is written as a markdown file.

## General Rules
1. Check how the page renders before submitting pull requests. [Material for MkDocs Getting Started page](https://squidfunk.github.io/mkdocs-material/getting-started/) shows how to set Material for MkDocs.
2. Add your page to the navigation tree in mkdocs.yml, in the appropriate location so that it shows up in the sidebar.
3. Ensure your pages are readable in both light mode and dark mode. 

## New Page/Section Guidelines
1. Include description of page/section in the pull request.
2. Only ONE new page/section per pull request.
3. Check the structure of other similar pages for inspiration.
4. Avoid table of content trees with a depth of greater than three. (ie: main page -> subpage -> subpage, depth = 3)

## Major/Minor Edits Guidelines
1. Describe reason for the edit in the pull request.
2. Only have ONE major edit per pull requests. You may include multiple minor edits in a single request.