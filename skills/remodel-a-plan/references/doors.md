# Doors

<!-- Generated from the rules the 4Lines MCP server states. Each rule is the exact text the server states; do not edit by hand. -->

Hinged or sliding, which way a leaf opens and which jamb it hangs on, and what the room composers may change in a door or a window.

These rules are word for word what the 4Lines server states in the places named under each one. The same list comes back from the server with `get_capabilities` and `topic: "doors"`.

## Rule 1

DOORS ARE HINGED BY DEFAULT and a door that opens fine stays hinged: one turns SLIDING only when the open leaf sweeps furniture or another door and neither rehanging the hinge nor sliding the opening along its wall frees it — same wall, same position, and it needs as much blank wall beside the opening as the leaf is wide (a pocket door on a partition of 0.10 m or more, surface-mounted on a thinner one). A leaf is never flipped towards a room the door does not serve. Sliding BY DEFAULT for walk-in closets, laundries and pantries, and between the kitchen and the living-dining. Bathroom and bedroom doors: hinged first, sliding only as the last resort when no hinged leaf fits; a bathroom that has to be accessible takes a sliding door more often. NEVER sliding on the entrance or on any door to the outside.

Stated in: `get_capabilities.furnishing_guide.doors`.

## Rule 2

WHICH LEAF TO CHOOSE: hinged is the default and a door that opens fine stays hinged. Sliding by default for walk-in closets, laundries and pantries and for a door between the kitchen and the living-dining; on a bathroom or bedroom door only as the last resort, when no hinged leaf fits, and a bathroom that has to be accessible takes a sliding door more often; never for the entrance or for any door to the outside. A sliding leaf needs as much blank wall beside the opening as it is wide, and validate_plan says so (sliding_no_pocket) when it does not have it.

Stated in: `add_openings`.

## Rule 3

Hangs the hinged doors of the plan the way an architect would, from the rooms it already has: the leaf swings INTO the room the door serves (from the hallway into the bedroom, from the bedroom into its ensuite or walk-in closet, from outside inward, between two rooms into the more private one) and hangs on the jamb nearest the perpendicular wall on that side, so the open leaf folds against it — unless that leaf would sweep furniture and the other jamb would not.

Stated in: `hang_doors`.

## Rule 4

DOORS: the same leaf doctrine as add_openings — prefer subtype:"sliding" for walk-in closets, laundries and pantries and for a kitchen-to-living door; on a bedroom or bathroom door hinged first and sliding only as the last resort, when no hinged leaf fits, and a bathroom that has to be accessible takes a sliding door more often; never for the entrance.

Stated in: `apply_plan_json`.

## Rule 5

With openings_policy:"keep", doors/windows and their host geometry stay unchanged; a new door obstruction rejects the whole layout.

Stated in: `design_kitchen`, `design_bedroom`, `design_living`, `design_bathroom`.

## Rule 6

Otherwise THE COMPOSER MAY RE-HANG OR SLIDE A DOOR OR A WINDOW on the SAME wall when the layout needs it — never onto another wall, never out of the room, never a different width — and reports every such change in openings_adjusted.

Stated in: `design_kitchen`, `design_bedroom`, `design_living`.

## Rule 7

Otherwise THE COMPOSER MAY RE-HANG OR SLIDE A DOOR on the SAME wall when the layout needs it — never onto another wall, never out of the room, never a different width — and reports every such change in openings_adjusted.

Stated in: `design_bathroom`.
