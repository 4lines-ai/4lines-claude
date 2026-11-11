# Placing furniture by hand

<!-- Generated from the rules the 4Lines MCP server states. Each rule is the exact text the server states; do not edit by hand. -->

What add_furniture works to for pieces no room composer places: bed sizes, the strip beside a door, clearances, the kitchen run and its modules, wall units, appliances, tables with their chairs and custom symbols.

These rules are word for word what the 4Lines server states in the places named under each one. The same list comes back from the server with `get_capabilities` and `topic: "furniture"`.

## Rule 1

Beds, by size: bed = the classic 1.35 double for small/medium bedrooms; bed_double 1.50x1.90; bed_queen 1.50x2.00; bed_king 1.80x2.00; bed_single 0.90x1.90.

Stated in: `add_furniture`.

## Rule 2

THE STRIP BESIDE A DOOR is where the wardrobe goes, and you can say it that way: beside_opening:"opening_1" + a face parks the piece flush against the jamb, in the free run between that opening and the end of its wall (beside_side picks which end; the default takes the longer one).

Stated in: `add_furniture`.

## Rule 3

PLACE LIKE AN ARCHITECT: bedside tables touch the bed sides; leave 0.70 m+ of circulation in front of doors and furniture.

Stated in: `add_furniture`.

## Rule 4

KITCHENS: kitchen_counter is ONE continuous run against a wall — set width_m to the full length (e.g. 3.20) instead of stacking several counters.

Stated in: `add_furniture`.

## Rule 5

Any slot takes w, its width along the run in meters (0.30..1.20, default 0.60 — real openings come in 0.45 / 0.60 / 0.90), and two neighbours that do not both fit share the gap between their centers instead of overlapping.

Stated in: `add_furniture`.

## Rule 6

A column takes appliance:"fridge" for a PANELLED fridge — a tall unit with the fridge inside, which is not the same as the free-standing kind "fridge" piece.

Stated in: `add_furniture`.

## Rule 7

Uppers hang OVER the base units (0.35 m deep against the wall, drawn dashed) so they may share a position with them, but never put one over a column or a fridge, and never across a window.

Stated in: `add_furniture`.

## Rule 8

Free-standing appliances — fridge, dishwasher, microwave, washing_machine, dryer — are their own pieces IN LINE with the run (same wall, same depth) or in the laundry room; never on top of the counter, never floating in the middle of the room.

Stated in: `add_furniture`.

## Rule 9

TABLES: table_dining and table_round COME WITH CHAIRS automatically, sized to the table — do NOT place chair pieces around a table (kind "chair" is for desks and standalone seats).

Stated in: `add_furniture`.

## Rule 10

Draw like an architect: a closed outline plus a few interior lines, not a rendering.

Stated in: `add_furniture`.
