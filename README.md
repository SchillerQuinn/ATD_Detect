# ATD_Detect
Detects non-standard ATD (Analog To Digital or rectangle) controllers

# Goals:
A problem I have heard from TOs on twitter goes something like the following:

> "There is no way to test if a rectangle controller is modded or not to break restrictions"

**The goal of this project is to try to identify if a controller can output certain banned coordinates by analyzing slippi files.**

This methodology has several key benefits:
1. You can't get around it because even if they hide their illegal coordinates behind some fancy button combination during some pre-check, if they use it during a game that has a slippi file, they will be caught.
2. You can still test before playing by having them plug their box into a game before entering bracket
  - The end goal would be to have it work on an ongoing slippi stream so TOs could just plug in a box, spam a bunch of buttons, and then see if it raises any errors
3. If the community ever changes rules for what are acceptable coordinates, the coordinate files can be updated and changed (we don't need a single solution that works for everyone, just a framework).

# In-Depth Approach:
- Make groups of banned coordinates into geojson files (overkill but geopandas is very fast for determining if things are in zones, it is also easy to graph)
- Load a .slp file and then check if either player is using a ATD controller (n unique inputs below some threshold)
- If using a ATD controller, check if any coordinates overlap with banned coordinates
- Output some visualization of the outputs and if it passed the tests.