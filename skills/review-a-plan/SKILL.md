---
name: review-a-plan
description: Review a floor plan with the 4Lines connector the way an architect would. Use when the user asks whether a plan works, what is wrong with it, whether it meets the usual room sizes and passages, or asks to check and fix a plan that was just drawn.
---

# Review a plan

A review reads the plan with the server's measurements, not by eye: the server computes areas, clear passages, door swings and the route from the front door on the same geometry its checks use. The judgement is then the architect's rules in `references/`, and a finding is worth raising only when there is a real alternative.

## Order of work

1. **Run the checks.** `validate_plan` returns every finding with a stable `code`, a severity, the ids involved and, for most door findings, the exact `update_opening` that fixes it, already checked against the geometry (`swing_read.fix`). Empty findings with a full `checks_run` list is a clean bill of health.
2. **Read the plan room by room.** `describe_plan`: each room's area and size, its doors (which way each opens, what blocks it), its windows and the facade they face, `from_entrance` (the rooms and doors crossed to get there, or `reachable: false` with why), the free meters on every side of every piece, and the `unnamed_areas` with no room label.
3. **Measure what is in doubt.** `measure`:
   - `kind: "route"`, `from: "entrance"`, `to` a room, `min_width_m: 0.9`: the route, its length, its narrowest point and up to four tight spots;
   - `kind: "clearance"` on a piece or a door: the free space on each side, the leaf sweep and the 0.60 m passage strip of the doorway;
   - `kind: "distance"` between two elements; `kind: "fits"` for where a piece of a given size stands.
4. **Look.** `view_plan` with `annotate: ["tags"]` writes the kind and size of every piece and every opening on the drawing; with `room_id` (or `box_m`) it returns a close-up of one room. Where Claude shows interactive apps, every `view_plan` call adds another viewer card to the conversation, so keep the looks to the ones the review needs.
5. **Judge against the rules** in `references/`, room by room, and report in the words of the trade: what does not work, by how much, and the change that fixes it. When the user wants the fixes applied, apply them, then run `validate_plan` again.

## What the checks find, and how much weight each has

- **Access.** `room_unreachable`: a room that cannot be reached from the entrance. `room_only_through_private`: a room reached only by crossing a bedroom or a bathroom (a bathroom, walk-in closet, terrace or balcony off its own bedroom, and a store room, are not flagged; a bathroom off a bedroom counts as an en-suite only when the level has another bathroom reached without crossing one). Each comes with its route and, when one door fixes it, the `add_openings` that does.
- **Sealed spaces.** `sealed_space_without_room`: an enclosed space with no room, no door and no window, 1.00 m2 or more and at least 0.80 m wide on average, is a warning; with windows it is probably a light well, narrower a built-in wardrobe or a wall cavity, smaller a services shaft, and the finding says so as information.
- **Sizes.** `room_too_small_to_furnish`: a room under what its label needs (a full bathroom under 2.40 x 1.40 m cannot take basin, wc and shower in a row). `narrow_hallway`, `tight_clearance`, `door_narrower_than_passage`.
- **Doors.** `door_swing_blocked`, `door_swings_collide`, `doorway_obstructed`, `door_swing_hits_wall`, `sliding_no_pocket`, `door_opens_away_from_room`, `door_sweeps_into_hallway`, `door_between_private_rooms`, `bath_opens_to_living`.
- **Furniture.** `furniture_overlap`, `furniture_inside_wall`, `furniture_front_blocked`, `furniture_blocks_window`.
- **Light.** `room_without_window`; `window_below_daylight_ratio` is information only, and only for bedrooms and living rooms.

## Doctrine that looks like a defect and is not

- **A wardrobe behind the door.** If it fits, wardrobes go BEHIND the doors: on the wall perpendicular to the door, on the hinge side, from the corner, with the open leaf standing a few centimetres from the fronts. That is the rule, not a defect. Do not report it.
- **A sofa in front of a window** can be acceptable, depending on the case. A tall piece in front of a window is the fault.
- **A door or a window slid along its own wall** by a room composer is normal practice and comes back in `openings_adjusted`.
- **An interior door of 0.70 m, and an entrance door of 0.80 m**, are acceptable.
- **A bathroom slightly under 1.40 m wide** is composed with less clear floor in front of the wc rather than refused; each centimetre makes it less practical, not wrong.

## What a good review looks like

- Every finding with its measure: "the bathroom is 2.10 x 1.35 m; the row of basin, wc and shower needs 2.40 x 1.40 m", never "the bathroom is small".
- Findings in order of what matters to living in the plan: access and circulation, then room sizes, then doors, then furniture.
- Only what has a real fix, and the fix named: which wall, which door, how many centimetres.

## Design principles behind the rules

The rules in `references/` are the ones the 4Lines server applies, in its own words; who calibrated them is in the plugin README. The checks are meant to take the possibilities into account and not to be too aggressive: a finding is worth raising only when there is a real alternative.

## References

- `references/dwelling.md`: circulation, standard room sizes and minimum passages.
- `references/doors.md`: hinged or sliding, which way a leaf opens.
- `references/kitchen.md`, `references/bathroom.md`, `references/bedroom.md`, `references/living.md`: the rules of each room, to judge its furniture.
- `references/furniture.md`: the rules for pieces placed one by one (clearances, the kitchen run, tables with their chairs).
