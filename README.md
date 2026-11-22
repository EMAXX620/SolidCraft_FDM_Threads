FDM 90° THREADS PLUGIN FOR SOLIDCRAFT
Version 1.9.1
======================================================================

<img width="1141" height="525" alt="image" src="https://github.com/user-attachments/assets/f0070607-03c7-4f99-b78b-7ce9988485f7" />

1.9.1 has fixes for SolidCraft 0.45.0

WHAT IT IS
----------
SolidCraft is a CAD program for designing 3D parts. This plugin adds
threads (like on a bolt or a nut) that are designed for FDM 3D printing.

Ordinary threads are hard to 3D print well: their slopes are too flat to
print cleanly, and parts that should screw together often come out too
tight. These threads fix both problems:

  - Their sides slope at 45° (a 90° angle between the two sides). Most
    printers can print a 45° slope without support, so the threads come
    out cleanly whether the part is printed upright or upside down.
  - The thread is shallow, with wide flat tops and bottoms, which makes
    it strong and easy to print.
  - You choose a clearance (extra gap) so the bolt and nut fit together
    after printing instead of jamming.

The sizes and measurements come from a popular Fusion 360 thread file
("FDM90 Metric Trapezoidal Threads"). If you've used those threads in
Fusion 360, these are the same, and bolts and nuts from either program
fit each other.


WHAT YOU NEED
-------------
  - SolidCraft (the desktop version).
  - The file fdm90-threads.zip. This is the plugin. Don't unzip it;
    SolidCraft installs the zip directly.

The file fdm90-threads-source.zip is only needed if you want to look at
or change how the plugin works (see "THE SOURCE CODE" below). You don't
need it to use the plugin.


HOW TO INSTALL
--------------
  1. Open SolidCraft.
  2. Go to Preferences > Plugins.
  3. Click "Install plugin..." and choose fdm90-threads.zip.
  4. Click Install.

Two new buttons appear on the ribbon (the toolbar along the top), in a
group called "Plugins":

  FDM Thread  - adds a thread to a shaft or a hole you've already drawn
  FDM Rod     - makes a new threaded rod

They're also in the Plugins menu, as "Thread a face" and "Threaded rod".
Both buttons have the same plug icon, because SolidCraft doesn't let
plugins choose their own icons yet.

To update to a newer version: in Preferences > Plugins, click Remove on
"FDM 90° Threads", then install the new zip. Threads you made with the
old version stay as they were; to change them, delete them and make them
again.


HOW TO USE IT
-------------

FDM Thread: add a thread to a shaft or a hole

  1. Draw your part as usual, with a plain round shaft (for a bolt) or a
     plain round hole (for a nut).
  2. Click the curved side of the shaft or hole to select it.
  3. Click FDM Thread. A window opens with these settings:

     Remember Settings/Use Last Settings
                  Tick this to reuse the settings from the last time
                  you ran it in this design. The plugin then ignores
                  the other settings in the window (but still uses the
                  face you selected). The first time, nothing is saved
                  yet, so it uses the settings in the window and saves
                  those. Every run saves its settings in the design
                  file, so they're still there after you save, close
                  and reopen it. To change them, untick the box and run
                  with the new settings.
                  The window itself always opens with the standard
                  settings showing; SolidCraft doesn't let plugins
                  change that.

     Thread type  "external" for a shaft or bolt,
                  "internal" for a hole or nut.

     Diameter     The thread's size. "auto" works it out from the shaft
                  or hole you selected. Each size in the list also shows
                  the pitches it comes in, for example:
                    20 mm  (pitch 2, 3, 4)

     Pitch        The distance from one thread to the next, in mm.
                  "auto" picks the usual pitch for that diameter. The
                  list shows every pitch for every size; if you pick one
                  the diameter doesn't have, the plugin tells you which
                  ones it does have.

     Clearance    The extra gap that lets printed parts screw together,
                  from 0.000 to 0.500 mm. 0.100 to 0.200 is a good place
                  to start. Use the same clearance on the bolt and the
                  nut that go together.

     Thread ends  "both": the thread runs all the way to both ends.
                  "picked": it runs to the end nearest where you clicked
                  the face, and stops half a thread short of the other.
                  "none": it stops half a thread short of both ends.

     Hand         "right" (normal: tighten clockwise) or "left".

     Chamfer      A 45° bevel at the open ends of the thread. It makes
                  the bolt and nut easier to start screwing together,
                  and removes the thin, weak half-thread at the start.
                    "auto"   - as deep as the thread itself (on a hole
                               this makes a countersink)
                    "custom" - the size you type in Chamfer size
                    "none"   - no chamfer
                  Ends that meet a base, a shoulder or the bottom of a
                  blind hole are never chamfered.

     Chamfer size Only used when Chamfer is "custom": how far the bevel
                  reaches, in mm.

     Length       Leave empty to thread the whole shaft or hole.

     Body, Point on face X / Y / Z
                  Only needed if you didn't select a face in step 2:
                  type the coordinates of a point on the shaft or hole
                  instead.

  4. Click Run.

