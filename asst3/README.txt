List of all files you modified or added:

Added:
  asst3/.vscode/tasks.json          (build task, see the compile instructions)

Modified:
  asst3/asst3.cpp
  asst3/matrix4.h


Note the platform you used for development (Windows, OS X, ...):

macOS 26 on Apple Silicon (arm64), with the Xcode Command Line Tools
(clang++ / make) and VS Code. Not tested on Windows or Linux.


Provide instructions on how to compile and run your code, especially if you used a nonstandard Makefile, or you are one of those hackers who insists on doing things differently.

Homebrew is not installed here, so glfw and glew live in ~/cs1750-deps/prefix
(static libraries). The Makefile is unchanged and defaults to /opt/homebrew:

    make HOMEBREW_PREFIX="$HOME/cs1750-deps/prefix"
    ./asst3

.vscode/tasks.json sets the same variable for Cmd+Shift+B. With Homebrew a plain
`make` works.


Indicate if you met all problem set requirements (more importantly, let us know where your bugs are and what you did to try to eliminate the bugs; we want to give you as much partial credit as we can).

All four steps are done. linFact/transFact were checked numerically (T*L == M).
Orbit keeps the sky camera's distance to the world origin; ego motion keeps its
position. No known bugs.


Provide some overview of the code design. Don't go into details; just give us the big picture.

Two cube frames in g_objectRbt next to g_skyRbt; getRbt(i) returns frame i
(0 = sky, 1/2 = cubes), used for both the eye (g_viewIndex) and the manipulated
object (g_objIndex). Every mouse motion builds x-rotation, y-rotation and
translation matrices, inverts them when the object is the eye, and applies
O <- A Q A^-1 O with the auxiliary frame A:
  cube:            transFact(cube) * linFact(eye)
  sky, orbit:      y: world-world, x: world-sky, translation: sky-sky
  sky, ego motion: y: sky-world,   x: sky-sky,   translation: sky-sky
The sky camera cannot be moved from a cube view.


Let us know how to run the program; what are the hot keys, mouse button usage, and so on? Describe steps or sequences of steps the TF should take to test and evaluate your code (especially if your implmenentation strays from the assignment specification).

  h            help menu
  v            cycle eye: sky camera, cube 1 (red), cube 2 (blue)
  o            cycle manipulated object: sky camera, cube 1, cube 2
  m            toggle orbit / ego motion (sky object with sky eye only)
  f            toggle flat shading
  s            screenshot to out.ppm
  Esc          quit
  left drag    rotate (left/right about y, up/down about x)
  right drag   translate in x and y
  middle drag, left+right drag, or space+left drag   translate in z

Cube manipulation from a cube view is allowed and uses the cube-eye mixed frame.


Finally, did you implement anything above and beyond the problem set? If so, document it in order for the TFs to test it and evaluate it.

No extra features.
