# Bomberman World — Kotte Bomberman

**Student:** Henri Welling

## How to play

- **Controls:** Move with "WASD" or Arrow keys, place a bomb with "Space", remotely detonate placed bombs with "E", restart the round with "R", and quit with "Q" or "Escape".
- **Objective and rules:** Defeat any 5 enemies across the map to win; touching an enemy or a bomb blast kills the player and ends the round in a loss. If player death and defeating the 5th enemy happen in the same frame, player death takes priority and the round ends as "LOST". The player starts with a blast range of 1, can place up to 3 active bombs at once, blasts trigger chain reactions on other live bombs, and green pickups scattered across the map increase blast range up to a maximum of 5.
- **Configurations / demo setup:** Default configuration spawns the player in the top-left corner at (2, 2) with a small clear starting corner, while crates, patrolling enemies, and blast-range pickups are scattered across the 200x120 room.

## Features and validation

| Feature | Check, observed result, and expected behaviour |
| --- | --- |
| 1. Player damage and death | I walked close to an enemy inside the same spatial grid cell without overlapping its collision footprint (no damage occurred), then walked directly into an enemy in one attempt and stood in a explosion in a second attempt. In both contact cases the player was destroyed once, the round stayed "LOST", and further blasts on that tile did not trigger duplicate destructions, matching expected behaviour. |
| 2. Round states and objective | I defeated 5 enemies in one round and let an enemy/blast hit me in another round, then tried moving and placing bombs after each round ended. The state changed to "WON" at 5/5 enemy kills and "LOST" on death, and all movement, bomb placement, and fuse countdowns stopped while active blast visuals finished fading, matching expected behaviour. |
| 3. Safe restart | I defeated 2 enemies, placed 3 bombs, detonated one so a blast effect was active while two live bombs remained on the map, ended the round, and pressed "R" three times in a row. All old entities, pending requests, and blast effects were cleared, and the new round started cleanly with 0/5 kills, 0/3 active bombs, and blast range 1, matching expected behaviour. |
| 4. Solid bombs with owner escape | I placed a bomb with "Space" (including while wedged in a corner below and next to crates), pressed `Space` again on the same tile, walked off the bomb, tried to walk back onto it, and watched an enemy collide with a newly placed bomb while I still overlapped it. The bomb spawned visibly on my floor tile, duplicate placement was rejected, the enemy was blocked immediately, and I could walk off the bomb once before being blocked from re-entering until detonation, matching expected behaviour. |
| 5. Blast-range pickup | I placed a bomb at initial range 1, collected a green pickup before that first bomb detonated, placed a second bomb, walked over the pickup's former tile again, and collected additional pickups across the map. The first bomb still detonated with range 1 while the second used range 2, revisiting the empty pickup tile had no effect, and collecting more than four pickups kept the range capped at 5/5, matching expected behaviour. |
| 6. Multiple bombs per owner | I pressed "Space" four times across adjacent tiles, waited for one bomb to detonate, and immediately pressed "Space" again. Only 3 bombs were placed (3/3), the fourth attempt was rejected, and capacity returned to 2/3 as soon as the first bomb was destroyed so a replacement bomb could be placed, matching expected behaviour. |
| 7. Chain reactions | I placed two bombs on adjacent tiles with staggered timing so the first bomb's blast ray reached the second bomb before its fuse expired. The first blast immediately triggered the second bomb and destroyed it without a second explosion occurring later when its original fuse would have ended, matching expected behaviour. |
| 13. Remote-detonated bombs | I placed two bombs and pressed "E" to detonate them early, pressed "E" several times with no bombs active in the world, and then placed another bomb and let its normal fuse expire. Pressing "E" safely detonated all active player-owned bombs immediately, pressing it with no bombs present caused no issues, and normal fuse countdowns still worked when "E" was not pressed, matching expected behaviour. |

**Known issues:** None known after testing.

## Sources and assistance

This project builds on the shared Kotte foundations.

None beyond the course material.