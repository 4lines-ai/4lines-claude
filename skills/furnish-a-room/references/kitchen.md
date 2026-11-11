# Fitted kitchen

<!-- Generated from the rules the 4Lines MCP server states. Each rule is the exact text the server states; do not edit by hand. -->

The kitchen layouts and how they are scored, what is worked out on each wall, the dining table that comes with it and the length of the run.

These rules are word for word what the 4Lines server states in the places named under each one. The same list comes back from the server with `get_capabilities` and `topic: "kitchen"`.

## Rule 1

It lays out every layout the room allows — a straight run on each wall, an L at each free corner, a U, a run with an island in front, a run closed by a peninsula — composes each one and scores them: the sink under a window, the work triangle opening across a corner, worktop length, 1.00-1.20 m of passage between fronts, no door or window forced to move, nothing collided with, and in a kitchen or an ldk the room left for the dining table in front of the run.

Stated in: `design_kitchen`.

## Rule 2

WHAT IT WORKS OUT FOR YOU on any wall: how much of it is really free — it stops at the partitions, never runs across a door AND never leaves the room, however far the wall goes on — the 60 cm modules counted from the corner, the sink on the module under the window, the hob clear of the inside corner and of the fridge, the dishwasher next to the sink, and the fridge at one END of the run so the worktop stays in one piece.

Stated in: `design_kitchen`.

## Rule 3

THE DINING TABLE COMES WITH THE KITCHEN in a kitchen or ldk room: parallel to the run, centred in the free depth in front of the run: at least 1.20 m off the worktop (1.00 when tight) and at most 1.50 in a wide room, the rest left on the far side; the wing of an L keeps the same pass. Behind the island if there is one, sized to the room (2.20 x 1.00 for 8-10 in a generous room, 1.80 x 0.90 for 6, 1.50 x 0.90 for 4) with 0.75-0.90 m clear round it, clear of the doors and of what is already there.

Stated in: `design_kitchen`.

## Rule 4

HOW LONG THE RUN COMES OUT: by default what the program asks for plus two free worktop modules, capped to the free wall.

Stated in: `design_kitchen`.

## Rule 5

Several valid types: a straight/L/U run working the sink-stove-fridge triangle; an ISLAND for modern open plans; a peninsula closing an L. PREFER THE L when the room offers a free corner: turn the run around it (two arms) instead of one straight strip. Sink under the window when there is one; 1.00 m (ideally 1.20) between facing runs. A KITCHEN IS TWO HALVES: the base units and the WALL UNITS above them (slots kind "upper"). Hang them over the base cabinets, never over a tall column or a fridge — those already reach the ceiling — and never across a window. Module widths are 0.45 / 0.60 / 0.90 (slots w), not one size for everything, and a fridge built into a tall unit is a column with appliance:"fridge" rather than the free-standing piece.

Stated in: `get_capabilities.furnishing_guide.kitchen`.

## Rule 6

Leave 0.75-0.90 m clear around the table to pull chairs out; place it near the kitchen. Size the table to the room and the household: a generous living-dining seats 8-10 at 2.20 x 1.00 m — do not default to the small 1.50 x 0.90 one.

Stated in: `get_capabilities.furnishing_guide.dining`.
