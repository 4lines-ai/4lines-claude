# Bathroom

<!-- Generated from the rules the 4Lines MCP server states. Each rule is the exact text the server states; do not edit by hand. -->

The linear row of basin, wc and shower with its steps and minimum sizes, the compact row, the shower stretched to the width and the double basin.

These rules are word for word what the 4Lines server states in the places named under each one. The same list comes back from the server with `get_capabilities` and `topic: "bathroom"`.

## Rule 1

the fixtures go in a ROW along the LONG wall, in this order — basin, then WC, then shower — with steps of 10 / 20 / 20 cm between pieces. That row fits a 2.40 x 1.40 m bathroom, which is the minimum; 1.50-1.55 m of width is the comfortable one.

Stated in: `design_bathroom`.

## Rule 2

The arithmetic closes on the nose: 10 + 60 (basin) + 20 + 40 (wc) + 20 + 90 (shower) = 240.

Stated in: `design_bathroom`.

## Rule 3

ON A SHORTER WALL THE ROW TURNS COMPACT before giving up: the shower tray shrinks to 0.80 and then 0.70 m, and only then the basin to 0.50 and 0.40 m — down to a 2.00 m row. A bathroom narrower than 1.40 m is composed down to 0.50 m of clearance in front of the wc, and the reasoning says so.

Stated in: `design_bathroom`.

## Rule 4

THE SHOWER BUTTS AGAINST THE FAR END AND IS STRETCHED TO THE WIDTH of the bathroom — a default 0.90 x 0.90 tray floating in a 1.50 m wide bathroom is the mistake this tool exists to stop.

Stated in: `design_bathroom`.

## Rule 5

WHAT IT WORKS OUT FOR YOU: which long wall is eligible (it stops at the partitions and never runs across a door), which end of it you come in through — the basin goes by the door and the shower at the back — the 0.70 m left clear in front of the wc and the basin, and every position along the wall.

Stated in: `design_bathroom`.

## Rule 6

A DOUBLE BASIN GOES IN BY ITSELF when the wall leaves 0.60 m over that minimum row: the basin comes out 1.20 m wide, which is what a basin past 1.10 m is drawn as. In a LONGER row the wall left over the double basin spreads the row instead of piling it at the door: the steps between pieces grow to 0.30 and then 0.40 m, the shower to 1.20 m, and what is still left goes half to the entrance and half before the shower.

Stated in: `design_bathroom`.

## Rule 7

Keep 0.70 m free in front of wc and basin, and no door swinging into fixtures. The most optimized bathroom is elongated and LINEAR at 1.50 m width, in order basin, then wc, then shower at the end — an optimized default, not dogma: the layout depends on where the walls already are. THE ROW, WITH NUMBERS: in a rectangular bathroom put the three along the LONG wall with steps of 10 / 20 / 20 cm between pieces. It fits a 2.40 x 1.40 m bathroom, which is the standard minimum; 1.50-1.55 m of width is the comfortable one. In a very small bathroom the shower tray goes down to 0.70-0.80 m and the basin to 0.40 m wide (a 2.00 m row), and the width a little under 1.40 m, each centimetre making it less practical. Anchor all three to the same wall with against_wall + a face and place them along it with t. A DOUBLE BASIN when the wall leaves 0.60 m over that row: 1.20 m wide, which is what a basin past 1.10 m is drawn as.

Stated in: `get_capabilities.furnishing_guide.bathroom`.
