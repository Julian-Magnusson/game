# Neon Flight

Play at **https://julian-magnusson.github.io/game/**.

Every browser and operating system now starts with the same full city and Sewer renderer,
including Chrome and Edge on Windows. Old saved fallback/interruption flags are ignored.
Automatic resolution adapts to frame cost, with selected resolution settings as pixel ceilings.
Optional effect failures have a readable display fallback. Graphics interruptions stop rendering
and flight without automatic reloads; the full renderer offers a single **use compatibility graphics**
switch that opens `?graphics=safe`. Failures do not save a graphics preference for later visits.
`?graphics=safe` explicitly selects the optional compatibility renderer. It retains meshes of the
real world, theme skies/weather, detailed buildings, park planting and warm Sewer brickwork/lamps,
with six small shaders, ordinary color buffers and bounded reflections/glow. Removing that URL
option restores full graphics on the next visit. Saved progress and preferences are preserved.
**Graphics error screen → Graphics report** provides copyable browser, adapter/backend, shader
preparation phases/times, source fingerprints and pending-program details. It remains available
after a graphics interruption, with pending durations frozen when rendering stops. Phase labels
identify the last submitted operation, not a proven
failing driver stage. No player
progress or course codes are included, and nothing is sent automatically. The earlier mesh
release worked on the reported Radeon RX 5700 XT with ANGLE/Direct3D11. An earlier report
confirms that all five city programs prepare in 128–1,746 ms, the Sewer program in 2,766 ms,
and initial program preparation in 4,587 ms.
Context loss and restoration follow one submitted 2560×1271 frame; successful GPU
completion is not established. Runtime stability remains unresolved, with no confirmed driver
defect or specific failing draw.
The player also reports failure at 640×360, so native pixel count alone is not an adequate
explanation. ANGLE may compile another executable for the first draw's output-attachment layout;
initial link readiness does not exclude this. It remains a possibility, not a confirmed cause.
The standalone 64×36 report now shows GPU-fenced completion of every resource setup stage,
then context loss during the first primary `city:trace` attempt with four RGBA32F outputs.
That narrows the failing stage without distinguishing native compilation, trace execution or
attachment writes as the underlying cause.
An interim compact-hit report stops before creating any shader or resource because WebGL2 is
unavailable. It does not test that renderer. A fresh full browser restart is needed for the next
check; repeated-loss blocking is one possible cause. The diagnostic captures the browser's
context-creation error message when available.
After fully exiting and reopening Chrome, context creation succeeds, followed by context loss
during shader preparation around 2.95 seconds. Several city programs are pending, so that report
does not identify which compiler job caused the reset. City programs now prepare one at a time,
with later sources queued, and the moving-fire calculation is invoked once after tracing instead
of through repeated early-return calls. Full graphics remain; Windows stability still needs confirmation.
The latest fresh Windows report (build 7cdcb0a) prepares movers in 150.3 ms and portal geometry
in 100.1 ms, then loses/restores the context while preparing only city:trace-static after 1452.3 ms.
The remaining city programs are queued and no world resources or city draws exist yet. This
isolates static preparation, without proving a specific internal driver defect.
Static geometry now uses one flat bounded loop for cell and primitive iteration, with no light
accumulator or depth output. A separate light pass replays exactly the visited cells, preserving
stationary fire and booster glow before moving fire. The geometry and light fragments are
16,151 and 11,008 bytes; the seven other city sources remain unchanged. Hit IDs and visited counts
share a finite normal float32 packet, preserving full precision without adding textures.
The actual pipeline matches 861 canonical GPU rays across 13 worlds/frames exactly for distance,
winning ID and glow, including maximum-part cells and 1/2/40/120-cell limits. All nine displayed
640×480 scene captures are identical to the preceding release. Storage tests recover 306 final
and 400 intermediate packets exactly. Local 1080p seam/resize/failure checks pass; these checks
preserve graphics locally and do not establish Radeon/Direct3D11 stability.
The full city renderer uses nine separate programs: five intersection/light stages, cached
reflected-ray preparation, building materials, street materials and composition. Each fragment
source is under 36 KB, replacing the previous 106 KB combined city shader. The same 120/40-cell
tracing budgets and full graphics remain on every browser. Sixteen draws per horizontal band
reuse four RGBA32F and two D32F scratch textures, capped at 18 MiB in steady use and 36 MiB briefly
during resize. Materials recover original attributes and analytic normals from the selected
primitive without another city walk. Final-image and post-processing targets are additional;
output resolution settings are preserved.
New reports distinguish observed context loss from timeout recovery. A [standalone per-draw
runtime probe](https://julian-magnusson.github.io/game/graphics-runtime-probe.html)
checks the remaining failure: generate it in the development repository with
`node tools/probe-city-runtime.mjs --prepare-only`, open it and explicitly press **Run**.
It checks resources, real output-attachment layouts and GPU-fenced completion between draws.
For a fresh test use [diagnostic 2, build 10c201c](https://julian-magnusson.github.io/game/graphics-check-10c201c78213.html).
Its unique address, visible build and ISO run time distinguish the new attempt from an older
loaded page or report. Copy and Save become available after completion or interruption;
clipboard failure selects the report and explains how to copy it manually.
A startup-resolution controller prototype is held back because it reduced image resolution too
aggressively in browser validation. Neither is a confirmed Windows fix; stable AMD/Direct3D11
gameplay still needs confirmation.
A standalone city compiler probe is available in the development repository for isolating
shader preparation from the rest of startup.
Nine local 640×480 scene comparisons against the original renderer with a shared reflection ray
differ by at most one 8-bit color value per channel. The raw original comparison also preserves
the same visible detail and features, with small floating-point differences in its rain ripples.
This checks graphics locally; Windows AMD runtime stability still needs confirmation.
Use the ordinary play URL for the same full renderer everywhere.

Fly through a generated city with mouse/keyboard on desktop, or phone tilt and an optional
touch stick on mobile. Find stars on harder detours, finish the course to save them, then spend
them in Shop. Saved stars are shared across difficulties; unfinished finds are lost on leaving
the course or starting a new attempt.
Course and flight summaries show collected slots without a lifetime “Stars saved” total.
Shop shows the stars still available to spend after purchases.

The **Collapse Key** costs **10 stars**. Its mysterious **MM:SS** hint changes with the selected
Hard/Extreme course and difficulty.

Look for glitching red windows and banners with white warning signs around the entrance
between buildings. Extreme has a short opening for the departure. Collapse follows crowded
streets with stopped traffic and four generous escape rings ahead of the entrance. Flight stays
fully manual, preserving the live heading, pitch, bank, speed and steering input on entry.
The first arc adapts to the incoming direction so the next ring is visible and reachable,
without temporary steering assistance or a camera alignment blend. The route ribbon is hidden;
the highlighted next ring and HUD arrow remain visible.
Nearby buildings and burning trees topple sideways while thousands more buildings fall
throughout the skyline. The route ends at a pointed mountain on a larger park plot, about
82 units high with a 135×149-unit local footprint. Six angular ridge pieces and four low boulders
have matching visible and collision surfaces. The broad tunnel entrance has
broken metal bars, a stone arch and warm Sewer-style brickwork and lamps. Fly gently downhill
to the fifth ring inside. A Collapse crash returns to the normal surface course.

Once discovered, **The Sewer** has playable courses through cylindrical collectors, smaller
connecting tunnels, and winding upward/downward chambers. Dodge round pipes and dirt banks;
the murky green water causes a crash, like the street above. Every underground crash restarts
the entire course with a fresh timer. Four difficulties, course codes and medals work
underground, with records kept separate from the city.
Completing Collapse gives 2.5 seconds of black, the white **The Sewer** chapter card, then opens
the Sewer menu directly. The menu previews the actual starting
tunnel, keeping the same scenery through **3, 2, 1, Go**. Brickwork, arch detail, lamps, services,
stone ledges and drains carry the menu's detail into the course. Side flows match their inlet's
flat waterline and full width before spilling into the lower collector. The manhole menu button
switches between the Sewer and the surface. **Undertow** provides the underground soundtrack.

Arctic Dawn has snowy trees and frozen fountains. Surface rain and snow stay above ground.
Some park parcels rise into broad grassy hills 7–10 units high, with raised lawns about
24–26 units across. Trees and bushes follow their actual height, and walking paths climb the
slopes. Fountains and benches keep level foundations. Avenue lanes remain roads through parks;
tree trunks and benches stay outside traveled streets and intersections, with bus stops and
shop-front benches on sidewalks. Ordinary course layouts and medal times stay unchanged.

This repository contains the published single-file build, `index.html`. Development sources,
tests and the project plan live in the separate `game-demo` workspace.
