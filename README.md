# Mega Man X3 Co-op — prototype 0.28

A two-player patch for **Mega Man X3 (USA)** on the SNES. Player 1 is X; **player 2 joins as Zero** on controller 2.
This is an early prototype. It is tested in the intro stage, all eight Maverick stages and their bosses, the four Doppler stages and their bosses (including the Maverick rematches, Dr. Doppler and Sigma), and the Ride Armors.

## New in 0.28: black armor for your Zero in VS mode

- **Whenever you play Zero in VS mode, press L or R on your controller to switch to black armor, and again to switch back.** That's controller 2 in 1P VS 2P, and controller 1 against the CPU gold X and in X + ZERO when you play Zero. It works as in co-op (see 0.25): the weapon-switch sound plays going black and the menu sound going back, and your shots and Z-Saber do double damage, to X or to both CPUs.
- **Measured** with a bot Zero in each setup: the hits that did 1, 2 and 3 did 2, 4 and 6 in black armor, against an X with no armor in 1P VS 2P, against the CPU gold X, and against both CPUs in X + ZERO. X's armor still halves what reaches him, as before.
- It's the same switch as in co-op and Boss Rush as Zero, so it stays on until you switch it back or power off.
- The CPU Zero is unchanged: his look and damage come from the CPU level (black armor on HARD), and L or R on his controller does nothing. In X + ZERO when you play Zero, the CPU Zero already wears black, so with yours on you both do. Your health bar is the one on the left.
- **How it works:** VS mode used to skip the black armor switch. Now a person's Zero as player 2 (1P VS 2P, or against the gold X, where your buttons go in controller 2's place) uses co-op's switch and colors. In X + ZERO you're player 1, and the switch and colors are the ones from Boss Rush as Zero. Each hit from your shots is doubled where VS mode works out its damage, before X's armor. The X + ZERO code that tints your Zero's charge glow now also recognizes his black colors, so it doesn't treat them as a glow, and the glow tints the black armor.

## New in 0.28: the computer Zero climbs ladders

- **When X climbs a ladder, the computer Zero follows him up or down it.** He keeps the ladder's position for 10 seconds after X used it. While X is 32 px or more above or below him and the ladder is within 200 px, he walks to it. Then he presses up (jumping for it if the ladder starts above his reach) or presses down at the top. On the ladder he climbs toward X and steps off at the top or bottom like a player. He doesn't jump or move sideways while climbing, but he still shoots.
- **Before,** he jumped in place under the ladder until the "X far above" catch-up put him next to X after 3 seconds, and to go down he walked off the top and dropped.
- **Tested** on the long ladder in Gravity Beetle's stage (about 240 px): X climbed it, walked on and later climbed back down. Zero went up right behind him, stepped off at the top, followed him down and stepped off at the bottom, with no catch-up warps. In 0.27.1 the same run needed two catch-up warps to get him up, and he came down by dropping off the top of the shaft. Across the 61-section bot sweep (66 minutes with him in) he was within 160 px of X 98.7% of the time and went down 28 times, as in 0.27.1 (98.9%, 28), with no new glitches. With Zero not called, co-op, single-player and VS mode play out update by update the same as 0.27.1, and VS mode plays the same as before when black armor isn't switched on.

## New in 0.27.1: the computer Zero costs lives, and dashes more

- **When the computer Zero goes down, a shared life comes off, as it does for a second player.** He beams back in after the usual delay. With no lives left he stays out until a 1-up, then beams back in on his own.
- **He dashes much more in stages.** Outside boss fights he dashes when he's 64 px or more behind X and heading his way (until he's within 32 px), when he heads for an enemy 136 px or more away (until it's in range), whenever X is dashing, and when the 150 px limit pulls him toward X. A dash runs out after about half a second, so he presses it again right away. In boss fights he only dashes to keep up with a dashing X or when the 150 px limit pulls him, so he keeps his distance from the boss.
- **No dashing on ice.** On Blizzard Buffalo's icy floors a dash keeps sliding well past where it's let go: in testing he slid past X and off ledges into spike pits, 10 times in 84 seconds of the stage's opening. On ice the game keeps his sliding speed in `$0A8C` (0 on other floors). While it's not 0, and for 4 seconds after, he walks, except when the 150 px limit pulls him.
- **Fixed: Zero wedged in scenery.** In one Maverick stage he got stuck in a nook under a low ceiling for half a minute, pushing toward X, who had climbed away. The co-op check for a wedged player 2 never fired, because his attempts to jump kept changing his height. Now, if he pushes a direction for 4 seconds without moving and X is 48 px or more away, he's put next to X.
- **Tested:** a bot playing X through eleven stage sections, once walking and once dashing, kept alive, with Zero along (about 15 minutes). When X dashed, the share of Zero's running done as a dash went from 1–29% in 0.27 to 22–85% (42% or more off the ice), and he was more than 160 px from X less often in 8 of the 11, about as often in 2 and more often in 1. He went down 5 times in those 15 minutes (0.27: 4). In the 61-section bot sweep (67 minutes with him in) he was within 160 px of X 98.9% of the time (0.27: 98.1%). All 28 of his losses there came in the second Doppler stage (0.27: 24, also all there), and none on Buffalo's ice. Against the bosses he does the same 8–46 damage in 50 seconds as in 0.27, and the Boss Rush chain, the lives rules (a 1-up brings him back) and the call, dismiss and take-over flows were rechecked. With Zero not called, co-op, single-player and VS mode play out update by update the same as 0.26.1.

## New in 0.27: a computer Zero

- **Pause with Start and press L on controller 1, and a computer-played Zero comes to help X.** The weapon-switch sound confirms it. When you unpause, Zero beams in next to X as player 2, the way a second player joins, and the game plays him. X stays X: nobody is swapped out. (L does nothing in the original game's pause menu.)
- **Press L in the pause menu again to send him away.** The menu sound plays and he leaves the way player 2 does with Select. Call him back the same way any time.
- **What he does:** he follows X, dashing when he falls behind. When an enemy is on screen he goes after the nearest one (the boss first, in a boss room), keeps about 48–120 px from it, turns to face it and shoots when it's level with him. Ordinary enemies get buster shots. Bosses and tough enemies get a full charge, then the second shot and the Z-Saber. He jumps over whatever blocks him, up to ledges where X or the enemy is, up walls with wall kicks, and over a boss or enemy that charges at him. He never strays more than 150 px from X.
- **Pits and dead ends:** if he falls below the screen while X is still on it, he's put back next to X. The same happens when X has been more than 80 px above or below him for 3 seconds (a ledge he can't get up, or a shaft X dropped down). The usual co-op catch-up warps still apply too.
- **He doesn't cost lives** (changed in 0.27.1: now he does). When he goes down, the lives counter stays the same and he beams back in after the usual delay. When X loses a life, Zero drops out with him and comes back once X has beamed in. He stays with you through stage changes until you send him away or power off.
- **A friend can take over.** Pressing anything on controller 2 hands Zero to that player, and from then on it's normal co-op. To hand him back to the computer, press L in the pause menu.
- He works in normal stages and in Boss Rush as X. VS mode and Boss Rush as Zero don't have him: L in the pause menu does nothing there.
- **How it works:** each frame the computer builds controller 2's buttons, in the place where VS mode's CPU Zero gets his. They go through your button config, so the game reads them like a player's. Its target is the nearest object on screen with health in the enemy list (the boss, when it's on screen). It works out a direction, jump, dash and shot from the distances to the target and to X. When he goes down, the life the co-op code takes off is put back (no longer since 0.27.1).
- **Tested:** a bot playing X through all 61 sections with Zero called (84 seconds each, about 66 minutes of play with him in). He stayed within 160 px of X 98% of the time, with no glitches beyond those seen in normal co-op. Against the eight Mavericks, a Maverick rematch and Dr. Doppler, with X just standing and firing now and then, he did 8–46 damage in 50 seconds and went down at most twice. He also followed X through a Boss Rush chain, two stages in a row. With Zero not called, co-op, single-player and VS mode play out update by update the same as 0.26.1.

## New in 0.26.1: black armor in a Zero rush

- **In Boss Rush as Zero, press L or R on controller 1 to switch to black armor, and again to switch back.** It works as in co-op (see 0.25): every attack does double damage (measured on Blast Hornet: buster 1 to 2), the weapon-switch sound plays going black and the menu sound going back, and the choice lasts until you switch back or power off. Zero has no weapons, so L and R had no other use there.
- **How it works:** each frame, every color of Zero's palette (sprite palette 1) that still matches his own is swapped for the black armor's, and back when it's off, so the charge glow still tints him. In black armor every shot that hits does double, since in a Zero rush all of them are his.

## New in 0.26: Boss Rush as Zero

- **BOSS RUSH now asks first who you play: X or ZERO.** X goes on to the armor and difficulty menus as before. ZERO goes straight to NORMAL / HARD (he has no armor to pick).
- **Zero plays the whole rush alone, with controller 1.** He beams in at every stage start and after every lost life, goes through the boss doors, and fights every Maverick, the final chain and Sigma. In the original game Zero can't fight bosses: a marker before each boss area hands over to X ("Zero, I'll handle this."). In Boss Rush as Zero that hand-over doesn't happen.
- **Losing Zero is a lost life.** In the original, when Zero goes down he says goodbye at the base ("Sorry X... I've failed...") and is gone for good. Here it costs a life, the same as X's death, and he beams back in; a game over works as usual.
- Zero has X's health in Boss Rush (all eight heart tanks), his own buster, charged shots and Z-Saber, and his "Z" icon on the health bar. He takes the weapon after each win as X would, but can't use it, as in the original.
- **Controller 2 can't join a Zero rush.** Start on controller 2 does nothing. To play Boss Rush together, pick X.
- **How it works:** the game itself can run Zero as the player: the player's character byte (`$0A8E`) set to 2 makes the player code, graphics and palette his. The player's start-of-life setup (`$04:80C3`) sets X; in a Zero rush it sets Zero. The boss-area marker (`$01:CEF0`) and the death code (`$04:9345`) skip their Zero cases in a Zero rush.
- **Tested:** both Maverick stages (normal) as Zero, from the stage start through every boss, the weapon get and the next stage; the final chain from Bit to Sigma's second form; a lost life during a fight (one life off, Zero back in); controller 2 pressing Start throughout (no join). Sigma's escape and last form weren't reached by the test bot, as before (see 0.9).

## New in 0.26: no talks in the final chain

