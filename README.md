# Neon Flight

Play at **https://julian-magnusson.github.io/game/**.

**Windows verification, 2026-10-16:** the player confirms build `3a1dd84` loads and plays in
fullscreen on the reported Radeon RX 5700 XT / Chrome ANGLE Direct3D11 system. It uses the
same full graphics as other browsers, with no compatibility switch needed. The ordered
lighting shader preserves the previous images and resolves the reported startup interruption.

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
The latest fresh Windows report (build 10c201c) prepares the flat static geometry in 383.6 ms,
then loses/restores the context while preparing only city:trace-static-light after 1251.1 ms.
Later city programs are queued and no world resources or draws exist. The remaining failure
is therefore isolated to light preparation, without proving a specific internal driver defect.
Lighting now uses one uniform-bounded loop and explicit near/far booster-ring blocks. Distances
are copied through a tiny 600-byte shader into ordinary R32F color buffers; no city shader writes
fragment depth or enables depth testing. This separates procedural lighting from the native
depth-output path. The other eight city shader sources, including the Windows-confirmed geometry,
remain unchanged. Full graphics, reflections and 120/40-cell traversal budgets remain.
All ten programs and 18 real city draws complete locally. GPU storage recovers 306 final and 400
intermediate packets exactly. The actual pipeline matches 871 canonical rays across 14 worlds/frames
exactly for hit distance, winning ID and glow, including visible near/far booster rings and inside
streaks. All nine 640×480 displayed captures are identical to the preceding release. These checks
preserve graphics locally; Radeon/Direct3D11 stability still needs confirmation. Full-HD
seam/resize/failure cleanup and complete-game startup/flight also pass locally; interrupted
reports remain copyable without querying the lost driver.
The next fresh Windows report (build `a894c3b`) still interrupts while preparing only the
11,349-byte light program (`e87eeed4`) after 1,234.6 ms. Geometry and the new color-only
distance writer are ready, with all later city programs queued and no world resources or draws.
Removing fragment-depth output did not resolve this failure. The player reports that the
smaller graphics option runs without freezing; full graphics remain unresolved on this PC.

