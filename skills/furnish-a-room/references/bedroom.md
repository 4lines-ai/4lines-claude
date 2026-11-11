# Bedroom

<!-- Generated from the rules the 4Lines MCP server states. Each rule is the exact text the server states; do not edit by hand. -->

Which bed by room area, the 2.60 m square of a double, the headboard wall, the wardrobe behind the door, bedside tables and the desk.

These rules are word for word what the 4Lines server states in the places named under each one. The same list comes back from the server with `get_capabilities` and `topic: "bedroom"`.

## Rule 1

THE BED FOLLOWS THE ROOM AREA: under 8 m2 one single bed; from 8 m2 two single beds side by side (one if two do not fit); from 10 m2 a double.

Stated in: `design_bedroom`.

## Rule 2

So OMIT bed — do not make every bedroom a double — unless the user asked for a particular bed.

Stated in: `design_bedroom`.

## Rule 3

The minimum mental model for a double bedroom is a 2.60 x 2.60 m SQUARE — the bed plus 0.60 m at its foot and 0.50-0.60 m on each side. The arithmetic closes on the nose: 55 + 150 (double bed) + 55 = 260. A room 2.60 m wide already takes the bed ACROSS it, headboard on the long wall.

Stated in: `design_bedroom`.

## Rule 4

THE HEADBOARD GOES AGAINST A BLIND WALL — not under a window while there is an alternative.

Stated in: `design_bedroom`.

## Rule 5

THE WARDROBE GOES BEHIND THE DOOR when the door sits by a corner: on the wall PERPENDICULAR to it, hinge side, starting at that corner, so the open leaf stands flat in front of the wardrobe fronts and the two share the same floor — you are never in a doorway and at an open wardrobe at once. It needs 0.65 m between the hinge jamb and the corner (0.60 m of wardrobe depth plus 0.05 m for the leaf); a door within 0.90 m of the corner that leaves less is slid along its wall to make it, and that shows up in openings_adjusted. When the door is too far from any corner for that, the older rule takes over: an off-centre door leaves 0.60-0.70 m or more of wall beside it, and that strip is where the wardrobe goes. Either way it is SIZED TO THAT WALL — never a token 1.20 m module floating on a 3 m wall — and keeps 0.60 m clear in front of its doors, checked against the bed and not just against the wall. It never goes in front of a window: it stops at the jamb.

Stated in: `design_bedroom`.

## Rule 6

BEDSIDE TABLES TOUCH THE BED, one per side when the gap takes one; the side that does not take one comes back as a warning saying how much wall was left there.

Stated in: `design_bedroom`.

## Rule 7

NO DESK unless the user asked for one — send desk:true only then.

Stated in: `design_bedroom`.

## Rule 8

THE BED FOLLOWS THE ROOM AREA, and a bedroom always gets its wardrobe: under 8 m2 one single bed; from 8 m2 two single beds (one if two do not fit); from 10 m2 a double. Do not make every bedroom a double: ask for a double or twin only when the user said so. A double bed needs the 2.60 x 2.60 m square (0.60 m at its foot, 0.50-0.60 m each side), so a room 2.60 m wide takes it ACROSS, headboard on the long wall. With its wardrobe it needs 2.60 x 3.10 m (1.90 bed + 0.60 pass + 0.60 wardrobe facing its foot) or 3.20 x 2.50 (wardrobe along the side wall). Headboard against a blind wall (not under a window if there is an alternative). WARDROBES GO BEHIND THE DOORS: on the wall PERPENDICULAR to the door, hinge side, from that corner — the open leaf then stands in front of the fronts, and doorway and wardrobe share the same floor. With no door by a corner, the older trick: an off-center door leaves 0.60-0.70 m of wall beside it and that strip is where the wardrobe goes (beside_opening). The wardrobe stretches along the wall it occupies: size it to the wall, not to a token 1.20 m. Keep 0.60 m free in front of wardrobe fronts; bedside tables touch the bed. No desk unless the user asked for one or the room is explicitly a study.

Stated in: `get_capabilities.furnishing_guide.bedroom`.