- **Bit, Byte, Vile and Dr. Doppler no longer stop to talk in Boss Rush.** Each one appears, fills its health bar and fights. Sigma still has his speech. The intros went from about 10 seconds to 3.5 for Bit, from 12 to under 3 for Vile, and from 33 to under 7 for Doppler (his entrance takes the rest).
- **How it works:** each of them opens the game's dialog box (`$02:FCB1`) and then waits until it closes. In the final chain the box isn't opened for them, so they go straight on.

## Fixed in 0.26: Blizzard Buffalo's ice beam in Boss Rush

- **Buffalo's big freezing beam works again in Boss Rush.** He fights in Neon Tiger's room there, and his beam only grows while its ends stay inside his own boss room, which the game gives as fixed positions in his stage. In another room it stopped after one step: a small crescent at his mouth, and nothing reached across the room. In Boss Rush outside his stage the beam now uses the room on screen, so it crosses the room, freezes whoever it hits and pulls back as in his own stage.

## Fixed in 0.26: pausing during a Boss Rush chain

- **A boss no longer turns into a jumble after the pause menu.** Closing the sub-screen reloads the stage's sprite graphics, and in a chain that brought back the stage's own boss over the one fighting (for example Gravity Beetle's pieces drawn as Blast Hornet). This happened alone and in co-op, as X or Zero, with every boss after the first in each stage. Now, when that reload ends, the fighting boss's graphics are loaded again; it shows its own graphics a moment after the sub-screen closes.

## New in 0.25.1: Boss Rush, each next boss starts with you on the left

- **In a Boss Rush chain, the players are moved to the left before the next boss appears.** Every boss in a chain appears where the stage's own boss did, on the right side of the room, dropping in from the top. If X was standing over there when the last one fell, the new one landed on him. Now, once the next boss is loaded, a player who is right of the left quarter of the room (Zero: right of 96 px) is moved: the screen fades out, X is put 48 px from the left edge and Zero 80 px, both facing right, and it fades back in (about half a second in all). Then the boss appears. A player who is already on the left stays where he is, and if nobody has to move there's no fade.
- This applies to every chain: the Maverick chains in Gravity Beetle's and Neon Tiger's stages, and the final chain in Sigma's room (Bit, Byte, Vile, Dr. Doppler and Sigma). The first boss of each stage is reached through its door as usual, with X already on the left.
- **Tested:** the all-eight chain in Neon Tiger's stage alone and with Zero, the normal chain in Gravity Beetle's stage with Zero, and the final chain from Bit to Sigma alone and with Zero, with X put next to each boss as it fell. Every next boss appeared with the players on the left, facing it, and no one was hit as a boss appeared. Outside Boss Rush nothing changes: a normal stage, a boss fight and VS mode play out exactly as in 0.25, alone and with Zero.

## New in 0.25: black Zero

- **Press L or R on controller 2 to switch Zero to black armor, and again to switch back.** In black armor every attack Zero has does double damage: buster shots, the charged shot, the second shot after it and the Z-Saber (measured on a boss: 1→2, 2→4, 1→2 and 16→32). There's no catch. It's a straight boost for whoever plays Zero, the harder of the two to play. X's damage doesn't change.
- Switching to black plays the weapon-switch sound, switching back the menu sound. The choice lasts through deaths and stages until you switch back or power off.
- It works in co-op and Boss Rush. Bosses still have their 50% extra health in co-op (see 0.5), so against a boss black Zero lands about 1.3x what Zero does in the original game. Regular enemies take the full 2x.
- In VS mode L and R do nothing (Zero's damage there is set by the CPU level), and the HARD CPU Zero keeps his own black armor.
- If the game's button options put shot, jump or dash on L or R, that button keeps its job and only the other one switches.
- In Volt Catfish's stage, at the moments Zero borrows X's colors (see Known issues), he shows in X's blue in black armor too. The double damage still applies.

## Fixed in 0.25: Bit and Byte in Boss Rush

- **Bit and Byte look like themselves again.** In the final chain (see 0.9) both were drawn in scattered pieces, Byte as a small red jumble instead of his full size, and Byte's talk before the fight turned into garbage partway through. This had been there since 0.9.
- **What went wrong:** the chain starts the two of them past their opening steps, the ones that check whether enough Mavericks are beaten. Those steps also give the boss its sprite set, its boss-bar id and a few starting values. Without the sprite set they were drawn from the wrong sprite data, and that is also what scrambled Byte's text. The chain now runs that setup itself before each of them appears.
- **Tested:** the final chain from Bit to Vile, alone and with Zero joined: both are drawn whole through their entrances, talks and fights, the text reads clean, and losing a life during Byte brings Bit back looking right.

## Fixed in 0.24.1: boss rooms

- **Zero can wall-jump up one wall while X is on the other.** Zero is kept within 192 px of X so the camera can show both of them. A boss room fits on one screen, but its walls are about 210 px apart, so with X on one wall, Zero was held about 20 px short of the other and couldn't reach it to wall-jump. The limit no longer applies where the camera can't scroll (boss rooms and other one-screen rooms): the room's own walls keep both players on screen there.
- **Pressing Start during a boss's intro no longer freezes Zero.** Zero joined in X's intro pose and kept it for the whole fight, unable to move. Now a Start press during the intro (or a boss-door walk, a victory pose or a teleport) waits, and Zero joins as soon as it's over. The other moments when Zero can't join (the READY at a stage start, while X rides a Ride Armor) hold on to the Start press the same way instead of dropping it. Losing a life or leaving the stage cancels it.
- **Zero no longer beams in inside a boss room's wall.** He appears 32 px behind X. Boss fights start with X near the left wall, so that spot was inside the wall, and Zero was stuck until the anti-stuck warp moved him 4 seconds later. If the spot behind X is within 24 px of the screen's left edge, he now appears 32 px in front of X instead.

## New in 0.24: a glitch hunt

The bot from 0.23 played every stage, checkpoint and boss in co-op again (about 11 hours of play per run), this time also watching for glitches: freezes and crashes, Zero vanishing while on screen, sprites drawn from the wrong graphics or in the wrong colors, sudden camera jumps, level graphics that failed to load, and values out of range. Every hit was saved with the inputs that led to it, so it could be replayed frame by frame. No freezes, crashes or level-graphics failures turned up. Fixed:

- **Crush Crawfish's claw holds one player at a time.** The claw goes for the nearer player. If the other one came closer during a grab, the boss switched to him halfway through, the hold flipped back and forth between the two, and Zero could vanish until it ended. An enemy now keeps aiming at a player it is holding or has just hit, until that player is free.
- **Zero no longer vanishes when the sprites run out.** The SNES shows at most 128 sprites. In the Doppler stage 2 boss fight the boss and its effects can use all of them, and Zero, drawn last, was cut off for as long as that lasted. While they're all in use now, X and Zero take turns being drawn first, so each one flickers instead of Zero disappearing.
- **Joining while X's special-weapon shot is still out.** When Zero joins, X goes back to the buster (see 0.4.4), but the game only allows that switch with no shot on screen. If an Acid Burst puddle, say, was still there, X kept the weapon, and its graphics and Zero's overwrote each other. Zero now beams in as soon as X's special-weapon shots are gone, at most about 8 seconds later (a Tornado Fang drill stuck in a boss lasts about 5). While he waits, a moment when joining isn't allowed (X starting a new move, a cutscene) no longer cancels the join; it goes ahead right after.
- **Doppler stages: X's shield and charge effects no longer garble Zero.** In these stages the body armor's shield and the charge sparkle draw from the sprite memory Zero uses, so they're kept off while Zero is in (see 0.4.4). One that was already on screen when Zero joined kept going, and it and Zero showed pieces of each other's graphics until it ended. They're now removed when Zero joins.
- **Volt Catfish's stage: Zero's first frame is red.** Zero borrows sprite palette 7 in that stage (stage 5; see 0.4.4), but the check ran before he joined, so his first frame was drawn in X's blue.

Less slowdown in some of the busiest moments:

- **Platforms with Zero nearby.** When a platform aimed at Zero, holding both players up on it swapped Zero's fields out and back in around every check. It now goes straight to what each check needs, and carrying a player is a plain position update with no swap at all. This was checked update by update against the previous build on all 61 sections: the game plays out the same.
- **Enemies don't switch players over a few pixels.** An enemy aims at the nearer player. When both are about equally near (within 16 pixels), it now keeps the player the enemy before it aimed at, which saves swapping Zero in or out. That adds up when X and Zero fight side by side.
- **Zero's splash makes 8 bubbles instead of 24.** Diving into water starts a burst of bubbles, and each bubble checks the level map every frame. With both players diving in at once, the water in Toxic Seahorse's stage dropped to about 60% speed for a second or two. X's splash is unchanged.
- **157 more of the game's long calls run in FastROM**, found by this run's code coverage.

Speed in the moments these target, replaying the bot's inputs for each game update on both versions (so both play out the same; share of frames that run a full update):

| Moment (about 2 seconds) | 0.23 | 0.24 |
|---|---|---|
| Blast Hornet's stage, the lift shaft, both players on the lift with enemies around | 60% | 68% |
| The same shaft, a calmer moment | 82% | 86% |
| Toxic Seahorse's stage, both players diving into the water | 59% | 65% |
| Doppler stage 1 boss, its busiest stretch | 53% | 57% |
| Doppler stage 2 boss, its busiest stretch | 60% | 60% |

Average speed in random two-player play is the same as in 0.23: 98% over all 61 sections (four runs each; the sections differ by a point or two from run to run either way). The Doppler-stage boss fights are still the slowest spots: there, two players' worth of the game's own work is more than one SNES frame holds.

Single-player was compared with the original game on all 61 sections, with the co-op difficulty changes switched off for the test. 48 play out the same update by update. The other 13 differ only in timing, because the game's code runs faster in FastROM: a boss intro that starts a few frames sooner, or the camera during the game-over screen. With FastROM switched off, 10 of those 13 are identical too, and the last 3 are Doppler-stage boss rooms where the original game itself slows down, so its frame timing differs there. Boss Rush and VS mode play as before.

## New in 0.23: a full playthrough, less slowdown, one freeze fixed

A bot played every stage, checkpoint and boss in co-op (and solo), then Boss Rush and every VS setup, while the frame time was profiled.

- **Less slowdown in co-op.** Two changes do most of it. Both were checked update by update against 0.22 on every stage and boss: the game plays out the same, it just needs fewer CPU cycles.
  - **The object loops are unrolled everywhere.** Each frame the game steps through 116 object slots, most of them empty. Since 0.19 VS mode used unrolled checks that only call the active objects. They now run in the stages too, which also helps single-player.
  - **Enemies no longer swap player 2 in and out one by one.** An enemy aims at whichever player is closer. When that's Zero, his position and hit fields are swapped in as "the player" for that enemy's update. Before, they were swapped back after every enemy. Now they stay in while the next enemy aims at him too, and are put back when one wants X or the list ends. With many enemies or boss parts around Zero, that removes most of the swaps.
  - **About 500 more of the game's long calls run in FastROM.** These are enemy code, mostly from the Doppler stages, that the single-player coverage run never reached.
- **Fixed a freeze in the Doppler stage 2 boss fight.** A Boss Rush value (which stage the final-chain boss's graphics come from, `$7EE513`) was never cleared at power-on. The game clears it on the first frame without a boss, so starting from the title was safe. A fight already on screen with leftover data there loaded the wrong stage's graphics, overflowed the game's graphics decompressor and hit its built-in hang. Power-on now clears `$7EE500-$7EE5FF` as well.

Speed in co-op (share of frames that run a full game update; random two-player play, two runs each, the game's own sound-loading pauses left out):

| Section | 0.22 | 0.23 |
|---|---|---|
| Doppler stage 4, start | 76% | 94% |
| Doppler stage 2 boss | 74% | 88% |
| Doppler stage 1 boss | 78% | 87% |
| Doppler stage 2, checkpoint 2 | 81% | 93% |
| Doppler stage 3, start | 89% | 97% |
| Stage 5 boss | 95% | 99% |
| The 12 slowest sections | 87% | 94% |
| All 61 sections tested | 96.6% | 98.3% |

Single-player still plays exactly like the original game (checked on every stage and boss with the co-op difficulty changes switched off for the test). Boss Rush and VS mode play as before.

## New in 0.22: you're Zero from the moment you beam in, and gold X hits Zero softer

- **X + ZERO, playing Zero: you beam in, wait and talk as Zero.** You used to arrive as gold X and turn into Zero only when the CPUs joined. That meant gold X stood there during the score message between rounds. You now turn into Zero as soon as you start beaming in, every round. The CPU X is built from your saved X data, so he looks and plays as before.
- **HARD gold X's damage against your Zero is halved**, against GOLD X and in X + ZERO. His damage against X (playing X in X + ZERO) is unchanged.

| HARD gold X's attack on Zero | Before | Now |
|---|---|---|
| Buster shot | 4 | 2 |
| Half charge | 6 | 3 |
| Full charge | 8 | 4 |
| Big blast | 10 | 5 |
| Z-Saber slash | 14 | 7 |
| Z-Saber wave | 8 | 4 |
| Touch | 4 | 2 |

EASY and NORMAL gold X already do the game's normal damage (1–4) and are unchanged, and so is the HARD CPU Zero. The values are in `VsHardDmgXZ` (`vsmode.asm`).

## New in 0.21: black X on HARD, Zero's side against gold X

- **X + ZERO on HARD: the CPU X wears black**, like the HARD CPU Zero, whichever side you play. On EASY and NORMAL he stays blue (you play X) or gold (you play Zero).
- **Against the CPU gold X, everything is on your side of the screen.** X now beams in on the right wall and waits there through the score message, and you (Zero) join on the left. There's no more swap after the round starts. Your health bar (the "Z") is on the left, and X's is on the right.
- **Fixed:** in X + ZERO when you play Zero, the CPU X could show washed-out, wrong colors (since 0.19). The code that tints Zero's charge glow also ran while player 1 was still X beaming in, and the CPU X copies his colors from player 1 at that moment.

## New in 0.20: Zero vs CPU X, fairer

- **Against the CPU gold X, you (Zero) now start on the left wall facing right, and X starts on the right wall.** (0.21 also moves the health bars and X's beam-in to match.)
- **Your Zero's hits on the CPU X ignore X's body armor.** The armor halved Zero's damage, and the gold armor often took another 1–2 points off, with a minimum of 1. That made the Z-Saber hit for 1–2 and a full charge for 1. Now the CPU X takes Zero's normal damage. This applies against GOLD X and to the CPU X in X + ZERO when you play Zero:

| Your Zero's attack | Before | Now |
|---|---|---|
| Buster shot | 1 | 1 |
| Half charge | 1 | 2 |
| Full charge | 1 | 3 |
| Z-Saber slash | 1–2 | 4 |

The CPU's damage to you, and your X's damage to the CPUs, are unchanged.

## New in 0.19: 1 vs 2, X and Zero against you at once

**1P VS CPU** has a third opponent: **X + ZERO**. Next you pick who you play, **X** or **ZERO**, and then the CPUs' level.

- **You play X** (gold armor, controller 1) against a CPU Zero and a CPU X. The CPU X is drawn in X's usual blue, so you can tell him from yourself.
- **You play Zero** (controller 1) against a CPU X in the gold armor and a CPU Zero in black.
- **The CPUs are a team.** Their shots and their touch never hurt each other, only you.
- **Each CPU has 16 health; you have 32.** Both CPUs use the same AI and levels as the 1-on-1 CPU, including HARD's rushing, wall-kicks, touch damage and HARD damage values.
- **A beaten CPU bursts and is out for the round,** and the other keeps fighting. Beat both to win the round. You lose the round if you go down. Best of 3, as before.
- **Health bars:** yours on the left (with a "Z" when you play Zero), and one bar per CPU on the right, with an X or Z icon.
- A new talk before round 1 for each side.

The CPU X is drawn without separate armor pieces, but he has the gold armor's moves: the big blast, the Z-Saber, the extra charge levels, and its slow health refill (up to his 16).

Three fighters are a lot for the SNES CPU, so this version also speeds up VS mode (the other VS modes run at full speed as before):

| 1 vs 2 | EASY | NORMAL | HARD |
|---|---|---|---|
| You play X | 100% | 96% | 89% |
| You play Zero | 100% | 98% | 91% |

Speed is the share of frames that run a full game update, averaged over four test matches each. The dips come in busy moments (both CPUs charging and wall-kicking at once) and show up as brief slowdown, as in the stock game.

Tested against a scripted player (it charges, fires and jumps over shots; four matches per row and level):

| Scripted player | EASY | NORMAL | HARD |
|---|---|---|---|
| Plays X | won all 4 | won all 4 (one went to round 3) | lost all 4, rounds of about 25 seconds |
| Plays Zero | won all 4 | lost all 4 | lost all 4, rounds of about 10–15 seconds |

The scripted player was written for X and uses Zero's moves poorly, so a person playing Zero should do better than these numbers.

## New in 0.18: HARD gold X hits harder too

HARD gold X now does the same damage as HARD Zero for the attacks they share, and scaled-up damage for his own two (the arm part's big blast and the saber's wave). Damage to Zero (32 health):

| HARD gold X's attack | Normal | HARD |
|---|---|---|
| Buster shot | 1 | 4 |
| Half charge (also the big blast's second shot) | 2 | 6 |
| Full charge | 3 | 8 |
| Big blast (arm part) | 4 | 10 |
| Z-Saber slash | 4 | 14 |
| Z-Saber wave | 3 | 8 |
| Touch | 4 | 4 |

EASY and NORMAL gold X keep the normal damage. Against the scripted Zero players, HARD gold X's rounds now last about 9–15 seconds. The values are in `VsHardDmgX` (`vsmode.asm`).

## New in 0.17: fight a CPU gold armor X

**1P VS CPU** now asks who you want to fight: **ZERO** or **GOLD X**. Then you pick the CPU's level as before.

- **ZERO:** as before. You play X, and pick X's armor after the level.
- **GOLD X:** you play **Zero with controller 1**, and the game plays X in the gold armor. There's no armor menu; the match starts after the level.

The CPU X uses the same AI and levels as the CPU Zero:

- He charges and fires, uses the arm part's big blast and the gold armor's Z-Saber, dodges your charged shots, and jumps to shoot you out of the air.
- **HARD** X also switches between rushing and blasting from range, chases you up walls, and his touch hurts you (4 damage), like HARD Zero's.
- His shots do the game's normal damage. (0.18 gives HARD X his own boost.)

Tested against scripted Zero players (one match each against four of them):

| CPU gold X | Result |
|---|---|
| EASY | lost all 4 |
| NORMAL | won all 4 (two went to round 3) |
| HARD | won all 4, rounds of about 20 seconds |

The two-player modes and the CPU Zero levels play as before.

**How it works:** the player slots stay the same (X is player 1, Zero is player 2), but the controllers are swapped. Zero's update takes controller 1's buttons. For X, the AI runs right after the game has converted controller 1 into X's moves. It then converts its own buttons the same way, overwriting yours. That conversion finds new presses by comparing with last frame's buttons, so the AI's own last-frame buttons are put back first; otherwise X could never press fire while you held it.

## New in 0.16: HARD Zero's damage, set by hand

HARD Zero's attacks now do these fixed amounts to X (32 health):

| HARD Zero's attack | 0.15 | 0.16 | With X's body armor |
|---|---|---|---|
| Buster shot | 1 | 4 | 2 |
| Half charge | 4 | 6 | 3 |
| Full charge (also the combo's shots) | 6 | 8 | 4 |
| Z-Saber slash | 12 | 14 | 7 |
| Touch | 2 | 4 | 2 |

Without armor, X goes down to 4 full charges, 3 saber slashes, or 8 touches or buster shots. EASY, NORMAL and 1P VS 2P keep the original damage. Against the scripted X players, HARD's rounds now last about 12–18 seconds. The values are in `VsHardDmg` (`vsmode.asm`) and `!VsTouchDmg` (`coop.asm`).

## New in 0.15: HARD Zero hits harder

The HARD CPU Zero's charged shots do double damage and his Z-Saber slash does triple. Damage to X (32 health):

| HARD Zero's attack | Before | Now | With X's body armor |
|---|---|---|---|
| Half charge | 2 | 4 | 2 |
| Full charge (also the combo's shots) | 3 | 6 | 3 |
| Z-Saber slash | 4 | 12 | 6 |
| Buster shot | 1 | 1 | 1 |
| Touch | 2 | 2 | 1 |

EASY, NORMAL and 1P VS 2P keep the old damage. Against the scripted X players, HARD's rounds now last about 22 seconds, down from about 35.

## New in 0.14: HARD Zero mixes rushing and blasting

HARD Zero now switches between two plans, so you can't settle into one way of fighting him:

- **Rush:** 0.13's behavior. He gets on top of you, his touch hurts, he jumps into you when you jump, and he follows you up walls.
- **Blast:** he keeps his distance. He backs off (often with a back-dash) when you come within about 96 px and closes in only when more than about 160 px away. Meanwhile he charges full shots, the double shot and the combo, dodges your charged shots, and jumps to shoot you out of the air. When you corner him, he kicks off the wall over you to get his distance back.

**When he switches:**
- Each plan lasts a random 1.5 to 3.6 seconds. Then, 3 times in 4, he switches to the other one; otherwise he keeps it a while longer.
- **Hit and run:** after his touch hurts you, he backs off into blast half the time.
- When you hit him, he switches a third of the time.
- Each round starts with a random plan.
- The dice for these choices are stirred by your controller input every frame, so the pattern can't be learned. EASY and NORMAL still use their own unchanged dice.

**Tested** against the same scripted X players, 3 matches each: HARD won all 12 without losing a round. Rounds took about 35 seconds, versus 23 for 0.13's pure rush, because he spends more than half his time at range. He switched plans 19-29 times per match. In those matches he did most of his damage while rushing (40-53 per match, versus 15-24 while blasting), so the blast spells are where you can catch your breath and trade shots.

## New in 0.13: HARD Zero rushes you, and his touch hurts

**Touch damage (HARD only).** The HARD CPU Zero's body now hurts X on contact, like an enemy's: 2 damage (1 with the body armor), with the usual flinch, knockback and blink. Until now, touching did nothing in VS mode. Only shots and the saber hurt, and that's still true for EASY, NORMAL and 1P VS 2P.

**Rushing.** HARD now plays all-out offense:

- He always heads straight for you. He re-decides every few frames and dashes in whenever he isn't on top of you. Close up, he runs or dashes right through you, turns, and comes back.
- He dash-jumps only from far away, so up close he stays on the ground with you.
- When you jump near him, he jumps into you.
- **He chases you up walls.** When you're on a wall (sliding or kicking), he runs to that wall and wall-kicks up after you until he's level with you, close enough to touch. He lets go once you leave the wall or he's above you.
- He keeps charging and firing as before: full charges, the combo and the saber. Being on top of you means they land more often.
- No more backing off, escaping corners, or climbing walls on his own (0.12's wall play). Rushing replaces them.

**Tested** against the same scripted X players, 3 matches each: HARD won all 12 matches without losing a round, about 23 seconds a round. X took about 15 hits a round, Zero 0–4. The scripted players handle a rusher badly: they don't turn and shoot point-blank, which is the obvious counter. In a separate test, X kept climbing the left wall and was touched 9 times in 15 seconds. The touch damage is `!VsTouchDmg` in `coop.asm`.

## New in 0.12: HARD Zero wall-kicks and wears black

**Black armor.** The HARD CPU Zero wears black armor: his three reds become dark grays with a slight purple tint, and his outline is darker. His gold hair, white parts and blue gem stay as they are. His charge glow tints the black armor. EASY, NORMAL, 1P VS 2P and co-op Zero stay red.

**Wall play.** HARD now uses the arena's walls:

- **Cornered:** when you close in with Zero near a wall, he jumps at the wall and dash-kicks off it, over your head. He turns in the air and fires his charge when he lands behind you.
- **On his own:** every few seconds, when the wall behind him is close and he has a charge going, he wall-kicks up it (one to three kicks, up to the ceiling), then kicks off toward you and fires once level.
- His dodges are still plain jumps. Tested as wall dodges, they got him hit more often.

**Fixed: HARD sometimes stopped charging.** If the CPU pressed the buster at a moment when Zero couldn't shoot (in the middle of a wall kick, or while flinching), the press was lost. It then kept the button held, and holding never starts a charge, so Zero could go many seconds without firing (once 27 seconds in a test). HARD now lets go for a frame and presses again. This made HARD noticeably stronger. EASY and NORMAL play exactly as in 0.11.

**Tested** against the same scripted X players as in 0.11, 3 matches each (best of 3):

| Scripted X | HARD in 0.11 | HARD in 0.12 |
|---|---|---|
| Taps the buster, jumps 15% of Zero's shots | wins 3 of 3 | wins 3 of 3 (rounds 6-0) |
| Charges every shot, jumps 30% of Zero's shots | wins 2 of 3 | wins 3 of 3 (rounds 6-0) |
| Charges every shot, jumps 45% of Zero's shots | wins 3 of 3 | wins 3 of 3 (rounds 6-1) |
| Charges every shot, jumps 95% of Zero's shots | wins 3 of 3 | wins 3 of 3 (rounds 6-1) |

Across these 12 matches, 0.11's HARD lost 5 rounds; 0.12's lost 2. In 6 test matches, it kicked off a wall 22 times when cornered and climbed one 10 times on its own.

## New in 0.11: CPU levels and a talk before round 1

**Before round 1**, Zero and X each say a line in the game's dialog box, so the match doesn't start out of nowhere:

> (ZERO) Ready, X? Don't hold back!
>
> (MEGA MAN) I won't, Zero. Here I come!

Neither player can move until the box closes, about 8 seconds later. Rounds 2 and 3 still start right after the score line.

**CPU level.** Picking 1P VS CPU now opens one more menu before X's armor: **EASY**, **NORMAL** or **HARD**. The cursor starts on NORMAL.

| | EASY | NORMAL | HARD |
|---|---|---|---|
| Dodging your shots | Jumps after 12–27 frames, lets more than half through | Jumps after 2–9 frames, lets about 1 in 6 through | Jumps after 1–2 frames and almost never misses a charged shot. Lets half of your plain buster shots through (they only take 1) to keep charging |
| Charging | Half or full charges, with a pause after each one; never the combo | Mostly full charges, sometimes the double shot or the whole combo; up close it lets a half charge go | Goes for the whole combo about half the time; up close it waits for at least a full charge |
| Spacing | Keeps its distance, never dashes, can be cornered | Middle distance, dashes in now and then, jumps out of corners | Stays close, dashes in often, and turns dashes into dash jumps |
| Extras | | | When you jump while it holds a charge, it jumps to meet you and fires once level. Dash-jumps in, also for the Z-Saber after the combo's two shots |

NORMAL is the 0.10 CPU, unchanged.

**Tested** against scripted X players (X's armor off, best of 3):

| Scripted X | EASY | NORMAL | HARD |
|---|---|---|---|
| Taps the buster, jumps 15% of Zero's shots | loses 3 of 3 (two went to round 3) | wins 2 of 2 | wins 5 of 5 |
| Charges every shot, jumps 30% of Zero's shots | loses 3 of 3 | loses 2 of 2 | wins 4 of 5 |
| Charges every shot, jumps 45% of Zero's shots | loses 2 of 2 | wins 2 of 2 | wins 4 of 4 |
| Charges every shot, jumps 95% of Zero's shots | loses 2 of 2 | wins 1 of 2 | wins 4 of 4 |

## New in 0.10: VS mode (X against Zero)

A new title item, **VS MODE**, sits under BOSS RUSH. It opens two more menus:

1. **1P VS 2P** (controller 2 plays Zero) or **1P VS CPU** (the game plays Zero).
2. X's armor: **NO ARMOR**, **ARMOR** or **GOLD ARMOR**, the same three as Boss Rush.

The match:

- **Arena:** one of the boss rooms of the Maverick-rematch stage in Doppler's fortress. It has a flat floor and walls on both sides, and fits on one screen. Its boss is removed, and there are no other enemies.
- **Best of 3 rounds.** X starts at the left wall, and Zero joins on his own at the right wall. Both have **32 health** and refill each round.
- **X has the buster only.** Its charge shots work as usual, and so do the arm part's two big blasts and the gold armor's Z-Saber. X's armor works as in the game: the body part halves the damage he takes, and the gold armor's chips refill his health while he stands still.
- **Zero** has his buster, his charged shots, and the full-charge combo. Release the full charge for one big shot, press again for the second, then press again for the Z-Saber.
- **Hits** use the game's own player-hit routine, so the player who's hit flinches, gets knocked back and blinks for a moment, the same as with an enemy. Damage:

| Attack | Damage |
|---|---|
| Buster shot | 1 |
| Half charge | 2 |
| Full charge | 3 |
| X's arm-part big blast | 4 |
| Z-Saber slash | 4 |
| Z-Saber wave (X, gold armor) | 3 |

- **End of a round:** the loser explodes and the room reloads. Then the winner's line shows in the game's dialog box with the score, for example "(ZERO) Round 1 is mine! X 0 - 1 ZERO", and the next round starts.
- **End of the match:** the winner gets a final line ("MEGA MAN WINS!" or "ZERO WINS!"), then the game goes back to the title.
- In VS mode Zero can't leave with Select. Lives never run out. The damage doubling from co-op play doesn't apply.

**The CPU Zero:**

- **Spacing:** it keeps a middle distance, closes in when far (sometimes dashing), backs off when crowded, and jumps toward you when cornered.
- **Dodging:** it jumps over your shots after a short reaction delay, but not every time.
- **Charging:** it charges its buster and fires when level with you. Usually it's a full charged shot, sometimes the double shot, and sometimes the whole combo, after which it dashes in for the saber.
- **Rapid fire:** now and then it switches to rapid buster shots.
- **Difficulty:** tested against scripted players, it beats one that just mashes the buster every time. Against one that charges its shots and jumps most of Zero's shots, it wins about a third of the matches. (This CPU is the NORMAL level in 0.11.)

## Fixed in 0.10: Zero's Z-Saber while X shoots (co-op too)

The Z-Saber's object takes its animation from a value (`$1F44`) that the player code sets whenever a player strikes a shooting pose. Both players shared it. If X fired while Zero was slashing, the saber switched to an animation that doesn't exist. Uploading that garbage stalled the game's vblank routine and froze the game. Each player now has his own copy of the value. In co-op this needed X and Zero attacking at the same moment, so it was rare, but VS mode hit it often.

## New in 0.9.5: no double-charge spheres in co-op

With Zero in the game, X's double charge with the arm part is now just the two big blasts:

- **Removed in co-op:** the three spheres that spiral out with the first shot and the four that orbit the second shot. They're no longer spawned at all; before, they existed but weren't drawn.
- **One invisible helper stays.** In the game's own logic, one sphere stores the second shot and launches it on your next press. It's never drawn and only sits at X's buster.
- **Less damage, fewer slots:** the attack does a little less damage than before, since the spheres no longer hit anything. It also takes 3 shot slots instead of up to 9, so Zero's shots and X's blasts compete less.
- **Kept:** the gold-armor Z-Saber slash and its wave still follow the two blasts.
- **Solo is unchanged:** playing alone, the spheres are still there, as in 0.9.4.

## New in 0.9.4: the first full-charge shot is the big blast

- **First shot = second shot.** With the arm part, releasing a full charge used to fire only a cluster of four small spheres, and the big blast came on the next press. Now the release fires the same big blast as the second shot, with the spheres spiralling out beside it. The next press fires the second big blast as before. In co-op the spheres aren't drawn (see 0.9.3), so the first shot had been almost invisible there. Now it's the full blast.
- **More damage:** the first shot hits harder than before, since it now carries the big blast as well as the spheres.
- **Shot slots:** with two big blasts plus spheres on screen, the nine shot slots can run out. When the second press can't find a slot, it reuses one from a first-shot sphere that's still flying, so the second blast always comes out, in solo too. X's shot counters return to normal afterward, as in the original.
- Unchanged: the full charge without the arm part, the gold-armor Z-Saber slash, and Zero's own charged shots.

## Fixed in 0.9.4: Zero couldn't charge after joining during X's full charge

Zero starts as a copy of X's player data, with X's charge cleared. That copy also carried the "follow-up stored" flags X's full charge sets: the pending second shot, and the saber with the gold armor. When Zero joined while X was holding a full charge (the green aura), he started out thinking he had a stored follow-up shot, so his buster wouldn't charge. Those flags are now cleared on joining, so Zero starts exactly as if X were standing still.

## Fixed in 0.9.3: X's double charge no longer garbles Zero

With the arm part, X's full double charge garbled the blast or Zero. That charge does more than fire two big shots: it adds four small spheres that circle X and a swirl that forms around him at the second press. Both are drawn with sprite memory the game normally keeps for X's special weapons. In co-op that memory holds Zero's body and his shots, so the extras wrote over Zero and showed up as scrambled tiles. Sprite memory is full in every stage, so there's no free room to move them to, and changing colors can't help because the shapes themselves were being overwritten.

What changed, in co-op only (playing alone is exactly as before):

- **Kept:** both big blasts, and the Z-Saber slash and its wave with the gold armor.
- **Hidden:** the circling spheres and the swirl. They're no longer drawn or loaded, so Zero's graphics stay intact. They still exist and still hit, so the attack does the same damage.
- **Second blast fixed:** with Zero shooting at the same time, the second big blast could fail to appear because all nine shot slots were taken. When that happens it now takes one of the hidden spheres' slots.

## Fixed in 0.9.2: both players on one moving platform

Zero could get knocked off a moving platform when X was on it too. Two causes:

- **Mixed-up players:** for each object's update, the patch hands the object whichever player is nearer, so enemies aim at the closer one. That swap moves only the values enemies read, such as position. A platform then checked a player against that player's position but the other player's previous position and jump state. It missed the landing, pushed the player off sideways, and lost track of who was standing on it. Platforms now see each player whole.
- **Sinking:** Zero moves before the platform does each frame, while X moves after it. When a platform turned from going down to going up, Zero met it already a few pixels deep. The game pushes a player back up only 2–3 pixels a frame, so he sank further each frame until he was pushed off sideways. He's now pushed out fully.

In a test on the flying platforms in Neon Tiger's stage, a bot had both players standing, walking and jumping on one platform for 1,500 frames per run. On 0.9.1, Zero fell off in almost every run; now he stays on. The only falls left were jumps that missed the platform's edge. Speed is unchanged.

## New in 0.9.1: NORMAL / HARD for Boss Rush

After you pick **NO ARMOR** or **ARMOR**, a third menu asks **NORMAL** or **HARD**:

| Choice | Maverick stages |
|---|---|
| **NORMAL** | 2 stages of 4 Mavericks: Beetle → Hornet → Seahorse → Crawfish in Beetle's stage, then Tiger → Buffalo → Rhino → Catfish in Tiger's stage |
| **HARD** | 1 stage with all 8, in Tiger's stage: Tiger → Hornet → Buffalo → Beetle → Seahorse → Catfish → Crawfish → Rhino |

- **GOLD ARMOR** skips this menu and is always all 8 in one stage, as before.
- The NO ARMOR option of 2 Mavericks per stage is gone.
- Either way, the final chain in Sigma's room (Bit, Byte, Vile, Dr. Doppler, Sigma) follows the Mavericks.

## New in 0.9: the final chain

After the eight Mavericks, Boss Rush no longer ends at the stage select. It takes you to **Sigma's stage, straight into Sigma's room**, for one last chain:

**Bit → Byte → Vile → Dr. Doppler → Sigma**

- Each one appears after the last one explodes, like the Maverick chains. No health refill between them. (Since 0.25.1 the players are moved to the left first, see 0.25.1.)
- **Vile** fights in both forms: first in his Goliath Ride Armor, then on foot.
- **Bit and Byte** appear right away. In the normal game they only show up after a certain number of Mavericks are beaten.
- **Dr. Doppler** can soak up shots to heal, as in the original. If the buster isn't getting through, switch weapons.
- **Sigma comes last**, with his usual speech. From there the game runs as normal: his next form, then the ending.
- Since 0.26 Bit, Byte, Vile and Dr. Doppler start fighting without their talks (see 0.26).
- **Losing a life or getting a game over** puts you back in Sigma's room, and the chain starts again from Bit.
- **How it works:** Sigma's stage has no checkpoint inside his room, so the patch adds one. Each boss's graphics load from its own stage: Bit and Byte from the Maverick stages, Vile from his own stage, Doppler from his. That's the same in-game loader the Maverick chains use. Bit and Byte skip their stage checks; since 0.25 the start values those checks set (`$02:E15C`: sprite set, boss-bar id) are set by the chain. When the chain starts, the elevator X normally rides up into the room is set to "already arrived". That closes the hole in the floor. Left alone, it would clear the room the moment X stepped on it.
- **Tested:** a bot played the armor rush from the title with Zero joined: both Maverick stages, then Bit, Byte, both Vile forms, Doppler and Sigma, through to Sigma's next form. The bot can't win against Doppler's healing, so his health was lowered in that test. It also couldn't beat Sigma's last form, so the ending wasn't reached by the bot. A life lost during Byte sent it back to Bit.

## New in 0.8.1

- **No more health refill between Mavericks in a chain.** Whatever health you have left when one falls is what you start the next one with. Each new stage still starts with full health.
- **Fixed: Blizzard Buffalo floated above the floor in Neon Tiger's room.** He doesn't fall when he enters. He slides in at a fixed height that matches the floor of his own room, and Tiger's floor is 16 pixels lower. He now enters at the floor height of whichever room he's in.

## New in 0.8: Boss Rush chains

Boss Rush now puts several Mavericks in one stage, **one at a time**: when one falls, it explodes, and the next one drops into the same room a couple of seconds later. Your armor choice decides how long the chains are:

| Choice | Stages | Mavericks per stage |
|---|---|---|
| **NO ARMOR** | 4 | 2 |
| **ARMOR** | 2 | 4 |
| **GOLD ARMOR** | 1 | all 8 |

- The order:
  - **NO ARMOR:** Hornet → Beetle, Seahorse → Crawfish, Rhino → Catfish, then Tiger → Buffalo.
  - **ARMOR:** Beetle → Hornet → Seahorse → Crawfish in Beetle's stage, then Tiger → Buffalo → Rhino → Catfish in Tiger's stage.
  - **GOLD ARMOR:** Tiger → Hornet → Buffalo → Beetle → Seahorse → Catfish → Crawfish → Rhino, all in Tiger's stage.
- **No health refill between Mavericks** (since 0.8.1): the health you have left carries into the next fight. Each new stage still starts at full health.
- Each Maverick has its normal health, damage and weakness, and its usual entrance.
- **Weapons:** the last Maverick in a stage gives its weapon on the usual weapon-get screen. The other weapons from that stage are added right after, so you have all of them for the next stage.
- **Losing a life or getting a game over** restarts that stage's chain from its first Maverick.
- **No slowdown:** only one Maverick is on screen at a time. The next one's graphics load the same way the game normally loads them, after the last one is gone.
- The mixed-pair test from 0.7 is gone, and so are the twin Mavericks in Boss Rush. The Double Boss build still has twins in the normal game.
- **Which rooms work:** every Maverick was tested in every other Maverick's boss room (56 combinations). A few got stuck and could never finish, so the groups avoid them:
  - Crawfish in Hornet's, Buffalo's or Catfish's room
  - Hornet in Buffalo's room
  - Seahorse in Buffalo's or Catfish's room
- **Tested:** a bot played all three choices start to finish, including GOLD ARMOR with two players. It cleared every chain and the rush ended at the stage select. Losing a life in the middle of a chain started it again from the first Maverick.

## New in 0.6.1

- **GOLD ARMOR now includes X's Z-Saber** (the beam saber Zero hands X in the original game). Charge fully: the first release fires the big charged shot, and the next presses fire the second shot and then a saber slash with its wave.
- **Fixed: Blast Hornet could fly off through the wall and never come back,** which made the first boss impossible to finish. Each Hornet picks a spot to fly to, and the game keeps that spot in one shared place. With two Hornets, one could re-aim the other in mid-flight; the re-aimed one then never arrived and kept flying. Each twin now keeps its own flight target, the same way 0.5.9 gave them their own damage settings. In a 20,000-frame test neither Hornet stayed off screen for more than about a second at a time. All the other twin pairs were checked the same way.

## New in 0.6: armor choice for Boss Rush

Picking **BOSS RUSH** on the title menu now opens a second menu: **NO ARMOR**, **ARMOR** or **GOLD ARMOR**. Move with Up/Down and confirm with Start.

- **NO ARMOR:** plain X.
- **ARMOR:** all four armor parts (helmet, body, arms, legs), as in 0.5.8.
- **GOLD ARMOR:** the four parts plus all four enhancement chips, which the game shows as the gold armor, plus X's Z-Saber (since 0.6.1). It includes the chips' effects: health refills while standing still, less damage taken, a faster charge and more air dashes.
- **Always:** all eight heart tanks and full health for every fight.
- The choice holds for the whole rush, including after a game over. While the gold armor is on, the chip effects also help Zero.

## Fixed in 0.5.9 (found in a full Boss Rush test run)

- **A twin could become immune to the buster for the rest of the fight.** The Mavericks keep a few values of their own in shared memory. One is the damage setting they go back to after their brief flash of invincibility when hit. Tunnel Rhino, for one, switches that setting to "buster-proof" during his angry phase. With two Rhinos, the second one picked up the first one's setting. If the first then died mid-phase, the survivor stayed immune for good, and the fight couldn't be won with the buster. Each twin now keeps its own copy of these values.
- Tested with a bot run through the whole Boss Rush in co-op, with real damage. All eight double fights were won, and the rush ended at the stage select as intended.

## New in 0.5.8

- **Boss Rush uses the original game's damage.** The bosses have their normal health, and enemies and bosses do normal damage to both players. The "50% more boss health" and "double damage" settings now apply only to a normal game.
- **X starts Boss Rush fully powered up:** all four armor parts (helmet, body, arms, legs) and all eight heart tanks, for a full-length health bar. Zero is unchanged.

## New in 0.5.7: Boss Rush

The title menu has a new item under GAME START: **BOSS RUSH**.

- **All eight Mavericks, two at a time.** Boss Rush starts a fresh game, skips the intro stage and the stage select, and takes you through the eight Maverick stages in order: Blast Hornet, Blizzard Buffalo, Gravity Beetle, Toxic Seahorse, Volt Catfish, Crush Crawfish, Tunnel Rhino, Neon Tiger. Every fight is a double boss fight (see 0.5.6 below).
- **Each stage starts at its last checkpoint**, a short walk from the boss door.
- **Full health for every fight.** After each win the weapon-get screen plays, so you collect the weapons as you go. The next stage then starts with both players at full health. Player 2 rejoins with Start after the stage loads, as after any victory.
- **Losing:** a lost life restarts at the same checkpoint. A game over sends you back into the boss you haven't beaten yet.
- **After the eighth boss** the rush ends at the normal stage select. You keep all eight weapons and can carry on into the Doppler stages as a normal game, with single bosses.
- The story scenes the game plays after certain bosses still play between fights.
- **GAME START is the normal game, with single bosses.** The separate Double Boss patch from 0.5.6 is gone: double bosses now come with Boss Rush. To get them in every Maverick fight of a normal game too, build with `-DDoubleBoss=1` (see Source).

## New in 0.5.6: Double Boss

Two of the same Maverick at once. Since 0.5.7 this is what Boss Rush plays (0.5.6 shipped it as a separate patch for the whole game).

- **The twin** appears beside the Maverick as the fight starts and runs the Maverick's own moves and attacks. Each one picks its own target, so in co-op they can split up and each go after a different player.
- **Two health bars.** The twin's bar sits just left of the boss bar. Both use the "50% more boss health" scaling, each keeping its own remainder.
- **The fight is won when both fall.** The first one to go down explodes and blinks for about a second and a half, then disappears. Its bar goes away, and the boss bar follows the one still fighting. The usual victory sequence, weapon get and stage clear play when the second one falls.
- **Covers all eight Mavericks**, in their own stages and in the Doppler-stage rematches. Dying and retrying works as usual; the twin comes back with the boss. Other bosses (mid-bosses, Vile, the Doppler-stage bosses, Dr. Doppler, Sigma) are single as before.
- **It's slower.** Two Mavericks are a lot of work for the SNES CPU. In co-op boss fights the game ran at about 77% speed on average in testing, against about 93% with one Maverick, and Toxic Seahorse and Tunnel Rhino dip to around 55–60%. Single-player fights stay close to normal: about 92% against 95%. An emulator CPU overclock helps if yours has one.
- **The twins share colors.** Color effects such as a Maverick's charge flash or hit flash change the shared palette, so the other twin flashes too.

## New in 0.5.5

- **Auto-charge, for each player.** Press **X** on your controller to turn it on (weapon-switch sound) or off (menu sound). While it's on, your buster charges by itself. Press shoot to fire: a charged shot if the charge has built up, or a normal shot if it hasn't. Then it starts charging again.
  - The double-charge follow-ups work as in the original. Zero's second shot and Z-Saber, X's second shot with the arm upgrade, and X's saber come out on your next presses. Auto-charge picks up again once they've been used.
  - The setting stays on through stage changes and deaths. It resets at power-on. It does nothing while X is in a Ride Armor. If you've assigned an action to the X button in the game's options, X keeps that action and auto-charge stays off.
  - Set `!AutoChg = 0` in `coop.asm` to build without it.
- Fixed: if X had charge sparkles on screen when Zero joined, Zero started with X's sparkle count. That count could keep Zero's Z-Saber from ever coming out.

## Faster in 0.5.4

With both players on screen the game now does about 10–12% less work per frame in busy scenes, so there's less slowdown. Measured over the same stretches of random two-player play: a busy Doppler stage went from 65% to 79% speed, Blast Hornet's fight from 89% to 93%, and the overall average from 89.5% to 93%. Single-player is unchanged.

- **More of the game runs in FastROM.** The FastROM conversion only covered code seen running in single-player. Zero's moves and the terrain checks for player 2 still called the slow ROM mirror hundreds of times a frame. 161 more call sites now use the fast mirror.
- **Zero no longer carries X's armor parts.** Every frame, player 2's data was swapped in and out, including X's helmet, arm and leg part objects. Zero never uses them, so they're left out, and Zero is drawn through the cheaper single-object path.
- **The swap itself is cheaper.** Player data is now reached through a page-aligned direct page, which saves a CPU cycle on every access.
- **Player 2's health bar is rebuilt only when it changes** (health, max health or position), not every frame.
- **Smaller per-frame checks are unrolled.** These are the shot-slot bookkeeping and stage 5's "is anyone using palette 7" scan.

## Fixed in 0.5.3

- **Zero's full-charge Z-Saber works.** At full charge Zero fires two large shots, and the next press swings the Z-Saber. In co-op the swing showed but the blade never appeared or did damage. The blade checks every frame that its owner is still slashing, and it was reading player 1's state, so it vanished at once. Zero's shots now see his own state while they update.
- **The saber no longer gets used up early.** The game holds the slash until the sparkles from the two shots are gone. Each sparkle counts itself on its owner, and Zero's were counted on X. Zero's count stayed at zero, so a quick press during the second shot used up the stored slash without swinging. Zero's sparkles now count on Zero.

## Fixed in 0.5.2

- **Zero's charged shots now hurt bosses the way they do in the original.** With the "50% more boss health" option, a boss takes 2/3 of each hit's damage, carried over in thirds. A 1-damage hit, such as Zero's charged shot against most bosses, could round down to nothing and still make the boss flash and turn briefly invincible, so the second shot that follows hit an invincible boss. The whole combo did nothing. Now a boss's first hit always counts, and a hit that rounds down to nothing doesn't make the boss invincible, so the next attack lands. Bosses still take about 1.5 times as many hits overall.
- **Zero keeps his red colors when you resume an older save state.** The game copies its vblank code into RAM at power-on, so a save state made with an older version still had the old palette upload, which never sent Zero's palette to the screen. Zero showed in X's blue. The patch now corrects that copy when it finds the old one.
- **Level graphics: more headroom for the background.** Player 2's sprite uploads now go after the level's own uploads in each frame's queue. If the queue is still very large, player 2's upload for that frame is cut to a minimum and resent on the next frame. This keeps more of vblank free for the background's new columns, which are sent last. The first-stage glitch has not been reproduced yet, so this is a precaution, not a confirmed fix (see Known issues).

## Fixed in 0.5.1

- **Zero's charge sparkles now show.** Charge effects (and the other small effects tied to a player) are separate objects that the game updates after both players, with player 1's data in place, so Zero's never animated or appeared. Player 2's effects now get their own object slots and are updated together with player 2.
- **Zero no longer jumps onto X while charging.** The "stuck in scenery" check counted holding the fire button without moving as being stuck, and warped Zero to X after 1.5 seconds. It now only counts a held direction, for 4 seconds.
- **X no longer flashes in Zero's colors** during Zero's charged shot and saber slash. Zero's flash at that moment went into X's palette.
- **Zero's second charged shot:** after a fully charged shot, press shoot again for the second shot, as in the original game.

## New in 0.5

- **Player 2 can leave with Select.** Pressing Select on controller 2 makes Zero disappear, with no life lost. Press Start on controller 2 to join again. (Select used to warp Zero back to X. Zero is still warped back automatically when he gets stuck or falls far behind.)
- **Enemies and bosses do double damage** to both players (not in Boss Rush). This covers contact damage and enemy shots. Spikes, pits and lava were already instant kills and are unchanged.
- **Bosses have 50% more health** (not in Boss Rush). Bosses take 2/3 of the damage they normally would, so they need about 1.5 times as many hits. The health bar still shows the usual 32 units; it just drains more slowly. This applies to every boss: the Mavericks, the Doppler-stage bosses, the rematches, Dr. Doppler and Sigma.
- These three are on by default. To turn one off, set `!SelLeave`, `!DoubleDmg` or `!BossHP150` to 0 at the top of `coop.asm` and rebuild. The difficulty changes apply in single-player too.

## Changes in 0.4.4

- **X is limited to the X-Buster while Zero is in the game.** Special weapons load their graphics into the same sprite video memory that Zero is drawn from, and the SNES has no free sprite memory left to move Zero to. Before, a special weapon and Zero could each show pieces of the other's graphics. Now, if X has a special weapon selected when Zero joins, he switches back to the buster (the game's own L+R reset), and L/R do nothing for X until Zero leaves. X keeps all his weapons and their energy.
- **Zero no longer drops out at every boss door.** 0.4.3 dropped player 2 when player 1 walked through a boss door, because the door walk uses the same player state as the Doppler-stage teleporters. Zero now stays in through doors, and only drops for the teleporters.
- **Fixed striped backgrounds in boss rooms.** During the boss-door scroll the camera followed the midpoint between the players, and the game's scripted scroll then skipped loading some background columns, which left black vertical stripes in the boss room. The camera now follows player 1 alone during the door walk and scroll, as the original does.
- **Zero glows in his own colors while charging.** He used to flash in X's blue. His glow is now gold at the first charge level, then orange, green and pink at the higher levels, matching X's level colors without the blue.
- **Zero keeps his red colors in stage 5.** That stage uses every sprite palette, so 0.4.3 drew Zero with X's palette. Zero now borrows palette 7 whenever none of the stage's objects is using it, gives it back with its original colors when one appears, and falls back to X's colors only for that time.
- **Player 2's health bar has a "Z" icon** instead of X's icon. It also no longer turns into an "R" when X rides a Ride Armor.
- **Co-op state starts clean in every stage.** The stage-select and stage-loading screens reuse the part of RAM where the patch keeps its data, so leftovers could carry into the next stage. The patch now marks its RAM and clears it whenever the mark is gone.
- **Doppler stages: X's charge sparkle and hit flash are not shown while Zero is in.** In those stages the game draws these two effects from Zero's sprite memory. The charge itself and the shots work normally.

## Fixed in 0.4.3 (found by an automated playthrough)

- **The camera could lock onto a room with player 1 left outside it.** Camera sections (boss rooms, scroll stops) are chosen by small trigger objects that were treating whichever player was nearer as "the player". If Zero ran ahead into the intro boss room, the room locked with X still outside, and the game softlocked. Camera sections now follow player 1 only, as in the original. This also made the game draw the wrong section's tiles at times, which is a likely cause of the glitchy level graphics reported earlier.
- **A closing room edge now pushes both players back into view**, as the game does for one player. Before, it could leave player 1 off-screen beside a boss arena.
- **Player 1 could slowly lose the ability to shoot.** If Zero died while his shots were still flying, those shot slots stayed marked as his. X's later shots in those slots were then taken off Zero's count instead of X's, until X's count was stuck at the limit.
- **Zero no longer starts with X's shot count when joining.** If X had shots on screen when Zero joined, Zero began with those counted against him.
- **Shot ownership is tracked per shot.** Special weapons that split into extra shots could spawn into a slot one of Zero's shots had just left, and the new shot was counted as Zero's.
- **Zero no longer gets X's special weapons.** Joining copied X's selected weapon, and L/R could switch it, so Zero fired X's weapons using X's weapon energy. Zero now always has the buster, and L/R do nothing on controller 2.
- **Doppler-stage teleporters:** Zero drops out when X teleports, then rejoins with Start in the new room. Before, the players' data could end up exchanged after the teleport.
- Player 2 can no longer join while player 1 is dying, beaming in, or on player 1's first frame in a new state.

## Fixed in 0.4.2

- **Player 2 can pick up health capsules and 1-ups.** Pickups live in the game's effects list, which only ever checked player 1. Heart tanks, sub tanks and armor capsules are still player 1 only, because they run small X-specific cutscenes.
- **Charging no longer breaks after both players fire charged shots.** Player 2's charged shots were counted against player 1's "charged shots on screen" counter. It went negative and then blocked every new charge. Each player now has their own counter.
- **Fewer dropped level graphics.** Player 2's animation uploads could push the per-frame video upload past the end of vertical blanking. Anything that misses vblank is dropped, which showed up as glitchy level tiles. Player 2's upload now waits a frame when the budget is full.
- **Less slowdown.** The game's own code now runs in FastROM: about 1,500 long calls, found by recording code coverage across every stage, checkpoint and boss, point at the fast ROM mirror. The co-op palette work is also skipped when nobody is charging. Busy co-op boss fights went from 68–100% to 73–100% speed. Blast Hornet is still the slowest.
- **Player 2 can stand on and ride floating platforms**, lifts and other solid objects. Push-out, standing and carrying now run for both players.

## Fixed in 0.4.1

- **Neither player could shoot after a real power-on.** The patch's RAM was never cleared at boot. The leftover garbage made every shot look like player 2's and jammed the shot counter at 3. The patch now clears its RAM on power-on and reset. (Testing had only used save states, where that RAM was already clean.)
- **Zero looked like a jumbled blob when he first joined**, until he moved. His frame table pointer was read from the wrong ROM bank.
- Player 2 can no longer join while "READY" is on screen. Zero's graphics would overwrite the READY letters.

## New in 0.4

- **Player 2 is Zero**, with his own sprite, colors, Z-Buster and charge shots, and Zero's 28-point health bar. (Set `!P2Zero = 0` in `coop.asm` to get a second X instead.)
- **Boss fights work in co-op.** All eight Mavericks were beaten with both players in the room, and each ended in the normal stage clear and weapon get.
- During a boss fight, player 2's bar moves to the left beside player 1's, so the boss bar keeps the right edge.
- The camera stays inside a locked boss room. Before this fix, a midpoint camera could pull the scroll past the room and X fell through the floor.
- When the boss is beaten, player 2 leaves before the victory teleport. That teleport turns off terrain collision for the whole game, so player 2 has to be gone before it runs.

## Applying

1. You need your own **Mega Man X3 (USA)** ROM, unheadered, 2 MB.
   - CRC32 `0xFA0FE671`
   - SHA-1 `b226f7ec59283b05c1e276e2f433893f45027cac`
2. Apply `MMX3_Coop_v0.28.bps` with Flips, or with an online BPS patcher such as Rom Patcher JS.
3. Play it in an emulator that supports the Cx4 chip (snes9x, bsnes, Mesen) with two controllers.

## Controls

| Action | How |
|---|---|
| Player 2 joins | Press **Start on controller 2** during a stage. Player 2 appears next to player 1. |
| Player 2 controls | The same buttons as player 1, using player 1's button config. |
| Player 2 leaves | **Select on controller 2**. No life is lost; Start joins again. |
| Computer Zero | **Start, then L** on controller 1 (the pause menu) calls him, and the same again sends him away. Anything on controller 2 takes him over. Not in VS mode or Boss Rush as Zero. |
| Auto-charge on/off | **X** on either controller, for that player. |
| Boss Rush | **BOSS RUSH** on the title menu, then X or ZERO. X: NO ARMOR / ARMOR / GOLD ARMOR, then NORMAL / HARD (not after GOLD ARMOR). ZERO: NORMAL / HARD; Zero plays alone. |
| VS mode | **VS MODE** on the title menu, then 1P VS 2P or 1P VS CPU. Against the CPU, pick ZERO, GOLD X or X + ZERO (then X or ZERO for yourself), then EASY / NORMAL / HARD. Then X's armor (only against ZERO). In 1P VS 2P controller 2 is Zero; against CPU gold X, and when you pick ZERO in X + ZERO, controller 1 is Zero. L or R on Zero's controller: black armor (see 0.28). |
| Pause | Controller 1's Start, as usual. |

## What works

- Player 2 runs, jumps, dashes and wall-kicks independently, with their own animation.
- Player 2 has their own buster shots and charge shots, with their own three-shot limit, and the shots hit enemies.
- **Enemies hurt player 2.** Contact damage, knockback and invincibility frames work like they do for player 1.
- **Enemies go after whichever player is closer.** This includes aiming and chasing, and player 2 can collect pickups.
- **Player 2 has a health bar** with a "Z" icon on the right edge of the screen, and it respects heart-tank max health. It hides along with player 1's during cutscenes.
- **Player 2 has their own colors**, Zero's red (or red armor when playing as a second X). Each player's charge glow stays on their own sprite.
- **Player 2 dying costs a shared life.** Player 2 bursts into energy orbs like player 1 does, and one life comes off the shared counter. After 2 seconds, player 2 presses Start to rejoin at full health.
- **Out of lives:** if no lives are left when player 2 dies, they stay out until a 1-up brings the count back above zero.
- If player 1 dies, player 2 drops out too. After the respawn, player 2 presses Start to rejoin.
- The camera follows the midpoint between the two players.
- The players can't drift more than 192 px apart horizontally, except in rooms that fit on one screen (boss rooms), where the walls are the limit.
- If player 2 goes far off-screen, or holds a direction for 4 seconds without moving (wedged in scenery), they're put back with player 1.
- Player 2 can leave at any time with Select and come back with Start.
- Zero switches to black armor (double damage) and back with L or R (see 0.25): controller 2 in co-op, controller 1 in Boss Rush as Zero (see 0.26.1), and Zero's controller in VS mode (see 0.28).

## Known issues

- **Slowdown in busy rooms.** Normal co-op play runs at about 94–100% speed (see 0.23 and 0.24). The busiest spots, mostly Doppler-stage bosses, still average about 85–90%, with short dips to half speed. VS 1 vs 2 on HARD runs at about 90% (see 0.19). The SNES CPU is the limit here. An emulator CPU overclock, if yours has one, removes the rest.
- **X has the buster only while Zero is in** (see 0.4.4 above). This is a video memory limit, not a choice that can be toggled.
- **Stage 5:** while one of the few enemies that use sprite palette 7 is on screen, Zero is drawn in X's colors.
- **Zero has no special weapons**, the same as in the stock game when you switch to him: his buster, his charged shots and the Z-Saber slash that follows a full charge.
- **Boss Rush as Zero:** the HUD shows X's icon for a moment at each stage start, until Zero beams in, and the sub-screen still shows X's lives icon.
- **The computer Zero is a simple player**, and since 0.27.1 his losses cost lives. He goes down most in the second Doppler stage (all of his losses in the bot sweep were there). He doesn't dodge most shots, and against a boss whose weak spot is high above the floor (the huge machine hanging from the ceiling in one of Doppler's stages) he can't reach it, so he did no damage there. He doesn't go for items or ride Ride Armors, and while X rides one he waits to beam in until X gets off. He leaves for the Doppler-stage teleporters like player 2 does, and beams back in on his own afterwards.
- **Trigger zones only check player 1.** Enemy spawners, camera sections and scripted events fire based on where player 1 is. If Zero runs far ahead, he gets warped back to X.
- **Heart tanks, sub tanks and armor capsules are player 1 only.**
- **Ride Armors are player 1 only.** Zero can't join while X is riding (a Start press then waits until X gets off), and the Robot Ride platforms only respond to X. Zero can play alongside a riding X if he joined before X got in.
- **Zero leaves for scripted moments:** the Doppler-stage teleporters, the boss-victory teleport, and the end of the Sigma fight. Press Start on controller 2 to rejoin afterwards.
- **FastROM by default.** The co-op code and the game's own code run in FastROM mode, which works in emulators and on flash carts. For original Cx4 cartridge timing, set `!FastGame = 0` and `!FastHook = 0` in `coop.asm` and rebuild.

## How it works

The game's player code is hard-wired to one object at `$7E:09D8`.

- **Second player.** Each frame, after player 1's normal update, the patch does the following:
  1. Swaps player 2's saved state into that slot. Only the 79 words that actually change during play are swapped (100 when player 2 is a second X, whose armor parts are live), using generated straight-line code.
  2. Runs the button remap with controller 2's input, then the stock player update, then the terrain and physics pass.
  3. Swaps player 2's state back out.
- **Rest of the frame.** The camera, HUD and trigger zones keep seeing player 1. Enemies see whichever player is closer (see Targeting).
- **Drawing.** Player 2 is drawn through a small proxy object inside the player block. They get their own tile base, so their animation frames go to separate VRAM. The sprite list fills the 128 OAM entries in drawing order and drops whatever doesn't fit, so when the last entry was in use the frame before (`DrawOrder`), the two players swap order every frame (`PartsHook`/`DrawHook`) and each one is cut at most every other frame.
- **Projectiles.** Shots are tagged with an owner when they spawn. Player 2's shots see player 2's position and counters during their updates.
- **Enemy contact.** Every enemy type calls one contact routine (`$04:CB31`). The patch runs it a second time with player 2's 15 hit-related fields swapped in, but only when the enemy is within 96 px of player 2.
- **Targeting.** Before each enemy update, and each pickup in the effects list, the patch checks which player is closer. If it's player 2, player 2's position, facing, health and hit fields stand in as "the player" for that object's update. Trigger objects (camera sections, spawners, events) always see player 1. Inside the unrolled object loops (since 0.23) the swap is left in place between objects: the next object that wants player 1, an object that doesn't aim (`TgtFlush`), or the end of the list (`TgtEnd`) puts player 1 back. Between two objects only the loop itself runs, and it reads nothing but the slots' active flags. Since 0.24 an object keeps its last target while that player is hurt or held (state $0E; one byte per object slot in `!TgtMem`), and it only switches when the other player is nearer by more than 16 px (`!TgtTie`), so a swap isn't spent on a near tie.
- **Solid objects.** Platforms, lifts and crates run their push-out, standing and carrying code once per player, and remember which platform each player is standing on. If the platform's own update has player 2 swapped in for targeting, the push-out and standing checks undo that first, and afterwards one 10-word swap (`SwapSA`, the words the solid and targeting sets don't share) goes straight back to it. Carrying only moves x and y, so it adds the platform's movement to wherever each player's position is at that moment, with no swap.
- **Health bar.** The HUD is a block of reserved sprite entries handed to the Cx4 chip. The patch reserves 8 more entries each frame for player 2's bar, and places them after the boss bar when one is on screen.
- **Zero.** The game already supports Zero in the player slot (`$0A8E` = 2). Player 2's copy is set up the way the game's own switch does it: animation set, frame pointer, hitbox, and Zero's palette from `$0C:B580`. Max health is swapped to 28 while player 2 runs.
- **Colors.** X's charge glow rewrites sprite palette 1 in RAM. Player 2 keeps a private copy that is swapped in only during their update, and the result is written to palette 7 whenever it changes: Zero's own palette, or during a charge glow Zero's palette blended halfway toward the glow's tint. A second X gets a recolored copy with red and blue exchanged on bluish colors.
- **Sprite memory.** Zero's animation frames use sprite tiles $50–$7C, which the game otherwise uses for special-weapon graphics (and, in the Doppler stages, for some of X's effects). His health-bar icon lives in tiles $7E/$7F as two tiles drawn four times, flipped for the bottom half.
- **Death.** The patch calls the game's own death-burst routine (`$04:92E8`) at player 2's position, and loads the orb graphics into player 2's tile area.
- **Black Zero.** Before the button remap, `ZBlackKey` checks controller 2's new presses for L or R (leaving out any the button options give to shot, jump or dash) and flips a flag at `$7EFF90`, high WRAM the game never writes, so it lasts through stage loads. The palette code already had a black Zero for the HARD CPU: `IsBlackPal` now also answers yes for the flag, and the charge glow tints the black colors the same way. Damage goes through the enemy-hit routine, at the spot where it subtracts the damage-table value (`$04:CF38`, the `BossDmg` hook, now installed in every build): `ZBlackDmg` doubles that value when the shot slot that hit (X) is tagged as player 2's. Each of Zero's attacks, the saber included, is an object in the shot list, so they all pass through there.
- **Double Boss.** When a Maverick (object types $52–$59) sets the boss pointer (`$1F1F`), the patch copies its 64-byte object into a free enemy slot, offset sideways. All eight Mavericks start their death through one routine (`$02:E0BA`), except Blast Hornet, which has its own (`$39:A0D7`). The patch hooks both. If the other twin still has health, the dying one skips the player freeze and victory sequence: it explodes on its own, then it and its attached parts (Hornet's and Buffalo's wings) are removed. The second bar is 8 more reserved HUD entries, rebuilt only when the health shown changes.
- **Title menus.** The patch draws the five title items and the Boss Rush and VS submenus itself, into the game's VRAM text queue in the game's own format, and moves the title X beside the lit item.
- **Boss Rush.** BOSS RUSH sets a flag in high WRAM and runs GAME START's new-game setup. Where the game picks the intro stage or the stage select (`$00:9A1C`), the patch picks the first Maverick stage whose weapon isn't owned yet. At stage load it sets the starting checkpoint (`$1FB5`) to 2. Twins only spawn while the flag is set. In a chain, once the next boss's graphics are in, `ChainSide` checks which side of the screen the bosses appear on (`!ChainX`) and whether a player is on that side; if so the last 32 frames before it appears fade the brightness shadow (`$00B4`, written to `$2100` in the NMI) from 15 to 0 and back, and at 0 `ChainPlace` sets the players' x (and previous x, `$09FA`) and their facing, both the sprite flag in `$09E9` and the one the player update keeps (`$0A41`). The fade ends before the boss appears because, as a boss appears, the game sends data to the sound chip and stops for several frames, which would have held the screen dark.

- **VS mode.** VS MODE sets a flag in high WRAM and runs GAME START's new-game setup into stage $0C at checkpoint 6, the rematch room. That checkpoint is forced again after each round, because a lost life in that stage would normally send you to the teleporter room. The room's boss is deleted before its first update. Zero joins on his own, as if Start were pressed on controller 2, and is moved to the right wall. After each shot's update, VS mode tests it against the other player with the game's overlap check (`$04:CC5C`) and, on a hit, runs the game's player-hit routine (`$04:CD6A`) with that player's hit fields swapped in. A round ends through mode 6, the "lost a life" fade and reload, so each round starts with a clean room. The results use the game's dialog box object (`$02:FCB1`), with seven messages added after the game's own in the free space of the text bank (the score lines and the talk before round 1). During the talk both players' input is cleared. To get back to the title: GAME START enters the game loop with a jump, so the patch saves the stack pointer there and later returns from that level into the title loop. The CPU builds a controller-2 word each frame from both players' positions, X's shots in flight and Zero's charge state. Its reaction times, odds and distances come from a small table with one column per level (`AiLv` in `vsai.asm`), and HARD's extra moves (dash jumps, jumping to meet X in the air, letting buster lemons through, wall play) are switched on by entries in that table. Wall play is a small state machine in `AiWallRun`: head for the wall behind Zero, jump at it, press jump each time he is back on the wall (state $12) while holding toward it to climb, then press jump with the opposite direction (and dash) to kick off. HARD's damage is applied when one of Zero's shots hits X (`VsCpuBoost`): for shot types 0–3 (buster, half charge, saber slash, full charge) it uses its own table, `VsHardDmg`, instead of the normal one. The HARD touch (`VsContact`) runs after player 2's update, with X back in the player block. If the two bodies are less than 16 px apart across and 28 px up or down, and X isn't blinking, it calls the game's player-hurt routine (`$04:CD6A`). That routine reads the attacker's x position and damage through the direct page, so a free shot slot stands in for Zero: his x and the damage go in, and the slot's bytes are put back after. Black Zero is a palette swap where player 2's palette is written to the screen (`P2PalSync`): while the HARD CPU plays Zero, each color still equal to Zero's own palette is replaced by the same entry of a black copy (`ZeroBlackPal`), and the charge glow tints that copy.

- **1 vs 2.** The third fighter (player 3, the CPU X) has his own copy of the player block at `$7E:F300`, in RAM the game leaves unused in the arena. After player 2's update the three blocks are rotated in one pass, straight from player 2 to player 3 (`SwapRot23`). The stock player update then runs for him with his AI's buttons, followed by the terrain pass, and he is swapped back out.
  - His animation frames and shot graphics live in sprite page 1 (VRAM `$7000`), which the arena doesn't use. Every upload his update queues is moved up by $1000, and his sprites set the name-table bit. He is drawn with sprite palette 6.
  - Shots get their owner (0, 1 or 2) the moment their slot is allocated: the slot allocator (`$02:D8C4`) is hooked. This replaced the before/after snapshots of the shot list in every mode.
  - His AI is `vsai.asm` assembled a second time with its state at `$7E:F2A0` (`vsai3.asm`), so no AI state is swapped.
  - When you play Zero, player 1 is turned into Zero at the start of each round, the same way player 2 is, after player 3 has copied X from him.
- **Speed in VS mode.**
  - The game's seven object-list loops step through 116 slots each frame. They're replaced by unrolled checks that only call the active objects (`fastloops.asm`; in every mode since 0.23).
  - Player 1's health bar is rebuilt only when it changes.
  - A CPU's palette is swapped in only when its update actually loads one. The charge glow and the hit flashes all go through the game's palette loader.
  - Zero's tinted glow palettes are cached.
  - A shot more than 64 px from a player skips the overlap test.

## Source

`source/` holds the following:

- **Patch source:** `coop.asm` (Asar), the Double Boss module `dblboss.asm`, the Boss Rush modules `bossrush.asm` and `chain.asm`, the VS mode modules `vsmode.asm`, `vsai.asm`, `vsai3.asm` and `p3.asm` (1 vs 2), plus the generated `swaps.asm`, `swaps3.asm`, `fastrom.asm`, `zicon.asm`, `fastloops.asm` and `fastloops_hooks.asm`, their generators, and the measured data they're built from (`writeset.json`, `hitset.json`, `fastsites.json`).
- **Test harness:** a headless snes9x driver used for testing, profiling and tracing.
- **Emulator patch:** the debug-hook changes for snes9x.

To rebuild:

```
python3 source/src/gen_swaps.py
python3 source/src/gen_fastrom.py
python3 source/src/gen_zicon.py
python3 source/src/gen_fastloops.py
cp "Mega Man X3 (USA).sfc" coop.sfc
asar source/src/coop.asm coop.sfc
```

For double bosses in every Maverick fight (not just Boss Rush), use `asar -DDoubleBoss=1 source/src/coop.asm coop.sfc` on a fresh copy of the ROM.
