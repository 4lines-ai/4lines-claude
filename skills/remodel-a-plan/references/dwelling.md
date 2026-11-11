# Laying out a dwelling

<!-- Generated from the rules the 4Lines MCP server states. Each rule is the exact text the server states; do not edit by hand. -->

How the rooms of a home are arranged and sized: the circulation from the front door, standard room sizes, minimum passages, the circulation rules of a room program and what its total area measures.

These rules are word for word what the 4Lines server states in the places named under each one. The same list comes back from the server with `get_capabilities` and `topic: "dwelling"`.

## Rule 1

LAY OUT THE DWELLING AS NEUFERT WOULD, OR BETTER, leaning modern: an open day zone (living, dining, kitchen), the least corridor possible and rooms of good proportions.

Stated in: `apply_plan_json`.

## Rule 2

WALK IT FROM THE FRONT DOOR: the entry is the head of the hallway, ONE circulation that reaches every bedroom and bathroom without crossing the living room, and the day zone hangs off it — open, or behind wide sliding doors. The hallway ends at the last door it serves: the floor it would run past belongs to the room at its end.

Stated in: `apply_plan_json`.

## Rule 3

Bedrooms together, wet rooms back to back, one door between two rooms.

Stated in: `apply_plan_json`.

## Rule 4

Rooms read as rectangles about 1.2-1.7 times longer than wide: one far longer than that says a partition is in the wrong place.

Stated in: `apply_plan_json`.

## Rule 5

EACH ROOM TO ITS STANDARD SIZE, minimum then usual: full bathroom (basin + wc + shower) 2.40 x 1.40 m, 1.50-1.55 m of width the one that works and about 1.70 x 2.80 when there is room — 5 m2 is already generous in a flat, a bathroom is never a tube; ensuite 3.5-6 m2; toilet 1.00 m wide, 3-4.5 m2; bedroom with its bed and wardrobe: a double 2.60 x 3.10 or 3.20 x 2.50, two singles 2.30 x 3.10 or 3.50 x 2.50, one single 1.40 x 3.10 or 2.10 x 2.50, usually 9-13 m2 and the master 12-18; kitchen 1.80 m wide, 8-14 m2; living-dining-kitchen 3.00 m wide, 22-45 m2; entry 1.30 m wide, 3-6 m2 on its own (6-8 above 120 m2); laundry 2.5-5 m2.

Stated in: `apply_plan_json`.

## Rule 6

Spare area goes to the day zone and the bedrooms, never to corridors or to stretch a bathroom.

Stated in: `apply_plan_json`.

## Rule 7

MEASURES ARE FLOORS, NOT TARGETS: corridors, and the clear floor IN FRONT OF every door, never under 0.90 m; door leaf 0.80 m. Draw ABOVE the minimums, not AT them: a room drawn exactly at its floor has nothing to give when the room beside it needs 10 cm, and what gets eaten is always the passage.

Stated in: `apply_plan_json`.

## Rule 8

validate_plan measures the floors; only view_plan shows you the route, so look at a new layout and walk it from the front door before you furnish it.

Stated in: `apply_plan_json`.

## Rule 9

CIRCULATION IS PART OF THE PROGRAM, and the server rejects the call (invalid_program, nothing spent) before the engine runs when it is missing. Three rules: (1) an "entry" room is REQUIRED as soon as the room bands add up, at their midpoints, to more than 25 + 15 x bedrooms m2 — only tighter programs may let the LDK absorb the entrance; give the entry 3-6 m2, or 6-8 above 120 m2. (2) Two or more bedrooms REQUIRE a "hallway" (3-6 m2) serving the night zone: bedroom and bathroom doors never open straight into the living space. (3) With two or more bedrooms, every bedroom and every full_bathroom needs an adjacency edge to the hallway (or to the entry).

Stated in: `solve_program`.

## Rule 10

Total BUILT area of the dwelling in m2, to the outer face of the facade walls. The engine does not size the envelope from it but from the room bands, or from boundary_polygon when one is sent; area_reading gives the built area of each variant against this figure.

Stated in: `solve_program.programs.area_total_m2`.

## Rule 11

Think in CIRCULATIONS and in the area you are distributing, always. When space is tight, circulation is what gets optimized: fewer dedicated halls, tighter passages, access straight into the day zone. With generous space, be generous. The doors an earlier layout left are a DRAFT, not law: while furnishing, sliding a door along its wall or flipping its swing to free the right wall for furniture is normal practice — bathrooms almost always need it.

Stated in: `get_capabilities.furnishing_guide.general`.

## Rule 12

Keep 0.90 m of clean passage; wardrobe or bench on the side clear of the door swing. When the dwelling is tight on area, the entry can open STRAIGHT into the living-dining-kitchen — the day zone absorbs the entrance instead of a dedicated hall. AND ON A PLAN ALREADY DRAWN, not just a fresh one: if the day zone is cramped while a dedicated entry or hall beside it holds floor, delete_wall on that partition plus delete_room on the label it leaves behind is the right correction — say what you removed and what the day zone gained. An interior partition needs no permission; a FACADE wall does.

Stated in: `get_capabilities.furnishing_guide.entry`.
