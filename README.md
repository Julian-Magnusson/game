# Neon Flight

Play at **https://julian-magnusson.github.io/game/**.

Windows starts with city and Sewer meshes instead of compiling the large ray-tracing shaders.
Small separate passes restore neon glow, theme skies/weather, filtered windows/brickwork,
wet surfaces and warm underground lamps. Bright lighting works in ordinary color buffers.
Clustered rooms, glass sheen, height fog, animated ring halos and broader glow match the phone
style. Wet streets reflect buildings through a small geometry pass, and Sewer water reflects
its lamps. These effects keep bounded shaders, real depth and fallbacks when effects fail.
The latest Windows polish adds hemispheric skylight, warmer sunlight, quieter distant windows,
stronger skyline haze and distinct seeded window patterns. Reflective shop glass, roof panels,
facade framing, edged park paths and finer water ripples enrich close views, using the same
six small shaders and ordinary RGBA8 buffers.
Automatic resolution starts at 1080p and adapts; selected resolution settings are honored.
Real obstacles, course layout and depth occlusion stay intact. Optional effects have a readable
fallback. Mac and mobile keep the full renderer, with a simpler display fallback
for optional effect failures. Graphics interruptions stop rendering without automatic reloads;
the full renderer offers a single **use compatibility graphics** switch. Interruptions are
remembered so later visits use compatibility rendering. Saved progress and preferences are preserved.
**Settings → Graphics → Graphics report** provides copyable browser, adapter/backend and shader
details for troubleshooting; it also remains available after a graphics interruption. No player
progress or course codes are included, and nothing is sent automatically. Use the ordinary play
URL so healthy phones/Macs retain their full renderer.

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
streets with stopped traffic and four generous escape rings ahead of the entrance. A brief
guided entry aligns the flight during the red warning and alarm, then restores manual control.
Nearby buildings and burning trees topple sideways while thousands more buildings fall
throughout the skyline. The route ends at a rocky park hill with a broad tunnel entrance,
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
Some park corners rise into grassy hills with trees and bushes rooted at their actual height;
walking paths, fountains and benches keep flat foundations. Ordinary course layouts and medal
times stay unchanged.

This repository contains the published single-file build, `index.html`. Development sources,
tests and the project plan live in the separate `game-demo` workspace.
