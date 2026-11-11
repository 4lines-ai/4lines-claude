---
name: design-a-home
description: Lay out a new flat or house with the 4Lines connector. Use when the user asks for a floor plan of a home from a room program, a number of bedrooms and bathrooms, a total area in m2 or a footprint, or wants alternative layouts of a dwelling to choose from.
---

# Design a home

A home is drawn in three passes: the walls and the rooms, the doors, then the furniture. Each pass is checked with the server's own measurements before the next one starts, because a bathroom that is 0.70 m short is cheap to fix while it is still four walls and expensive once the flat is built around it.

## Order of work

1. **Read the brief.** Number of bedrooms and bathrooms, the total area, whether it is a flat or a house, the shape of the plot or footprint if there is one. A total area given by the user is the BUILT area, measured to the outer face of the facade walls (see "Where the rules come from").
2. **Create the draft.** `create_plan` returns the `plan_token` every other tool takes and the `claim_url` the user opens to see and save the plan.
3. **Draw the shell and the rooms.** Two paths, and they mix well:
   - `solve_program`, for residential programs only: describe the rooms with an area band each and how they connect (`adjacency_graph`). The engine returns up to 6 variants as one contact sheet, with the area of every room, `recommended` and `recommendation_blockers`. Send `boundary_polygon` (counter-clockwise, in meters) when the footprint is fixed, and two alternative programs to explore two circulation patterns. Then `apply_variant` with the one you pick; rooms come back under your program ids. 3 solves per plan per day.
   - `apply_plan_json` for the whole document in one call, or `add_walls` + `set_room` by hand. Partitions are 0.10 m by default and a facade is usually 0.30 m; `add_walls` with `parallel_to` + `at_m` gives a room the exact clear width you ask for.
   Either way, follow `references/dwelling.md`: it is the rule set the engine and the server check against.
4. **Label every room.** `set_room` with the closed `label_key` list (`entry`, `hallway`, `ldk`, `full_bathroom`, `master_bedroom`...); `custom_name` carries the user's own wording. One name per enclosed space; an open living-dining-kitchen is one `ldk`.
5. **Doors and windows.** `add_openings` with `opens_into` (or nothing) and the server hangs each door into the room it serves; `hang_doors` rehangs every door once the rooms are labelled. Which leaf (hinged or sliding) follows `references/doors.md`.
6. **Check the bones before furnishing.** `validate_plan` (text, cheap), then `describe_plan` to read every room with its area, its doors and how it is reached from the entrance, and `view_plan` to see it. `measure` with `kind: "route"`, `from: "entrance"` and `min_width_m: 0.9` walks to a room and names the narrowest point. Fix what the findings name, and validate again.
7. **Furnish.** Follow the `furnish-a-room` skill: `design_kitchen`, `design_bathroom`, `design_bedroom` and `design_living` lay out a whole room in one call each, and each answer's `summary` is that room in one line for the user.
8. **Show it.** `place_camera` inside the main room, looking across it (cameras are where the user renders from in the editor), `view_plan` for the final look, and give the user the `claim_url`.

## Defaults

- Interior door leaf 0.80 m; windows 1.20 x 1.20 m with a 0.90 m sill unless the brief says otherwise.
- Corridors and the clear floor in front of every door: never under 0.90 m.
- With two or more bedrooms, a hallway serves the night zone; the entry is the head of that hallway.
- A single bathroom in the home: 1.50 m wide is better than the 1.40 m minimum.
- Spare area goes to the day zone and the bedrooms, in proportion, not to corridors or to stretch a bathroom.

## What a good result looks like

- `validate_plan` with no warning left, or only findings that are explained to the user.
- `describe_plan`: every room `reachable` from the entrance, no bedroom or bathroom reached only by crossing another bedroom or bathroom, and no `unnamed_areas` that should be a room.
- Rooms near their usual size from `references/dwelling.md`, about 1.2-1.7 times longer than wide, and a total built area close to what was asked (`solve_program` reports it per variant in `area_reading`).
- The day zone open, the hallway ending at the last door it serves, wet rooms back to back.
- The user has the drawing and the link.

## Design principles behind the rules

The rules in `references/` are the ones the 4Lines server applies, in its own words; who calibrated them is in the plugin README. The principles that matter most when laying out a home:

- No long corridors: layouts leaning modern, laid out as Neufert would, or better.
- A home of X m2 means X m2 BUILT, outer walls included.
- When it is the only bathroom of the home, 1.50 m of width works better than the 1.40 m minimum.
- Rooms can be large, but in proportion to one another.
- When the day zone cannot take three separate zones, the dining table goes with the kitchen.

## References

- `references/dwelling.md`: circulation from the front door, standard room sizes, minimum passages, the circulation rules of a room program and what the total area measures. Read it before drawing the first wall.
- `references/doors.md`: hinged or sliding, which way a leaf opens, and what the room composers may change in a door or a window. Read it when placing doors.