Things to know:
  - The plugin resizes the shaft or hole to the exact size the thread
    needs, the way Fusion 360 does. For example, a 20 mm shaft with
    0.100 clearance is trimmed to 19.8 mm.
  - The thread never cuts into anything past the ends of the shaft or
    hole, such as a base, a shoulder or a bolt head.
  - The thread is made from ordinary SolidCraft steps: cylinders, a
    chamfer, one sketch (the thread's profile), a coil and a combine. They're all put into
    one folder on the timeline, named after the thread, for example
    "FDM90-20x4 0.100e thread", so the timeline stays tidy. Click the
    folder to open it and see the steps inside. Suppressing or deleting
    the folder does the same to the whole thread. Undo removes all of
    it in one go.
  - The thread's sketches are put into one group of the same name in
    the browser's Sketches folder, and hidden once the thread is made,
    so the finished part shows on its own. To see them again, click
    the eye on that group in the browser.
  - The thread doesn't update itself. If you later change the size of
    the shaft or hole, delete the thread's steps from the timeline and
    run FDM Thread again.
  - The shaft or hole must be a complete, unbroken cylinder.

FDM Rod: make a threaded rod

  Makes a new, separate part: a rod threaded along its whole length. You
  choose the diameter, pitch, clearance, length, which way it points
  (X, Y or Z), where it starts, and a chamfer for both ends (the same
  choices as on FDM Thread). "Remember Settings/Use Last Settings"
  works here too.

  It's useful for:
  - Test prints. Print a short rod and a block with a hole threaded at
    the same size, and try a few clearances to see which fits your
    printer best before printing the real part.
  - Making bolts: make a rod, then add a head to it.
  - Lead screws and other long threaded rods.


SIZES
-----
  - 77 diameters, from 3 mm to 320 mm, with 249 diameter and pitch
    combinations in total.
  - Everything from 6 mm to 320 mm comes from the original Fusion 360
    thread file.
  - 3 mm, 4 mm and 5 mm were added: 3x1, 4x1, 4x1.5, 5x1 and 5x1.5.
    They're built with the same formulas as the rest of the table.
    Threads this small are at the limit of what FDM printers can do.
    Print them upright with a 0.4 mm nozzle or smaller and 0.12 mm
    layers or thinner. For 4 and 5 mm, the 1.5 pitch prints more
    reliably than 1.
  - Small pitches only go up to a smaller clearance: 0.125 mm at pitch
    1, 0.175 mm at pitches 1.25 and 1.5. The plugin tells you if you
    pick more than a size allows.


IF SOMETHING GOES WRONG
-----------------------
  "This entry needs to be run from the agent or CLI"
      The plugin is too old for your SolidCraft. Install the newest
      fdm90-threads.zip.

  "select a cylindrical face (a shaft or a hole) first..."
      Nothing round was selected. Click the curved side of the shaft or
      hole before clicking FDM Thread, or type a point into X, Y, Z.

  "no FDM90 size is near it"
      The shaft or hole isn't close to any thread size. Choose the
      diameter yourself instead of "auto".

  "... has no N mm pitch; choose ..."
      That pitch doesn't exist for that diameter. Pick one of the
      pitches the message lists, or "auto".

  "a N mm chamfer is more than the ... shaft can take"
  "the chamfers at the two ends would meet"
      The custom chamfer is too big for the shaft or rod. Make it
      smaller, or use "auto".

  "... goes up to a N mm clearance"
      That size's pitch is too fine for the clearance you chose. Pick a
      smaller clearance.


THE SOURCE CODE (fdm90-threads-source.zip)
------------------------------------------
You only need this to read or change how the plugin works.

How it works, in short: the plugin is a small program written in C and
compiled to WebAssembly (a format SolidCraft runs safely inside itself).
It can't draw anything by itself. It works by sending SolidCraft the same
commands you could run yourself: make a sketch, draw the thread's shape,
sweep it around a spiral, cut it from the part. The finished result is
ordinary SolidCraft geometry.

Files:

  plugin.json
      The plugin's description for SolidCraft: its name and version, the
      two buttons, the settings each one shows (with the Diameter and
      Pitch dropdown lists), which SolidCraft commands it may use, and
      its limits on time and memory.

  src/plugin.c
      The plugin itself. It:
        - finds the shaft or hole you selected and measures it exactly
          (where it starts and ends, and how big it is)
        - picks the thread size and the measurements for the clearance
        - checks whether each end is open or meets more of the part (a
          base or a shoulder), so it doesn't cut into what's past the end
        - resizes the shaft or hole to the right size, with Cylinder
          features (no sketches)
        - chamfers the open ends with SolidCraft's Chamfer, if a
          chamfer was chosen
        - draws the cross-section of the thread groove: 45° sides, flats
          at the right depth
        - sweeps that shape along a spiral, trims it to the ends, and
          cuts it from the part
        - puts everything it made into one timeline folder, and its
          sketches into one browser group, then hides the sketches
        - saves the settings it used in the design, for "Remember
          Settings/Use Last Settings", and reads them back when that
          box is ticked
        - or, for FDM Rod, makes the rod first and then does the same

  src/json.c, src/json.h
      A small tool for reading and writing JSON, the text format the
      plugin uses to talk to SolidCraft.

  threads_table.h
      The table of thread sizes and their measurements for each
      clearance, compiled into the plugin. It's generated by
      gentable.py, so don't edit it by hand.

  threads.json
      The complete original Fusion 360 thread table, turned into a
      simpler format.

  threads_used.json
      The sizes the plugin actually uses: up to 320 mm, plus the added
      3, 4 and 5 mm sizes.

  parse.py
      Reads the original Fusion 360 file
      (FDM90MetricTrapezoidalThreads.xml) and writes threads.json.

  gentable.py
      Writes threads_used.json and threads_table.h from threads.json,
      leaving out sizes over 320 mm and adding 3, 4 and 5 mm. To add or
      remove sizes, change this script and run it again.

  build.sh
      Builds the plugin file, fdm90-threads.wasm. It needs three free
      tools: wasi-sdk (a C compiler for WebAssembly), wit-bindgen and
      wasm-tools. The script's comments say where it expects them.

  wit/plugin.wit
      SolidCraft's official description of how plugins talk to it. The
      build uses it.

  test/
      Tests that run without SolidCraft:
        host.c, driver.c, compose.wac, wit/
            A pretend SolidCraft that answers the plugin's commands and
            prints them, so you can check what the plugin would do.
        check_fit.py
            Checks every bolt and nut pair at every clearance, to make
            sure they fit together without touching.
        check_manifest.py
            Checks plugin.json against SolidCraft's rules, so it will
            install and its settings window will work.

To rebuild after a change:
  1. If you changed the sizes: python3 gentable.py
  2. ./build.sh
  3. Put plugin.json, README.md and build/fdm90-threads.wasm in a folder
     called fdm90-threads, and zip that folder. That zip is what you
     install in SolidCraft.
