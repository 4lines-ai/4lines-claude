---
name: furnish-a-room
description: Furnish rooms of a floor plan with the 4Lines connector. Use when the user asks to furnish a plan, or to lay out or redo a kitchen, a bathroom, a bedroom or a living-dining room, or to place, move or resize furniture.
---

# Furnish a room

Four rooms have a composer on the server that lays the whole room out in one call, to the rules in `references/`: `design_kitchen`, `design_bathroom`, `design_bedroom` and `design_living`. They measure the room, pick the walls and do the arithmetic, and what comes out is ordinary furniture that can still be moved, resized or deleted. Everything else (a study, a laundry, a single shelf, a piece the catalogue does not have) is placed with `add_furniture`.

## Order of work

1. **Find the rooms.** `query_plan` with `{"filter":{"kind":"room"}}` lists every room with its id, area, size and the doors and windows on its walls. `describe_plan` reads the same rooms with how each is reached from the entrance.
2. **Lay out each room with its composer**, passing `in_room`:
   - kitchen or `ldk`: `design_kitchen`. Leave `shape` and `against_wall` out and the server chooses among a straight run, an L, a U, an island and a peninsula; the answer says `shape_chosen` and why the others lost. In a kitchen or an `ldk` the dining table comes with it.
   - bathroom: `design_bathroom`, the linear row basin, wc, shower.
   - bedroom: `design_bedroom`. Leave `bed` out: the bed follows the room area.
   - living, living-dining or `ldk`: `design_living`, after `design_kitchen` in an `ldk` (a dining table already there stays and the sitting group goes round it).
   Calling a composer again REPLACES what it placed, so a second call with other arguments is how to change a room.
3. **Read what each call says.** `summary` is the layout in one line, written by the server for the user; `reasoning` lists the rules that decided it; `openings_adjusted` lists every door or window the composer re-hung or slid along its own wall; `walls_adjusted` any partition it moved; `warnings` what did not fit and by how much.
4. **Place the rest** with `add_furniture`, to the rules in `references/furniture.md`: `against_wall` + `side` for anything that stands against a wall (the server does the wall-face arithmetic), `x`/`y` only for free-standing pieces. `measure` with `kind: "fits"` gives the places where a piece of a given size stands, with the `place_with` to send. To nudge a piece, `move_furniture` with `along_m` or `dx_m`/`dy_m`, relative to where it is.
5. **Check.** `validate_plan`; `measure` with `kind: "clearance"` on a piece or a door gives the free meters on each side; `view_plan` with `annotate: ["tags"]` writes the kind and size of every piece on the drawing, and with `room_id` it returns a close-up of one room.

## Defaults

- Doors and windows: the composers may re-hang or slide them on the same wall when the layout needs it, and report it. When the user wants every door and window left as it is, send `openings_policy: "keep"`.
- `design_bathroom` slides an interior partition by itself when a room is a few centimetres short; it touches a facade only with `may_move_facade: true`, after the user agreed. When only the facade can give the centimetres, its error carries `question`, the question for the user already written with the wall and the centimetres. `design_bedroom` moves a window on a plan it did not draw only with `may_move_windows: true`, after the user agreed; when a window stays over the headboard for that reason, the result carries `question`.
- No desk in a bedroom unless the user asked for one (`desk: true`).
- Dining table: sized to the room and the household (`seats` when the user said how many they are), not the small 1.50 x 0.90 one by default.
- A studio (one room, several uses) is furnished piece by piece with `add_furniture`: the composers do not coordinate inside a single room.

## What a good result looks like

- Every bedroom with its wardrobe, sized to the wall it occupies, 0.60 m clear in front of its doors.
- The bathroom row on the long wall with the shower stretched to the width, 0.70 m clear in front of the wc and the basin.
- A kitchen that turns the corner when the room offers one, the sink under the window, 1.00-1.20 m between facing runs.
- The sofa anchored and facing the focal point, 0.80 m kept on the routes between doors, the television 2.50-4.00 m from the sofa.
- `validate_plan` with no `door_swing_blocked`, `doorway_obstructed`, `furniture_overlap` or `furniture_front_blocked` left.

## Doctrine that looks like a defect and is not

- **A wardrobe behind the door is the rule, not a fault.** If it fits, wardrobes go BEHIND the doors: on the wall perpendicular to the door, on the hinge side, from the corner. The open leaf stands in front of the wardrobe fronts and the doorway and the wardrobe share the same floor, because nobody is in the doorway and at an open wardrobe at once. With the leaf fully open it can stand a few centimetres from the fronts; that is the design.
- **A sofa in front of a window can be acceptable**, depending on the case. Tall pieces in front of a window (wardrobe, fridge, tall unit) are the fault.
- **Moving a door or a window along its wall to make the room work is normal practice**, not a change to report as a problem, unless the opening is locked.

## Design principles behind the rules

The rules in `references/` are the ones the 4Lines server applies, in its own words; who calibrated them is in the plugin README. Their figures are exact and are not rounded:

- The linear bathroom: basin, wc, shower along the long wall with steps of 10 / 20 / 20 cm; 2.40 x 1.40 m is a minimum that works well.
- The bed by room area: under 8 m2 one bed, from 8 m2 two beds, from 10 m2 a double.
- The television wall stands 2.50 to 4.00 m in front of the sofa, measured from the television to the sofa opposite; a little less or a little more is fine.
- Kitchens: what is easiest to build and fit, covering the usual 95 % of kitchens.

## References

- `references/kitchen.md`: layouts and how they are scored, what is worked out on each wall, the dining table, the length of the run. Read it before a kitchen.
- `references/bathroom.md`: the linear row, its steps and minimum sizes, the compact row, the double basin. Read it before a bathroom.
- `references/bedroom.md`: the bed by area, the 2.60 m square, the headboard wall, the wardrobe behind the door. Read it before a bedroom.
- `references/living.md`: the anchored sofa, the coffee table and routes, the dining table. Read it before a living room.
- `references/doors.md`: hinged or sliding, and what a composer may change in a door or a window.
- `references/furniture.md`: what `add_furniture` works to for the pieces no composer places: bed sizes, the strip beside a door, clearances, the kitchen run, wall units, appliances, tables with their chairs. Read it before placing pieces by hand.