The fresh Windows [Diagnostic 3, build d6001ce — lighting state machine](https://julian-magnusson.github.io/game/graphics-light-check-d6001ce6a4ab.html?variant=state-machine)
prepares the new light in 233.7 ms, with no context loss and verified source identity on the
reported RX 5700 XT / ANGLE Direct3D11 backend.
This separate page compiles exactly one selected program when **Run once** is pressed, without
generating a city or drawing frames. It never retries automatically. Copy/Save reports include
the selected source hash, transformations, build and run time; no report controls are added to
the game's menu. Individual selections also isolate beam, fire and traversal work; the full
control retains the failing historical `a894c3b` light source.
The full game now uses the exact light source that passed on Windows: 11,858 bytes / `6d9cd023` /
SHA-256 `f1894d61438178141d927db6c3866274c92dcc3bbd73c666fa19cc47a0d279ce`.
It rewrites the unchanged light math into seven ordered phases per visited cell. All other
nine city program sources, tracing budgets, detail, textures and draw counts remain unchanged.
The exact candidate passes 871 canonical GPU ray comparisons and produces nine PNG-identical
local scene captures. Full-HD rendering, all seven band seams, transactional resizing/failure
cleanup and complete-game startup/flight also pass locally. The 1080p PNG matches the preceding
release. Windows and Mac browser profiles upload identical shaders, and interrupted reports
remain copyable without driver reads. These local profiles use Intel/ANGLE OpenGL.
The standalone test establishes Windows compilation of this one program. The subsequent
full-game build `3a1dd84` is also confirmed by the player to load and play in fullscreen on
the Windows PC. This verifies the reported startup issue, not every theme, course or driver
version. The diagnostic page itself never
changes the game or retries automatically. Its controls remain pinned to historical sources
after the production light is adopted.
The full city renderer uses ten separate programs: six intersection/light/distance stages, cached
reflected-ray preparation, building materials, street materials and composition. Fragment sources
range from 600 to 35,719 bytes. Eighteen draws per horizontal band reuse four RGBA32F and two R32F
color textures, capped at 18 MiB in steady use and 36 MiB briefly during resize, with the same
32-bit precision and memory footprint as the preceding depth buffers. R32F color rendering is
supported by the [existing full-renderer extension](https://registry.khronos.org/webgl/extensions/EXT_color_buffer_float/).
Materials recover original attributes and analytic normals from the selected primitive without
another city walk. Final-image and post-processing targets are additional; resolution settings
are preserved.
New reports distinguish observed context loss from timeout recovery. A [standalone per-draw
runtime probe](https://julian-magnusson.github.io/game/graphics-runtime-probe.html)
checks the remaining failure: generate it in the development repository with
`node tools/probe-city-runtime.mjs --prepare-only`, open it and explicitly press **Run**.
It checks resources, real output-attachment layouts and GPU-fenced completion between draws.
For a fresh full-pipeline test use [diagnostic 2, build f0a4e89](https://julian-magnusson.github.io/game/graphics-check-f0a4e8916c2a.html).
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

Shop has **Gear**, **Themes** and **Music** tabs. **Neon Night** and **Neon Flight** are included
at the start and appear only in Settings. Synthwave Sunset, Amber Haze and Ember City cost
**2 stars**; Toxic Haze and Aurora Night cost **3**; Tokyo Rain costs **4**; Arctic Dawn and
Overgrown City cost **5**. **Skyline Rush**, **Midnight Drift** and
**Afterburn** cost **5 stars each**. Purchases are saved once per browser, and settings reset
keeps ownership. Select owned items in Shop or Settings; locked Settings choices have dimmed
icons and a lock. Random music plays only your owned surface songs. **Undertow** is free upon
discovering The Sewer, plays exclusively underground, and is the Sewer's only song. It is hidden
from surface Settings and Shop. Your
surface music preference returns when you go back up. Existing boosts, keys, star claims and
spending are preserved; cosmetic purchases do not change medals or count as assisted flights.
Themes purchased before the price update retain their original payment in the wallet ledger.

The Gear tab also sells a **Flashlight** for **5 stars**, giving **five Sewer flights**, displayed
as **5 / 5 uses left**. Equip or unequip it in the Shop; Buy returns when it runs out.
Previously paid spare lights stay available. An equipped light uses one charge on Sewer Fly and lasts until you crash,
finish or leave. Pause/resume keeps the same use; surface flights and automatic crash restarts
never consume another. Existing unused lights gain five uses each without changing past
spending. The underwater beam is wider and stronger and cuts through the murk.

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
ordinary murky green water causes a crash, like the street above. Marked flooded sections let
you dive into narrower underwater mazes. A big red arrow painted on a barricade points down into
the water; the barrier and submerged tunnel roofs prevent staying above the maze. At each
fork, bright cyan lights with soft halos sit clearly inside the correct passage and lead toward the outlet.
An iron shutter closes behind the dive, so only that outlet leads back into air. Wrong branches
have capped turning rooms so you can turn back. More underwater service pipes and elbows add
solid obstacles with room to steer around them. Race rings and navigation arrows stay hidden underwater.
An oxygen bar holds **26 seconds** of air and refills after surfacing. Pause freezes it;
running out restarts the course. Mazes occur occasionally on Easy/Medium, twice on Hard and
three times on Extreme. Rising currents carry the outlet climb through the surface while
restoring normal cruising speed. Every underground crash restarts
the entire course with a fresh timer. Four difficulties, course codes and medals work
underground, with records kept separate from the city. The new layout uses version-8 Sewer
records; existing Extreme unlocks, saved stars and shop purchases stay intact.
Normal tunnels also split into passages during flight: one dry fork on Easy/Medium, two on
Hard and three on Extreme. Large red skulls painted onto wooden sluice barricades mark the wrong
entrances in dry tunnels. Only cyan lights mark the underwater route. Capped wrong
branches have enough room to turn back. Normal rings and guidance remain visible in air.
Tiled walkways follow rounded channel edges through bends and joins. Water from side pipes
starts at the visible mouth and falls directly from its curved rim, without a detached gap.
Huge fans span the cylindrical rooms and rotate at varied speeds and directions. Each room
has 1/2/3/3 full crossing fans, 2/3/4/4 rotating sweeper poles, and 2/3/4/5 surging waterfall
obstacles on Easy/Medium/Hard/Extreme. Damaged pipe holes spray smaller decorative water jets,
and chipped rims and cracks surround the outlets. Tunnel fans have solid central hubs; fly
between their blades. Wall fans push air and water through visible streams that you can dodge.
Moving streaks show the current direction, and entering the stream causes sideways drift.
Hard and Extreme include locally tighter stretches of tunnel. Hard and
Extreme include sections with failed lights, leaving rings and nearby obstacles visible; a
flashlight reveals the tunnel ahead. Actual scene lighting fades over about 0.8 seconds in
both directions. Easy and Medium keep working lights. Sewer courses have
**1 star on Easy/Medium, 2 on Hard and 3 on Extreme**. Finish to save them; crashing or leaving
discards pending finds. Saved slots are shared across Sewer difficulties and kept separate from
surface slots, while both environments fund the same shop wallet.
Completing Collapse gives 2.5 seconds of black, the white **The Sewer** chapter card, then opens
the Sewer menu directly. The menu previews the actual starting
tunnel, keeping the same scenery through **3, 2, 1, Go**. Brickwork, arch detail, lamps, services,
stone ledges and drains carry the menu's detail into the course. Side flows match their inlet's
flat waterline and visible opening before spilling into the lower collector. The manhole menu button
switches between the Sewer and the surface. **Undertow** provides the underground soundtrack.

Arctic Dawn has snowy trees and frozen fountains. Surface rain and snow stay above ground.
Some park parcels rise into broad grassy hills 7–10 units high, with raised lawns about
24–26 units across. Trees and bushes follow their actual height, and walking paths climb the
slopes. Fountains and benches keep level foundations. Avenue lanes remain roads through parks;
tree trunks and benches stay outside traveled streets and intersections, with bus stops and
shop-front benches on sidewalks. Ordinary course layouts and medal times stay unchanged.

This repository contains the published single-file build, `index.html`. Development sources,
tests and the project plan live in the separate `game-demo` workspace.
