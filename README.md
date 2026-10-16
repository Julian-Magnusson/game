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
release worked on the reported Radeon RX 5700 XT with ANGLE/Direct3D11. Its latest report
confirms that all five city programs prepare in 128–1,746 ms, the Sewer program in 2,766 ms,
and initial program preparation in 4,587 ms.
Context loss and restoration follow one submitted 2560×1271 frame; successful GPU
completion is not established. Runtime stability remains unresolved, with no confirmed driver
defect or specific failing draw.
The player also reports failure at 640×360, so native pixel count alone is not an adequate
explanation. ANGLE may compile another executable for the first draw's output-attachment layout;
initial link readiness does not exclude this. It remains a possibility, not a confirmed cause.
The full city renderer now uses five separate programs for intersection, reflected-ray preparation,
building materials, street materials and composition. Reflected rays are computed once and
cached so tracing and shading use the same direction. Each submitted fragment source is under
30 KB, replacing the previous 106 KB combined city shader. They preserve the full graphics and
reflections with the same 120/40-cell tracing budgets. Eight draws per horizontal band reuse
eight full-precision RGBA32F scratch textures, capped at 32 MiB (33.6 MB) in steady use and
64 MiB (67.1 MB) briefly during resize. Final-image and post-processing targets are additional;
output resolution is preserved.
New reports distinguish observed context loss from timeout recovery. A [standalone per-draw
runtime probe](https://julian-magnusson.github.io/game/graphics-runtime-probe.html?v=4fa453b)
checks the remaining failure: generate it in the development repository with
`node tools/probe-city-runtime.mjs --prepare-only`, open it and explicitly press **Run**.
It checks resources, real output-attachment layouts and GPU-fenced completion between draws.
A startup-resolution controller prototype is held back because it reduced image resolution too
aggressively in browser validation. Neither is a confirmed Windows fix; stable AMD/Direct3D11
gameplay still needs confirmation.
A standalone city compiler probe is available in the development repository for isolating
shader preparation from the rest of startup.
Nine local scene comparisons against the original renderer with a shared reflection ray retain
at least 99% identical display channels; differences are at most three 8-bit code values, confined
to three isolated Arctic Dawn pixels above one code. The raw original comparison also preserves
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
