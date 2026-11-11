---
name: remodel-a-plan
description: Remodel an existing floor plan with the 4Lines connector. Use when the user describes, sketches or sends the plan of a flat or house that already exists and wants rooms joined, split, moved or resized, a kitchen opened to the living room, or a renovation drawn with what is demolished and what is new.
---

# Remodel a plan

A remodel starts from what is there. Draw the existing state first, exactly as given, then change it the way an architect would: interior partitions move freely, a facade does not move without the user's permission, and anything the user has locked stays where it is.

## Order of work

1. **Draw the existing plan** on a draft (`create_plan`), with the measures the user gives: `add_walls` (facade usually 0.30 m, partitions 0.10 m), `add_openings`, `set_room`. When the user describes a renovation, mark what exists today with `phase: "inicial"`, what comes down with `"derribo"` and what is new with `"nueva"` (the default); the editor then shows the initial state, the final state and demolition plus new work.
2. **Read it before changing it.** `describe_plan` gives every room with its area, its doors and how it is reached from the entrance; `validate_plan` lists what already does not work; `view_plan` with `annotate: ["ids", "dimensions"]` shows the wall ids to refer to. Tell the user what the plan has before proposing what to change.
3. **Change it with the editing tools**, each with its own reach:
   - move a partition: `update_wall` with `move_m` + `towards` (the walls that die into it follow, and anchored doors and furniture keep their place along it);
   - remove a partition: `delete_wall`, then `delete_room` on the label it leaves without a space; take a door out with `delete_opening`, never by deleting its wall;
   - new partitions: `add_walls` with `parallel_to` + `at_m` for an exact clear width;
   - doors: `update_opening` to move, widen, re-hang or turn one sliding; `hang_doors` after the rooms are relabelled.
   `references/dwelling.md` and `references/doors.md` are the rules the result is judged by.
4. **Furnish what changed** with the room composers (see the `furnish-a-room` skill), with `openings_policy: "keep"` when the user wants doors and windows left as they are.
5. **Check and show.** `validate_plan` and `describe_plan` again, `measure` with `kind: "route"` from the entrance to any room whose access changed, then `view_plan` and the `claim_url`.

## Defaults

- An interior partition can be moved or removed without asking; a facade wall needs the user's permission (for a bathroom row, `design_bathroom` takes it as `may_move_facade: true`, and its error carries `question`, the question for the user with the wall and the centimetres).
- A wall or an opening marked `locked` keeps its body and its place.
- A partition is not moved if it leaves a corridor under 0.90 m.
- A cramped day zone beside a dedicated entry or hall: removing that partition and the label it leaves is the right correction; say what was removed and what the day zone gained.

## What a good result looks like

- What the user asked for, and nothing else moved without being said.
- The final state passes `validate_plan`: no `room_unreachable`, no `room_only_through_private`, no `sealed_space_without_room`, passages of 0.90 m or more.
- Every change listed for the user in words of the trade: which wall moved and how much, which door changed, which rooms grew or shrank and by how many m2.

## Design principles behind the rules

The rules in `references/` are the ones the 4Lines server applies, in its own words; who calibrated them is in the plugin README. On remodelling:

- Walls may move to distribute the spaces better, in a non-substantial way. Square bathrooms work badly.
- If the living-dining-kitchen is too small, the entry can be removed and joined to the living room.
- An interior partition moves when it can, and not for a small toilet; no corridor is left narrower than it should be because of it.
- Windows are adjusted to the layout unless they are locked.

## References

- `references/dwelling.md`: circulation from the front door, standard room sizes and minimum passages. Read it before proposing a change.
- `references/doors.md`: hinged or sliding, which way a leaf opens, what the composers may change in a door or a window.
