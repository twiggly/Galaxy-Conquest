# Galaxy Conquest

A turn-based multiplayer space strategy game about exploration, colonisation, local logistics, hidden information, brutal fleet combat, and galaxy-scale megaprojects.

Players begin on isolated homeworlds in separate named galaxies. They mine metal and gas, construct ships, scout unknown planets, colonise empty worlds, reinforce borders, attack rivals, and pursue one of three win conditions: **Conquest**, **Dominance**, or **Singularity**.

This version favours fast play: one decision per active planet, a one-minute order timer, unlimited stationed fleets, mission-specific fleet behaviour, simplified scouting, real galaxy names, and countdown-based megaprojects.

---

## Table of Contents

1. [Game Overview](#game-overview)
2. [Mini Quick Reference](#mini-quick-reference)
3. [Core Definitions](#core-definitions)
4. [Game World](#game-world)
5. [Galaxy Names](#galaxy-names)
6. [Starting Setup](#starting-setup)
7. [Resources and Cargo](#resources-and-cargo)
8. [Planets](#planets)
9. [Buildings](#buildings)
10. [Mines](#mines)
11. [Shipyards and Ship Production](#shipyards-and-ship-production)
12. [Ships](#ships)
13. [Player Decisions](#player-decisions)
14. [Travel](#travel)
15. [Missions](#missions)
16. [Mission Behaviour](#mission-behaviour)
17. [Fog of War](#fog-of-war)
18. [Probes and Scouting](#probes-and-scouting)
19. [Combat](#combat)
20. [Capturing and Devastating Planets](#capturing-and-devastating-planets)
21. [Colonisation](#colonisation)
22. [Megaprojects](#megaprojects)
23. [Blackhole Generator](#blackhole-generator)
24. [Research Facility and Singularity](#research-facility-and-singularity)
25. [Destroyed Galaxies](#destroyed-galaxies)
26. [Megaproject Visibility and Timing](#megaproject-visibility-and-timing)
27. [Round Structure](#round-structure)
28. [Simultaneous Mission Resolution](#simultaneous-mission-resolution)
29. [Win Conditions](#win-conditions)
30. [Example Round Orders](#example-round-orders)
31. [Full Quick Reference](#full-quick-reference)
32. [Design Notes](#design-notes)

---

## Game Overview

Each player controls an expanding space empire. The core loop is:

1. Produce metal and gas.
2. Build infrastructure.
3. Construct ships.
4. Scout unknown planets.
5. Colonise or conquer planets.
6. Reinforce key worlds.
7. Defend or destroy megaprojects.
8. Win by Conquest, Dominance, or Singularity.

The game is designed around limited decisions, local resources, fog of war, active scouting, harsh combat attrition, and public endgame projects that force players to react.

---

## Mini Quick Reference

| Category | Rule |
|---|---|
| Players | 2-10 players |
| Map | Scales by player count and targets roughly 6-8 planets per player |
| Decisions | 1 decision per active planet per round |
| Timer | 1 minute per player per round |
| Resources | Metal and gas are stored locally on planets |
| Ship storage | Unlimited stationed ships |
| Hub | Required core structure for a planet to be colonised, occupied, and active; costs 10 metal |
| Cargo | Cargo may be carried only on Transport and Colonise missions |
| Same-galaxy travel | 4 gas per ship, 1 round |
| Intergalactic travel | 12 gas per ship, 2 rounds |
| Probe scout travel | 2 gas same-galaxy; 6 gas intergalactic |
| Scouting | Probes are constructed ships; Scout missions use discounted probe travel; enemy scans destroy the probe after information is revealed |
| Combat | Defender wins ties |
| Winner losses | Winner chooses eligible ship or defence losses equal to loser combat power |
| Raid | Never captures occupied planets and never destroys completed Hubs |
| Capture | Only Invade attacks capture occupied planets; requires at least 1 surviving non-probe attacking ship after winner losses |
| Megaproject final warning | Issued at 2 rounds remaining, so same-galaxy attacks launched next round can still arrive |
| Elimination | Checked only during the Victory Phase; travelling fleets do not prevent elimination |
| Conquest | Eliminate all other players by leaving them with no completed Hubs and no Hubs under construction |
| Dominance | Control at least 60% of Developed Hubs for 3 consecutive Victory Phases |
| Singularity | Complete a Research Facility countdown megaproject |

---
## Core Definitions

| Term | Meaning |
|---|---|
| Empty planet | A planet with no owner, no Hub completed or under construction, no normal buildings or megaprojects, no stationed ships, and no stored resources |
| Colony under construction | A planet with a Hub under construction |
| Occupied planet | A planet with a completed Hub |
| Controlled planet | Either an occupied planet or a colony under construction |
| Active planet | An occupied planet with a completed Hub; only active planets produce resources and provide decisions |
| Developed Hub | A completed Hub on a planet with at least one completed normal building; counts toward Dominance victory |
| Outpost | An occupied planet with a completed Hub and zero completed normal buildings; prevents elimination but does not count toward Dominance |
| Starter Building | An optional first Metal mine or Gas mine started by a Colonise mission from carried metal; it completes with the Hub |
| Destroyed galaxy | A named galaxy permanently removed from the game by a Blackhole Generator |
| Stationed ships | Ships currently present at a controlled planet and available to defend that planet |
| Travelling fleet | Ships currently moving to or from a mission target |
| Returning fleet | A travelling fleet that has resolved its mission and is returning to its origin at the end of the Movement and Mission Phase |
| Core structure | A special structure that does not count against planet size; currently only the Hub |
| Hub | The core structure that establishes and maintains planetary control |
| Normal building | A Metal mine, Gas mine, Shipyard, or Rocket launcher |
| Non-defensive normal building | A completed normal building that is not a Rocket launcher |
| Defensive building | A building that contributes combat power while defending; currently only the Rocket launcher |
| Defence pool | The total current defensive power provided by Rocket launchers on a planet |
| Building slot | One unit of a planet's size capacity used by a normal building, normal-building construction project, normal-building deconstruction project, or megaproject. Hubs do not use building slots |

Only **active planets** generate resources and provide planet decisions.

Colonies under construction count as controlled for elimination and defence purposes, but they do not produce resources and do not provide a decision until their Hub is complete.

A planet may have zero normal buildings and still remain occupied if it has a completed Hub. Such a planet is an Outpost: it remains controlled and prevents elimination, but it does not count toward Dominance.

Normal buildings and megaprojects can only be started on active planets with completed Hubs, except for the initial Hub and optional Starter Building started by a successful Colonise mission.

Megaprojects are not normal buildings. A megaproject can occupy building slots, but a megaproject by itself never makes a planet occupied or active. Only a completed Hub does that.

Travelling fleets do not count as controlled planets and do not prevent elimination.

### General Adjudication Principles

Use these principles whenever a timing question is not answered by a more specific rule.

1. **Specific rules override general rules.** Mission, combat, capture, colonisation, and megaproject rules override general phase rules when they conflict.
2. **Orders must be legal when costs are paid.** If an order cannot be fully paid or legally completed when the Movement and Mission Phase begins, that order fails and no partial effect occurs unless a rule explicitly allows partial completion.
3. **Costs are paid before effects resolve.** Resources spent on normal buildings, ships, missions, repairs, and megaprojects are removed before the order's effect occurs. Hub and optional Starter Building costs are paid from carried cargo when a Colonise mission resolves.
4. **Arrivals cannot fund earlier orders.** Resources delivered during the Movement and Mission Phase cannot be used to pay for orders already submitted that round. They become spendable starting in the next round.
5. **New arrivals cannot receive orders immediately.** Ships that arrive or are produced during a round cannot be assigned to new missions until a later round, but they may defend if the mission resolution order places them at the target before an attack.
6. **Control updates immediately.** After each colonisation, capture, devastation, or colony destruction, update planet control before resolving the next mission at that planet.
7. **Elimination and victory wait until the Victory Phase.** A player is not eliminated in the middle of the Movement and Mission Phase, even if they temporarily control no planets.
8. **No hidden partial refunds.** Failed, cancelled, or wasted orders do not refund metal, gas, cargo, or repairs unless a specific rule says they do.

---
## Game World

The game supports **2-10 players**.

Each player starts in a **different named galaxy** on a **random planet**.

Because each player starts in a different galaxy, the maximum player count is **10**.

### Map Scaling

Use the following map sizes by default. These values target roughly **6-8 planets per player**, which keeps exploration meaningful without making the endgame cleanup too slow.

| Players | Named Galaxies Used | Planets per Galaxy | Total Planets | Planets per Player |
|---:|---|---:|---:|---:|
| 2 | 3 | 5 | 15 | 7.5 |
| 3 | 4 | 5 | 20 | 6.7 |
| 4 | 5 | 6 | 30 | 7.5 |
| 5-6 | 7 | 6 | 42 | 7-8.4 |
| 7-8 | 8 | 7 | 56 | 7-8 |
| 9-10 | 10 | 7 | 70 | 7-7.8 |

Use the first galaxies from the standard galaxy list in [Galaxy Names](#galaxy-names).

For a faster or slower game, players may agree to use a smaller or larger map.

A simple alternative is:

```text
Use about 7 planets per player.
Use at least one more galaxy than the number of players, up to a maximum of 10 galaxies.
```

---
## Galaxy Names

The game uses real galaxy names by default.

| Order | Galaxy Name | Short Code |
|---:|---|---|
| 1 | Milky Way | MW |
| 2 | Andromeda | AND |
| 3 | Triangulum | TRI |
| 4 | Large Magellanic Cloud | LMC |
| 5 | Small Magellanic Cloud | SMC |
| 6 | Whirlpool | WHI |
| 7 | Sombrero | SOM |
| 8 | Pinwheel | PIN |
| 9 | Bode's Galaxy | BOD |
| 10 | Cigar Galaxy | CIG |

Planets are numbered within each galaxy.

Default planet format:

```text
Milky Way-P4 = Planet 4 in the Milky Way
Andromeda-P2 = Planet 2 in Andromeda
```

Short code format:

```text
MW-P4 = Planet 4 in the Milky Way
AND-P2 = Planet 2 in Andromeda
```

Public megaproject messages use the real galaxy name.

Example:

```text
Space-time disturbances emanate from Andromeda...
```

---

## Starting Setup

Each player begins with one occupied starting planet.

### Starting Planet Stats

| Stat | Value |
|---|---:|
| Size | 10 |
| Metal abundance | 5 |
| Gas abundance | 5 |

### Starting Structures and Buildings

| Structure or Building | Quantity |
|---|---:|
| Hub | 1 completed |
| Metal mine | 1 |
| Gas mine | 1 |
| Shipyard | 1 |
| Rocket launcher | 1 |

The starting Hub does not count against the starting planet's size limit.

### Starting Resources

| Resource | Amount |
|---|---:|
| Metal | 40 |
| Gas | 40 |

Starting resources are stored on the player's starting planet.

---
## Resources and Cargo

There are two resources:

| Resource | Used For |
|---|---|
| Metal | Buildings, ships, colonisation, repairs, megaprojects |
| Gas | Ship travel and megaprojects |

Resources are stored **locally on planets**, not globally.

A planet can only spend resources stored on that planet, except that a Colonise mission spends carried metal to start a Hub and optional Starter Building when the mission resolves.

There is **no storage limit** for metal or gas.

Example:

| Planet | Metal Stored | Gas Stored |
|---|---:|---:|
| Milky Way-P1 | 80 | 45 |
| Milky Way-P3 | 5 | 10 |

Milky Way-P3 cannot build a 20-metal normal building unless it produces more metal or receives transported metal.

Resources delivered by Transport missions become stored at the destination when the mission resolves. On a successful Colonise mission, 10 carried metal is spent on the Hub. The player may also spend 20 carried metal to start one optional Starter Building, which must be either a Metal mine or a Gas mine. Any unspent carried resources become stored on the colony. Delivered or unspent resources cannot be used to pay for orders already submitted that round.

### Cargo Capacity

Each unit of metal or gas uses **1 cargo capacity**.

A ship may carry any mix of metal and gas up to its cargo capacity.

Example: a cruiser with 30 cargo capacity may carry:

- 30 metal
- 30 gas
- 10 metal for a Hub and 20 metal for a Starter Building
- Any other metal/gas mix totalling 30 resources

Cargo may be loaded only on **Transport** and **Colonise** missions.

Attack, Scout, and Reinforce missions cannot carry metal or gas. This prevents attacks or reinforcements from secretly moving resources.

If a cargo-carrying ship is destroyed, its cargo is destroyed with it.

If a mission carrying cargo fails and returns, the cargo returns with the surviving fleet unless the fleet is destroyed, its origin is no longer controlled, or another rule destroys the cargo.

---

## Planets

Each planet has three stats:

| Stat | Purpose |
|---|---|
| Size | Limits the number of normal buildings and megaproject building slots the planet can hold |
| Metal abundance | Determines metal mine production |
| Gas abundance | Determines gas mine production |

A planet's **size** equals the maximum number of normal-building and megaproject slots it can contain.

Hubs do **not** count against planet size.

Example:

| Planet Size | Maximum Normal-Building / Megaproject Slots |
|---:|---:|
| 6 | 6 slots |
| 10 | 10 slots |
| 12 | 12 slots |

### Planet Generation

All planets are generated at the start of the game, but their stats are hidden by fog of war until discovered.

For simpler manual play, planet stats may instead be generated when first probed or colonised.

New planets have **20 points** distributed between:

- Size
- Metal abundance
- Gas abundance

Use these limits:

| Stat | Minimum | Maximum |
|---|---:|---:|
| Size | 4 | 12 |
| Metal abundance | 2 | 10 |
| Gas abundance | 2 | 10 |

The total must always equal **20**.

Example valid planets:

| Size | Metal Abundance | Gas Abundance | Total |
|---:|---:|---:|---:|
| 8 | 7 | 5 | 20 |
| 10 | 4 | 6 | 20 |
| 6 | 10 | 4 | 20 |
| 12 | 4 | 4 | 20 |

---
## Buildings

The **Hub** is a core structure, not a normal building. It establishes and maintains control of a planet.

Normal buildings and megaprojects count against a planet's size limit. Hubs do **not** count against a planet's size limit.

Normal buildings take **2 rounds** to construct, except Starter Buildings created by Colonise missions, which take **1 round**.

Deconstructing a normal building takes **1 round**.

Deconstructing a normal building refunds nothing.

A **normal building** is a Metal mine, Gas mine, Shipyard, or Rocket launcher. Megaprojects use their own rules.

Normal buildings can only be built on active planets with completed Hubs, except for one optional Starter Building created during a Colonise mission.

A Hub cannot be voluntarily deconstructed. A player may deconstruct all normal buildings on a planet, but the planet remains controlled as long as its Hub remains intact.

### Hub

The Hub is required for planetary control.

| Core Structure | Cost | Build Time | Slots Used | Effect |
|---|---:|---:|---:|---|
| Hub | 10 metal | 1 round | 0 | Establishes ownership and makes the planet active once complete |

A Hub:

- is created only through a Colonise mission or starting setup,
- does not produce resources,
- does not provide defence,
- does not count against the planet's size limit,
- cannot be voluntarily deconstructed,
- is captured intact when an occupied planet is captured,
- is destroyed when a planet is devastated or when its galaxy is destroyed.

A planet with a Hub under construction is a colony under construction. A planet with a completed Hub is occupied and active.

### Construction and Deconstruction Queues

A planet may have multiple normal buildings under construction or deconstruction at the same time.

Each **Build building** decision starts exactly 1 normal building. Hubs are not started with Build building decisions; they are started by Colonise missions. The optional Starter Building from a Colonise mission also does not use a Build building decision.

Each **Deconstruct building** decision starts removing exactly 1 completed normal building.

Construction and deconstruction continue automatically after they have started and do not use future planet decisions.

Normal buildings under construction count against the planet's size limit immediately, but they do not function until completed. Starter Buildings follow this same slot rule.

Hubs under construction do not count against the planet's size limit.

Normal buildings being deconstructed continue to count against the planet's size limit and continue to function until deconstruction completes.

Because Production Phase resource generation happens before deconstruction completion, a mine being deconstructed still produces one final time during the Production Phase in which it is removed.

A building slot is freed only when a normal building under deconstruction is actually removed.

### Normal Building List

| Building | Cost | Build Time | Effect |
|---|---:|---:|---|
| Metal mine | 20 metal | 2 rounds | Produces metal |
| Gas mine | 20 metal | 2 rounds | Produces gas |
| Shipyard | 30 metal | 2 rounds | Builds ships |
| Rocket launcher | 40 metal | 2 rounds | Adds 4 maximum defence to the planet's defence pool |

Rocket launchers have no special numeric cap. They are limited by the planet's normal building slots like every other normal building.

---
## Mines

Each mine produces resources every round while on an active planet.

### Metal Mine

A metal mine produces:

```text
1 metal × planet metal abundance
```

Example:

| Metal Mines | Metal Abundance | Metal Produced Per Round |
|---:|---:|---:|
| 1 | 5 | 5 |
| 2 | 5 | 10 |
| 3 | 5 | 15 |

### Gas Mine

A gas mine produces:

```text
1 gas × planet gas abundance
```

Example:

| Gas Mines | Gas Abundance | Gas Produced Per Round |
|---:|---:|---:|
| 1 | 5 | 5 |
| 2 | 5 | 10 |
| 3 | 5 | 15 |

---

## Shipyards and Ship Production

A shipyard costs **30 metal**.

Each active, non-disabled shipyard can build **1 ship per round** when the planet uses the **Produce Ships** decision.

A planet with multiple shipyards may build multiple ships during the same Produce Ships decision.

A Produce Ships decision may build any mix of ship types, as long as the number of ships does not exceed the number of usable shipyards and the planet can pay the total metal cost.

The order must name the ship types and quantities being produced.

If the full declared production cannot be paid for when costs are paid, the entire Produce Ships order fails and no ships are produced.

Ships produced during a Produce Ships decision are completed during the Movement and Mission Phase before arriving attacks are resolved. Newly produced ships may defend that round, but they cannot be sent on missions until a later round.

| Shipyards on Planet | Ships Produced When Producing Ships |
|---:|---:|
| 1 | 1 ship |
| 2 | 2 ships |
| 3 | 3 ships |

There is **no ship capacity limit**. Any number of ships may be stationed on a planet.

If a planet is captured during Round N, captured shipyards on that planet cannot produce ships during Round N+1. They function normally again starting in Round N+2.

---

## Ships

| Ship | Cost | Attack Power | Cargo Capacity | Role |
|---|---:|---:|---:|---|
| Probe | 5 metal | 0 | 0 | Scouting |
| Fighter | 10 metal | 1 | 0 | Cheap combat |
| Cruiser | 20 metal | 0 | 30 | Transport and colonisation |
| Destroyer | 50 metal | 4 | 0 | Heavy combat |

### Probe

Probes are constructed by shipyards and behave like ships.

They have no attack power and no cargo capacity.

Probes are destroyed after successfully scanning enemy-controlled planets, including occupied planets and colonies under construction.

### Fighter

Fighters are cheap combat ships.

They have **1 attack power** and no cargo capacity.

### Cruiser

Cruisers are transport and colonisation ships.

They have **0 attack power** and **30 cargo capacity**.

A cruiser can colonise alone because it can carry enough metal to start a Hub and, if desired, one Starter Building.

### Destroyer

Destroyers are heavy combat ships. They are more shipyard-efficient and gas-efficient than fighters, but less metal-efficient.

They have **4 attack power** and **0 cargo capacity**.

Destroyers cannot colonise or transport resources by themselves.

---

## Player Decisions

Each player may make **1 decision per active planet per round**.

Each player has **one minute** to submit all decisions for the round.

This is one minute total per player, not one minute per planet.

### Decisions

| Decision | Description |
|---|---|
| Build building | Start constructing 1 normal building |
| Deconstruct building | Start removing 1 normal building |
| Produce ships | Use shipyards on that planet to produce ships |
| Repair defences | Restore a declared number of damaged defence points on that planet |
| Scout | Send a probe to reveal information |
| Attack | Send a fleet to raid or invade an enemy-controlled planet |
| Transport | Move resources between controlled planets |
| Reinforce | Move ships to another controlled planet |
| Colonise | Send cargo ship with at least 10 metal to start a Hub on an empty planet; may also carry 20 metal for one Starter Building |
| Start Blackhole Generator | Begin galaxy-destruction megaproject |
| Start Research Facility | Begin Singularity megaproject |

### Order Legality and Payment

Orders are submitted during the Orders Phase and paid for during the Movement and Mission Phase.

An order is legal only if the acting planet is still active and controlled by the ordering player when costs are paid.

An order that cannot be fully paid or legally performed when costs are paid fails with no partial effect.

Players may order Attack or Colonise missions using current or last known information. The mission's actual result is determined by the target's true state when the mission resolves.

### Automatic Effects

These do not use a planet decision:

| Automatic Effect |
|---|
| Resource production |
| Hub and normal-building construction progress |
| Deconstruction progress |
| Travelling fleets continuing movement |
| Passive defence |
| Megaproject progress after it has started |

### Timer Rules

| Situation | Result |
|---|---|
| Player submits before timer ends | Submitted decisions are used |
| Timer expires before all active planets have decisions | Active planets without decisions take no action |
| Construction already in progress | Continues automatically |
| Deconstruction already in progress | Continues automatically |
| Travelling ships | Continue travelling automatically |
| Stationed ships | Defend automatically |
| Megaprojects already active | Continue automatically |

There are no default orders in the core rules.

---
## Travel

Ships can travel within the same galaxy or between galaxies.

| Travel Type | Travel Time | Gas Cost |
|---|---:|---:|
| Same galaxy | 1 round | 4 gas per ship |
| Different galaxy | 2 rounds | 12 gas per ship |

Gas must be paid from the origin planet.

Scout missions use discounted probe travel:

| Scout Travel Type | Travel Time | Gas Cost |
|---|---:|---:|
| Same galaxy probe scout | 1 round | 2 gas per probe |
| Different galaxy probe scout | 2 rounds | 6 gas per probe |

The scout discount applies only to Scout missions made by probes. All other missions, including moving probes by Reinforce, use normal travel costs.

Travel time represents the full mission duration.

For missions that return, the listed travel time includes travelling to the target, completing the mission, and returning to the origin planet.

For missions that stay, the listed travel time represents travelling to the destination and becoming available there.

Fleets are unavailable while travelling.

Mission countdowns are measured in rounds after the mission is launched. A mission launched this round with a travel time of 1 round resolves during the next round's Movement and Mission Phase. A mission with a travel time of 2 rounds resolves during the following round's Movement and Mission Phase.

### Arriving and Returning Fleets

A fleet that succeeds on a mission that **stays** becomes stationed at the destination immediately when that mission resolves. It may defend against later attacks at that same planet during the same Movement and Mission Phase, but it cannot be given new orders until a later round.

A fleet that succeeds on a mission that **returns** resolves its mission effect at the target, then becomes a returning fleet. Returning fleets complete their return at the end of the Movement and Mission Phase and become available at the start of the next round.

Returning fleets do not defend either the destination or their origin during the round in which they resolve.

Delivered cargo becomes stored at the destination immediately when the delivery resolves, even though Deliver ships are already returning and do not defend the destination.

Fleets remember their origin planet. If a fleet must return to its origin and that planet is no longer controlled by the fleet owner at the end of the Movement and Mission Phase, the returning ships and cargo are lost.

Fleets cannot be attacked or intercepted while travelling unless a future rule specifically allows it.

Travelling fleets do not prevent player elimination.

---

## Missions

| Mission | Purpose |
|---|---|
| Scout | Send a probe to reveal planet information |
| Attack | Raid or invade an enemy-controlled planet |
| Transport | Move resources between controlled planets |
| Reinforce | Move ships between controlled planets |
| Colonise | Send cargo ship with at least 10 metal to start a Hub on an empty planet; may also carry 20 metal for one Starter Building |

---
## Mission Behaviour

Fleet behaviour is determined by the mission type. There is no separate fleet stance system.

### Scout

A probe travels to the target using discounted Scout travel costs, reveals information, and then either returns or is destroyed depending on the target.

| Target | Result |
|---|---|
| Empty planet | Probe reveals information and returns |
| Own controlled planet | Probe reveals information and returns |
| Enemy occupied planet | Probe reveals information, then is destroyed |
| Enemy colony under construction | Probe reveals information, then is destroyed |
| Destroyed galaxy | Cannot be scouted |

A returning probe follows the normal returning fleet rules.

### Attack

When sending an attack, choose one attack mode.

Attack missions may not carry cargo.

| Attack Mode | Result |
|---|---|
| Raid | If the attacker wins against an occupied planet, defending ships, defensive buildings, and any megaproject on the target are destroyed, but the completed Hub survives and the planet is not captured. Surviving attackers return. |
| Invade | If the attacker wins against an occupied planet and at least 1 non-probe attacking ship survives winner losses, the planet is captured. Surviving attackers stay on the captured planet. If the attacker fails to capture, surviving attackers return. |

Players may order attacks using current or last known information. The attack resolves against the target's actual current owner when the attack arrives.

If the target is controlled by an enemy when the attack resolves, the attack proceeds against that current owner, even if the target changed owner after the attack was launched.

If the target is empty, destroyed, or controlled by the attacker when the attack resolves, the attack is cancelled and surviving attackers return. Mission gas is not refunded.

Raid attacks never capture occupied planets and never destroy completed Hubs. They are used to weaken defences or destroy megaprojects.

A successful Raid against an occupied planet does not affect the completed Hub, completed non-defensive normal buildings, normal buildings under construction, normal buildings being deconstructed, or stored resources. The original owner keeps the planet.

If an **Invade** attack wins against an occupied planet but no non-probe attacking ship survives winner losses, the target is devastated instead of captured.

Against a colony under construction, any winning Attack destroys the incomplete Hub, destroys the colony, and leaves the planet empty. Surviving attacking ships return, regardless of whether the attack was a Raid or Invade.

### Transport

Transport missions move resources between controlled planets.

When sending resources, choose one transport mode.

Only Transport and Colonise missions may carry cargo.

| Transport Mode | Result |
|---|---|
| Deliver | Ships deliver cargo immediately and return. Delivered cargo becomes stored at the destination, but Deliver ships do not defend there. |
| Relocate | Ships deliver cargo immediately and stay at the destination. Relocating ships become stationed and may defend against later attacks at that planet in the same Movement and Mission Phase. |

Transport missions cannot target enemy planets.

If the destination is no longer controlled by the transporting player when the mission resolves, the transport fails and the fleet returns with its cargo. Mission gas is not refunded.

Resources delivered this round cannot be spent until the next round.

### Reinforce

A Reinforce mission moves ships from one controlled planet to another controlled planet.

Reinforce missions may not carry cargo.

Reinforcing ships stay at the destination and may defend against later attacks at that planet in the same Movement and Mission Phase.

If the destination is no longer controlled by the reinforcing player when the mission resolves, the mission fails and the fleet returns. Mission gas is not refunded.

### Colonise

A Colonise mission sends cargo ships to an empty planet with enough metal to start a Hub.

Colonise missions may carry cargo. At minimum, they must carry **10 metal** to pay for the Hub.

When a Colonise mission successfully starts a Hub, the colonising player may also spend **20 carried metal** to start one optional **Starter Building**. A Starter Building must be either a Metal mine or a Gas mine.

If the target is empty when the Colonise mission resolves, 10 carried metal is spent immediately, a Hub begins construction, and the colony is created. If a Starter Building is chosen, its 20 metal cost is also spent immediately from carried cargo and the Starter Building begins construction. Any unspent carried resources become stored on the colony.

A Starter Building takes **1 round** to complete and completes at the same time as the Hub. It does not function until the Hub is complete. It counts against the planet's size limit as soon as it is started.

Colonising ships become stationed at the colony immediately. They may defend against later attacks at that planet during the same Movement and Mission Phase, but they cannot be given new orders until a later round.

If the target is no longer empty when the Colonise mission resolves, the mission fails and the ships return with their cargo. Mission gas is not refunded.

---
## Fog of War

Fog of war is active.

Players know the full list of galaxy names and planet coordinates from the start, but they do not automatically know the full state of those planets.

### Always Visible Information

Players always know:

| Information | Visibility |
|---|---|
| Their own planets | Fully visible |
| Their own stationed ships | Fully visible |
| Their own stored resources | Fully visible |
| Their own Hubs, buildings, and construction | Fully visible |
| Their own travelling fleets | Fully visible |
| Destroyed galaxies | Public |
| Public megaproject warnings | Public |
| Galaxy containing an active megaproject | Public |
| Exact megaproject planet after midpoint warning | Public |

### Hidden Information

Players do not automatically know:

| Information | Visibility |
|---|---|
| Unexplored planet stats | Hidden |
| Enemy planet ownership | Hidden unless revealed by probing, battle, public megaproject information, or another public effect |
| Enemy Hubs and buildings | Hidden unless ownership or colony status is revealed |
| Enemy ships | Hidden |
| Enemy stored resources | Hidden |
| Enemy construction | Hidden unless publicly announced |
| Exact megaproject planet | Hidden until probed or publicly revealed |
| Captures, raids, and devastations | Hidden from non-participants unless caused by a public effect |

### Last Known Information

When a planet is probed or fought over, the player records its information as **last known information**.

That information may become outdated.

Example:

A player probes Andromeda-P4 in round 5 and sees medium defences. By round 8, that planet may have more ships, more buildings, damaged defences, a different owner, or a megaproject.

### Battle Reports

Only players who participate in a battle receive a battle report for that battle.

A battle report reveals:

| Category | Information Revealed |
|---|---|
| Target | Planet attacked |
| Participants | Attacker and defender |
| Attack mode | Raid or Invade |
| Combat totals | Total attacker combat power and total defender combat power |
| Result | Winner and loser |
| Losses | Ships lost by each side and defence pool damage or destruction |
| Planet result | No change, captured, devastated, emptied, or colony destroyed |
| Megaproject result | Whether a megaproject was present and destroyed |
| Captured resources | Amount captured and destroyed, but only if the planet was captured |

Battle reports do not reveal exact surviving enemy ship counts, exact remaining buildings, or stored resources beyond what the battle result itself exposes.

---

## Probes and Scouting

Probes cost **5 metal** and must be constructed by shipyards.

Probes behave like ships. They use the Scout decision, use discounted probe travel costs, and can be destroyed.

### Probe Travel Costs

| Scout Travel Type | Travel Time | Gas Cost |
|---|---:|---:|
| Same galaxy probe scout | 1 round | 2 gas per probe |
| Different galaxy probe scout | 2 rounds | 6 gas per probe |

### Probe Outcomes

| Target | Result |
|---|---|
| Empty planet | Probe reveals information and returns |
| Own controlled planet | Probe reveals information and returns |
| Enemy occupied planet | Probe reveals information, then is destroyed |
| Enemy colony under construction | Probe reveals information, then is destroyed |
| Destroyed galaxy | Cannot be probed |

A probe is destroyed **after** it successfully scans any enemy-controlled planet, including an occupied planet or a colony under construction.

### Simplified Probe Information

A probe reveals only:

| Category | Information Revealed |
|---|---|
| Planet stats | Size, metal abundance, gas abundance |
| Ownership | Empty, occupied, or colony under construction |
| Owner | Owner name, if controlled |
| Defence estimate | Approximate enemy combat strength |
| Megaproject | Present or absent |

Probes do not reveal exact enemy ship counts, exact building counts, stored resources, or exact construction details unless a future advanced rule allows it. They do reveal whether the planet is empty, occupied, or a colony under construction.

### Defence Estimate Categories

| Scan Result | Enemy Combat Power |
|---|---:|
| No defence detected | 0 |
| Light defence detected | 1-5 |
| Medium defence detected | 6-15 |
| Heavy defence detected | 16-30 |
| Massive defence detected | 31+ |

---

## Combat

Combat happens when a player attacks an enemy occupied planet or enemy colony under construction.

Combat is brutal and mostly simultaneous.

### Combat Participants

Attacking ships are the ships assigned to the Attack mission.

Defending ships are stationed ships at the target when the attack resolves.

Ships that arrived earlier in the same Movement and Mission Phase by Reinforce, Relocate, or successful Colonise missions count as stationed and may defend.

Returning fleets do not defend the target or their origin during the round in which they resolve.

### Combat Power

Attacker combat power comes from attacking ships.

| Attacking Ship | Attack Power |
|---|---:|
| Fighter | 1 |
| Destroyer | 4 |
| Cruiser | 0 |
| Probe | 0 |

Defender combat power comes from defending ships and the planet's current defence pool.

| Defender | Combat Power |
|---|---:|
| Fighter | 1 |
| Destroyer | 4 |
| Current defence pool | 1 per current defence point |
| Cruiser | 0 |
| Probe | 0 |

Cruisers and probes have 0 combat power.

They can be destroyed in combat, but they do not help win combat and do not increase winner losses.

### Rocket Launcher Defence Pool

Rocket launchers create a shared defence pool on each planet.

Each rocket launcher adds **4 maximum defence**.

Damage reduces the planet's **current defence**.

Damage does not destroy rocket launcher buildings by itself. Rocket launchers are destroyed only when the defending planet loses a battle, when the planet is devastated, or when the building is deconstructed or otherwise removed.

Current defence is used in combat.

Example:

| Rocket Launchers | Maximum Defence | Current Defence |
|---:|---:|---:|
| 1 | 4 | 4 |
| 2 | 8 | 8 |
| 2 after damage | 8 | 5 |

### Defence Pool Updates

When a rocket launcher finishes construction, the planet's maximum defence and current defence each increase by 4.

When a rocket launcher is deconstructed or otherwise removed, the planet's maximum defence decreases by 4. If current defence is higher than the new maximum defence, reduce current defence to the new maximum.

When a defender loses a battle, all rocket launchers are destroyed and the planet's maximum and current defence both become 0.

### Repair Defences

A planet may use its decision to repair a declared number of damaged defence points.

Repairing costs **8 metal per defence point restored**.

Repairs complete during the Project Phase, after arriving missions and attacks have resolved.

If the planet is captured or devastated before repairs complete, the repair is cancelled and the spent metal is not refunded.

If the planet's defence pool maximum is reduced before repairs complete, repairs can restore only up to the new maximum. Any paid repair that cannot be applied is lost.

A planet cannot repair above its maximum defence.

### Combat Resolution

1. Add the attacker's combat power.
2. Add the defender's combat power.
3. Higher combat power wins.
4. Defender wins ties.
5. The losing side's ships present in the battle are destroyed.
6. If the defender loses, all defensive buildings and defence points on the planet are destroyed.
7. The winning side suffers losses equal to the losing side's combat power.
8. Winner losses do not change who won.

### Losing Side

The losing side loses all ships present in the battle.

If the defender loses, all defensive buildings and defence points on the planet are destroyed.

### Winner Losses

The winning side suffers losses equal to:

```text
losing side's total combat power
```

The winning player chooses how to satisfy winner losses from eligible surviving ships and, for defending winners, defence pool damage.

Attacking winners may pay winner losses only with surviving attacking ships.

Defending winners may pay winner losses with surviving defending ships and/or defence pool damage.

Ships are destroyed as whole units and may overpay the required loss.

Defence pool damage is exact.

The winning player does not have to minimise overpayment.

Ships with 0 combat power may survive winner losses because destroying them contributes 0 toward the required loss.

If the winner does not have enough eligible combat power to fully satisfy winner losses, destroy all eligible positive-combat ships and apply as much defence pool damage as possible. The battle result still stands.

Example:

A defender wins and must suffer 3 combat power of losses. The defender may:

- Destroy 3 fighters.
- Destroy 1 destroyer, overpaying with 4 combat power.
- Apply 3 damage to the planet's defence pool.
- Use a mix of ships and defence damage.

### Combat Example: Attacker Wins

Defender has 1 rocket launcher with 4 current defence.

Attacker sends 5 fighters.

| Side | Combat Power |
|---|---:|
| Attacker | 5 |
| Defender | 4 |

The attacker wins.

The defender loses the rocket launcher.

The attacker suffers losses equal to the defender's combat power: **4**.

If the attack mode was Invade, the attacker loses 4 fighters and captures the planet with 1 fighter remaining. If the attack mode was Raid, the remaining fighter returns instead.

### Combat Example: Defender Wins a Tie

Defender has 1 rocket launcher with 4 current defence.

Attacker sends 4 fighters.

| Side | Combat Power |
|---|---:|
| Attacker | 4 |
| Defender | 4 |

The defender wins because defenders win ties.

The attacker loses all 4 fighters.

The defender suffers losses equal to the attacker's combat power: **4**.

The defender applies 4 damage to the defence pool, reducing current defence to 0, but keeps the planet. The rocket launcher remains as a damaged defensive building and can be repaired later.

### Battle Report Format

Use a compact report like this for players who participated in the battle:

```text
Battle Report: Andromeda-P4

Attacker: Player A
Defender: Player B
Attack mode: Invade

Attacker combat power: 9
Defender combat power: 6

Result: Attacker wins.
Defender losses: all defending ships, all rocket launchers, defence pool removed.
Attacker winner losses: 6 combat power.
Planet result: Captured by Player A.
Captured resources: 15 metal, 10 gas.
Destroyed resources: 16 metal, 10 gas.
Megaproject: none.
```

---

## Capturing and Devastating Planets

A player captures another player's occupied planet by sending an **Invade** attack, winning the battle, and having at least **1 surviving non-probe attacking ship** after winner losses are applied.

When an occupied planet is captured, its completed Hub is captured intact.

Winner losses do not reverse the battle result, but they can prevent an Invade attack from capturing if every non-probe attacking ship is destroyed.

### Capture Requirements

| Requirement |
|---|
| The attack mode is Invade |
| The target is an occupied planet with a completed Hub |
| The attacker wins the battle |
| Defending ships are destroyed |
| Defensive buildings are destroyed |
| At least 1 non-probe attacking ship survives winner losses |

A fleet with 0 combat power cannot capture an enemy planet by attacking.

If an occupied enemy planet has 0 combat power, any **Invade** fleet with at least 1 combat power captures it when the attack resolves, provided at least 1 non-probe attacking ship survives.

### Raid Results

If a Raid attack against an occupied planet wins, the defender loses all ships present, all defensive buildings, the defence pool, and any megaproject on the target.

Raid attacks never capture occupied planets and never destroy completed Hubs. If the target has a completed Hub, the original owner keeps the planet, its Hub, its remaining completed non-defensive normal buildings, normal buildings under construction, normal buildings being deconstructed, and stored resources.

A Raid that defeats a colony under construction destroys the incomplete Hub and empties the planet, as described in [Attacking Colonies Under Construction](#attacking-colonies-under-construction).

### Captured Planet Results

When a planet is captured:

| Asset | Result |
|---|---|
| Hub | Captured intact |
| Defending ships | Destroyed |
| Rocket launchers | Destroyed |
| Defence pool | Removed |
| Metal mines | Captured intact |
| Gas mines | Captured intact |
| Shipyards | Captured, but inactive for the next round |
| Normal buildings under construction | Destroyed |
| Normal buildings being deconstructed | Destroyed |
| Stored metal | 50% captured, 50% destroyed |
| Stored gas | 50% captured, 50% destroyed |
| Megaproject | Destroyed, never captured |

Captured shipyards cannot produce ships during the next round after capture. If a planet is captured during Round N, captured shipyards are inactive during Round N+1 and function normally starting Round N+2.

Round fractions down when splitting captured resources.

Example:

| Stored Resource | Amount Before Capture | Captured | Destroyed |
|---|---:|---:|---:|
| Metal | 31 | 15 | 16 |
| Gas | 20 | 10 | 10 |

### Devastated Planets

If an **Invade** attack wins against an occupied planet but no non-probe attacking ship survives winner losses, the target is devastated instead of captured.

When an occupied planet is devastated:

| Asset | Result |
|---|---|
| Hub | Destroyed |
| Defending ships | Destroyed |
| All normal buildings | Destroyed |
| Normal buildings under construction | Destroyed |
| Normal buildings being deconstructed | Destroyed |
| Stored metal and gas | Destroyed |
| Megaproject | Destroyed |
| Planet ownership | Removed |

A devastated planet becomes an empty planet and may be colonised later.

---
## Colonisation

An empty planet has:

| Property |
|---|
| No owner |
| No Hub |
| No normal buildings or megaprojects |
| No ships |
| No defences |
| No stored resources |
| Hidden or known planet stats depending on scouting |

To colonise an empty planet:

1. Send a cargo ship or fleet with enough cargo capacity to the empty planet.
2. The fleet must carry at least **10 metal** to start the Hub.
3. Spend 10 carried metal to start constructing a Hub.
4. Optionally spend 20 additional carried metal to start one Starter Building.
5. The Starter Building must be either a Metal mine or a Gas mine.
6. Any carried resources not spent on the Hub or Starter Building become stored on the colony.
7. The Hub takes **1 round** to complete.
8. A Starter Building also takes **1 round** to complete and completes at the same time as the Hub.
9. The Hub and Starter Building complete during the next Production Phase after colonisation resolves.
10. When the Hub is complete, the planet becomes occupied and active.

A lone cruiser can carry 30 resources, so it can start a Hub and one Starter Building by carrying 30 metal.

| Colony Package | Metal Needed |
|---|---:|
| Hub only | 10 |
| Hub + Metal mine Starter Building | 30 |
| Hub + Gas mine Starter Building | 30 |

Starter Buildings are optional. If a colony starts without a Starter Building, it becomes an Outpost when the Hub completes. An Outpost remains controlled and prevents elimination, but it does not count toward Dominance until it has at least one completed normal building.

Normal buildings and megaprojects cannot be started on a new colony until its Hub is complete, except for the optional Starter Building started by the Colonise mission.

A colony under construction counts as controlled for elimination and defence purposes, but it does not produce resources or provide a decision until its Hub is complete.

Colonising ships become stationed at the colony immediately. They may defend the colony against later attacks in the same Movement and Mission Phase. After the colony becomes active, those ships remain stationed at the new planet.

### Attacking Colonies Under Construction

A colony under construction can be attacked.

Colonies under construction are never captured intact. Defeating one destroys the incomplete Hub and the colony.

If the defender loses:

- Stationed defending ships are destroyed.
- The Hub under construction is destroyed.
- Any Starter Building under construction is destroyed.
- Stored resources on the colony are destroyed.
- The colony is destroyed.
- The planet becomes empty.
- Surviving attacking ships return, regardless of whether the attack was a Raid or Invade.

An attacker who wants to take the planet must later colonise it with a valid Colonise mission.

If the defender wins:

- The Hub remains under construction.
- Any Starter Building remains under construction.
- The colony remains controlled by the defender.
- Normal winner losses are applied.
- Construction continues normally.

---
## Megaprojects

Megaprojects are massive public projects.

| Megaproject | Purpose |
|---|---|
| Blackhole Generator | Destroys an entire galaxy |
| Research Facility | Reaches Singularity and wins the game |

### General Megaproject Rules

| Rule | Value |
|---|---:|
| Minimum planet size | 10 |
| Building slots required | 5 |
| Maximum active megaprojects per player | 1 |
| Can be built on captured planets | Yes, if the captured planet has a completed Hub |
| Counts against building limit | Yes |
| Requires a completed Hub | Yes |
| Requires a minimum number of planets | No, except Blackhole Generators require one completed Hub outside the project galaxy |
| Can be captured | No |
| Can be destroyed | Yes |
| Progress lost if destroyed | Yes |

A planet must be active and have a completed Hub plus at least **5 unused building slots** to start a megaproject.

A Blackhole Generator also requires the builder to control at least one completed Hub in a different galaxy from the project planet. Hubs under construction do not satisfy this requirement.

Those 5 slots are occupied immediately when the megaproject starts and remain occupied until the megaproject is completed, destroyed, or consumed by its own effect.

A player may only have **one active megaproject at a time**.

A megaproject stops counting as active when it is completed, destroyed, or consumed by its own effect.

Megaprojects are not normal buildings and do not make a planet occupied by themselves. A completed Hub is still required.

Megaproject countdowns are measured in rounds after the project is started. A megaproject started this round does not progress during the same round's Project Phase; its first countdown progress happens during the next round's Project Phase.

### Megaproject Restrictions

While a planet is building or operating a megaproject:

| Restriction | Rule |
|---|---|
| New defensive buildings | Cannot be started on that planet |
| New non-defensive normal buildings | Cannot be started on that planet |
| Ship production | Cannot be started on that planet |
| Reinforcements | Allowed |
| Existing defences | Still function |
| Resource production | Still functions |
| Repairs | Allowed |
| Deconstruction | Allowed for normal buildings; the Hub cannot be voluntarily deconstructed |
| Transport missions | Allowed |
| Scout missions | Allowed |

A player should prepare the planet before starting a megaproject.

### Destroying a Megaproject

A megaproject is destroyed if the project planet loses a battle.

When that happens:

| Result |
|---|
| The megaproject is destroyed |
| All megaproject progress is lost |
| Defensive buildings are destroyed |
| Defending ships are destroyed |
| If the attack was a Raid, the original owner keeps the planet and its completed Hub |
| If the attack was an Invade, the attacker may capture or devastate the planet depending on surviving ships |

A megaproject is never captured intact.

---
## Blackhole Generator

The **Blackhole Generator** is a late-game conquest weapon.

It does not directly win the game, but it can destroy entire galaxies and eliminate players.

### Blackhole Generator Stats

| Requirement | Value |
|---|---:|
| Metal cost | 450 metal |
| Gas cost | 350 gas |
| Building slots | 5 |
| Construction time | 9 rounds |
| Outside-Hub requirement | Builder must control at least 1 completed Hub in a different galaxy |
| Minimum planet size | 10 |
| Requires completed Hub | Yes |
| Active limit | 1 megaproject per player |

The resources must be stored on the planet where the Blackhole Generator is started.

The planet must have a completed Hub and 5 unused building slots when the Blackhole Generator is started. The builder must also control at least one completed Hub in a different galaxy from the Blackhole Generator's galaxy.

### Blackhole Generator Effect

When construction completes, the entire galaxy containing the generator is destroyed.

This includes:

| Destroyed |
|---|
| All planets in that galaxy |
| All Hubs and normal buildings in that galaxy |
| All stationed ships in that galaxy |
| Ships travelling to that galaxy |
| Ships travelling from that galaxy |
| All stored metal and gas in that galaxy |
| All colonies under construction in that galaxy, including incomplete Hubs |
| The Blackhole Generator itself |

The galaxy becomes permanently uninhabitable.

No player can travel to, colonise, probe, or occupy that galaxy again.

The player who built the Blackhole Generator is not immune. Their own planets in that galaxy are destroyed too.

### Blackhole Generator Timeline

| Stage | Remaining Time | Public Information |
|---|---:|---|
| Construction begins | 9 rounds | Galaxy revealed |
| Midpoint warning | 5 rounds | Exact planet revealed |
| Final warning | 2 rounds | Final same-galaxy intervention window |
| Activation | 0 rounds | Galaxy destroyed |

The final warning is issued at 2 rounds remaining because a same-galaxy attack launched in the next Orders Phase can still arrive before activation. New intergalactic attacks launched after the final warning normally cannot arrive in time.

### Blackhole Generator Public Warnings

When a Blackhole Generator begins construction, the galaxy is publicly announced.

The exact planet is not immediately revealed unless discovered by probing.

#### Start Message

```text
Space-time disturbances emanate from Andromeda...
```

#### Halfway Message

When 5 rounds remain, the exact planet becomes public.

```text
A collapsing gravitational anomaly intensifies on Andromeda-P7...
```

#### Final Warning

When 2 rounds remain:

```text
Andromeda has begun gravitational collapse. Final same-galaxy intervention window detected.
```

#### Activation Message

When the Blackhole Generator completes:

```text
Andromeda is consumed by a black hole.
```

---
## Research Facility and Singularity

The **Research Facility** is the Singularity win-condition megaproject.

It represents a player training a self-improving artificial intelligence.

### Research Facility Stats

| Requirement | Value |
|---|---:|
| Metal cost | 450 metal |
| Gas cost | 450 gas |
| Building slots | 5 |
| Construction time | 10 rounds |
| Minimum planet size | 10 |
| Requires completed Hub | Yes |
| Active limit | 1 megaproject per player |

The resources must be stored on the planet where the Research Facility is started.

The planet must have a completed Hub and 5 unused building slots when the Research Facility is started.

When the 10-round countdown completes, Singularity is reached and that player wins immediately during the Victory Phase.

### Research Facility Timeline

| Stage | Remaining Time | Public Information |
|---|---:|---|
| Project begins | 10 rounds | Galaxy revealed |
| Midpoint warning | 5 rounds | Exact planet revealed |
| Final warning | 2 rounds | Final same-galaxy intervention window |
| Singularity | 0 rounds | Player wins |

The final warning is issued at 2 rounds remaining because a same-galaxy attack launched in the next Orders Phase can still arrive before Singularity.

### Research Facility Public Warnings

When a Research Facility begins, the galaxy is publicly announced.

The exact planet is hidden until discovered by probing or until the midpoint warning.

#### Start Message

```text
Ominous electromagnetic activity rouses from Triangulum...
```

#### Halfway Message

When 5 rounds remain, the exact planet becomes public.

```text
Self-improving machine intelligence signals intensify on Triangulum-P4...
```

#### Final Warning

When 2 rounds remain:

```text
The Singularity threshold is approaching on Triangulum-P4. Final same-galaxy intervention window detected.
```

#### Completion Message

When the Research Facility completes:

```text
The Singularity has been reached. Player X wins.
```

---
## Destroyed Galaxies

When a galaxy is destroyed:

| Asset | Result |
|---|---|
| Planets | Removed from the game |
| Hubs | Destroyed |
| Normal buildings | Destroyed |
| Defensive buildings | Destroyed |
| Ships stationed there | Destroyed |
| Ships travelling to that galaxy | Destroyed |
| Ships travelling from that galaxy | Destroyed |
| Stored resources | Destroyed |
| Colonies under construction and incomplete Hubs | Destroyed |
| Megaprojects | Destroyed |

A destroyed galaxy cannot be used again.

If a player's last controlled planet is destroyed by a Blackhole Generator, that player is eliminated during the Victory Phase.

If multiple Blackhole Generators activate in the same round, their galaxy-destruction effects are simultaneous.

If no players control any completed Hub or Hub under construction after simultaneous Blackhole effects resolve, the game ends in mutual destruction with no winner.

---
## Megaproject Visibility and Timing

Megaproject information is handled through fog of war.

| Stage | Public Information |
|---|---|
| Project starts | Galaxy is public |
| Before midpoint | Exact planet is hidden unless probed |
| Midpoint reached | Exact planet becomes public |
| 2 rounds remaining | Final same-galaxy intervention warning is public |
| Completion | Result is public |

A probe that scans the exact project planet reveals the megaproject immediately, even before the midpoint message.

If that planet is controlled by an enemy, the probe is destroyed after the scan.

### Megaproject Completion Priority

At the end of the round, resolve megaprojects in this order:

1. Blackhole Generator and Research Facility countdowns progress during the Project Phase.
2. Public warnings are issued when countdown thresholds are reached.
3. During the Victory Phase, check whether any Research Facility has completed its countdown and reached Singularity.
4. If Singularity is reached, the game ends immediately.
5. If no Singularity victory occurs, completed Blackhole Generators activate simultaneously.
6. Check eliminations and Conquest victory after Blackhole effects resolve.
7. If no Conquest victory occurs, check Dominance progress and Dominance victory.

If multiple players reach Singularity in the same round, they share victory.

If a Research Facility and a Blackhole Generator both complete in the same round, Singularity is checked first.

### Example Research Facility Timeline

For a Research Facility started in Round 12:

| Round | Event |
|---:|---|
| 12 | Project started at 10 remaining; no progress this Project Phase |
| 13 | Countdown becomes 9 |
| 14 | Countdown becomes 8 |
| 15 | Countdown becomes 7 |
| 16 | Countdown becomes 6 |
| 17 | Countdown becomes 5; exact planet revealed |
| 18 | Countdown becomes 4 |
| 19 | Countdown becomes 3 |
| 20 | Countdown becomes 2; final same-galaxy intervention warning |
| 21 | Countdown becomes 1 |
| 22 | Countdown becomes 0; Singularity victory checked during Victory Phase |

---

## Round Structure

Each round has 5 phases.

### 1. Production Phase

- Active planets produce resources.
- Hub construction and normal-building construction progress by 1 round.
- A Starter Building created by colonisation progresses with the Hub and completes at the same time as the Hub. If the Starter Building is a mine, it does not produce until the next Production Phase because resource production has already happened this phase.
- Deconstruction progresses and any completed deconstruction removes the normal building.
- Normal buildings being deconstructed still function until they are removed, so mines being removed produce one final time this phase.
- Completed normal buildings become active after construction progress resolves.
- If the Hub on a colony finishes, that colony becomes an occupied active planet. It does not produce resources until the next Production Phase, but it does provide a decision during this round's Orders Phase.

### 2. Orders Phase

- Each player has 1 minute to submit orders.
- Each active planet may make 1 decision.
- Planets without submitted decisions take no action.
- Players may submit Attack and Colonise orders based on last known information.

### 3. Movement and Mission Phase

Resolve this phase in the following order:

1. Validate orders and pay costs for new normal buildings, ships, missions, repairs, and megaprojects.
2. Complete ship production ordered this round.
3. Launch new missions.
4. Resolve missions whose travel countdowns have expired.
5. Immediately apply each mission's specific behaviour, such as Raid, Invade, Deliver, Relocate, Reinforce, or Colonise.
6. At the end of the phase, complete returns for returning fleets whose origins are still controlled by their owners.

Newly launched missions do not resolve until their listed travel time has passed.

Newly produced ships may defend this round, but they cannot be sent on missions until a later round.

Resources delivered this phase cannot be spent until the next round.

Returning fleets do not defend either the mission target or their origin during this phase.

### 4. Project Phase

- Repairs ordered this round complete if the planet is still controlled by the repairing player and was not captured or devastated after the repair was ordered.
- Repairs can restore only up to the planet's current maximum defence.
- Megaproject countdowns progress.
- Public warnings are issued if thresholds are reached.

### 5. Victory Phase

- Check Singularity.
- Resolve completed Blackhole Generators if no Singularity victory occurred.
- Check eliminations and Conquest.
- If no Conquest victory occurs, check Dominance.

---
## Simultaneous Mission Resolution

If multiple missions arrive at the same planet during the same round, resolve them in this order:

1. Scout missions
2. Reinforce missions from the current owner
3. Transport missions from the current owner
4. Colonisation missions
5. Attack missions

There is no separate post-mission behaviour step. Each mission applies its specific behaviour immediately when it resolves.

If several missions in the same category arrive at the same planet in the same round, resolve them in random order unless players agree to use another initiative system.

If multiple players attempt to colonise the same empty planet in the same round, resolve those Colonise missions in random order. The first successful Colonise mission starts the Hub and creates the colony; later Colonise missions to that planet fail and return with their cargo because the planet is no longer empty.

An attack mission resolves if the target is enemy-controlled when the attack arrives. If the target changed owner after the attack was launched, the attack resolves against the new owner as long as that owner is still an enemy of the attacker.

If the target is empty, destroyed, or controlled by the attacker when the attack arrives, the attacking fleet returns without combat.

If multiple players attack the same planet in the same round, resolve attacks in random order unless players agree to use another initiative system.

After each colonisation, attack, capture, devastation, or colony destruction, immediately update planet control before resolving the next mission targeting that planet.

Player elimination is not checked during mission resolution. It is checked only during the Victory Phase.

---
## Win Conditions

The game has three win conditions.

### Conquest

A player wins by Conquest when all other players are eliminated and the winning player still controls at least one completed Hub or Hub under construction.

Elimination is checked only during the Victory Phase.

A player is eliminated when they control:

| Controlled Asset | Required Amount for Elimination |
|---|---:|
| Completed Hubs | 0 |
| Hubs under construction | 0 |

Travelling fleets do not prevent elimination.

When a player is eliminated, all of their stationed ships, travelling fleets, cargo, stored resources, colonies, Hubs, construction, deconstruction, normal buildings, and megaprojects are removed from the game.

If all remaining players are eliminated simultaneously, the game ends in mutual destruction with no winner.

### Singularity

A player wins by Singularity when their Research Facility completes its 10-round countdown.

The galaxy is publicly announced when the project begins.

The exact planet becomes public at the midpoint warning or earlier if discovered by probing.

If multiple players reach Singularity in the same round, they share victory.

Singularity is checked before completed Blackhole Generators activate in the same round.

### Dominance

A player wins by Dominance if they control at least **60% of all Developed Hubs** for **3 consecutive Victory Phases**.

A Developed Hub is a completed Hub on a planet with at least one completed normal building.

Outposts do not count toward Dominance. An Outpost still counts as controlled and still prevents elimination, but it does not help satisfy the Dominance threshold until the planet has at least one completed normal building.

Dominance is checked during the Victory Phase after Singularity, Blackhole activation, and Conquest checks.

If the number of Developed Hubs changes, recalculate the 60% threshold at that Victory Phase. Round the required number up. Dominance cannot be won unless at least one Developed Hub exists.

Example:

| Developed Hubs in Game | 60% Threshold | Required Hubs for Dominance |
|---:|---:|---:|
| 7 | 4.2 | 5 |
| 10 | 6 | 6 |
| 13 | 7.8 | 8 |

A player must satisfy the threshold for 3 consecutive Victory Phases. If they fall below the threshold, their Dominance count resets to 0. Dominance progress announcements are public, but they do not reveal the exact locations of hidden Hubs.

---
## Example Round Orders

Example orders using real galaxy names and planet numbers:

```text
Round 6 orders:

- Milky Way-P3: Build gas mine.
- Milky Way-P7: Produce 2 fighters, if it has at least 2 shipyards.
- Andromeda-P2: Send 1 probe to Andromeda-P5.
- Triangulum-P1: Reinforce Triangulum-P4 with 3 fighters.
- Large Magellanic Cloud-P6: Start Research Facility.
```

Short code version:

```text
Round 6 orders:

- MW-P3: Build gas mine.
- MW-P7: Produce 2 fighters, if it has at least 2 shipyards.
- AND-P2: Send 1 probe to AND-P5.
- TRI-P1: Reinforce TRI-P4 with 3 fighters.
- LMC-P6: Start Research Facility.
```

---

## Full Quick Reference

### Map

| Players | Galaxies Used | Planets per Galaxy | Total Planets | Planets per Player |
|---:|---|---:|---:|---:|
| 2 | Milky Way, Andromeda, Triangulum | 5 | 15 | 7.5 |
| 3 | Add Large Magellanic Cloud | 5 | 20 | 6.7 |
| 4 | Add Small Magellanic Cloud | 6 | 30 | 7.5 |
| 5-6 | Add Whirlpool and Sombrero | 6 | 42 | 7-8.4 |
| 7-8 | Add Pinwheel | 7 | 56 | 7-8 |
| 9-10 | Add Bode's Galaxy and Cigar Galaxy | 7 | 70 | 7-7.8 |

### Starting Setup

| Starting Asset | Value |
|---|---:|
| Starting metal | 40 |
| Starting gas | 40 |
| Starting Hub | 1 completed |
| Starting metal mines | 1 |
| Starting gas mines | 1 |
| Starting shipyards | 1 |
| Starting rocket launchers | 1 |
| Starting planet size | 10 |
| Starting metal abundance | 5 |
| Starting gas abundance | 5 |

### Core Structures, Buildings, and Megaprojects

| Structure, Building, or Project | Cost | Build Time | Slots Used | Effect |
|---|---:|---:|---:|---|
| Hub | 10 metal | 1 round | 0 | Required for occupation and active planet status |
| Metal mine | 20 metal | 2 rounds | 1 | Produces metal × abundance |
| Gas mine | 20 metal | 2 rounds | 1 | Produces gas × abundance |
| Shipyard | 30 metal | 2 rounds | 1 | Builds 1 ship per round |
| Rocket launcher | 40 metal | 2 rounds | 1 | Adds 4 maximum defence |
| Blackhole Generator | 450 metal, 350 gas | 9 rounds | 5 | Destroys its galaxy |
| Research Facility | 450 metal, 450 gas | 10 rounds | 5 | Wins by Singularity |

Normal buildings and megaprojects count against planet size as soon as they are started. Hubs do not count against planet size. Megaprojects require 5 unused slots and a completed Hub. A Blackhole Generator also requires the builder to control at least one completed Hub in a different galaxy.

### Ships

| Ship | Cost | Attack | Cargo | Role |
|---|---:|---:|---:|---|
| Probe | 5 metal | 0 | 0 | Scouting |
| Fighter | 10 metal | 1 | 0 | Cheap combat |
| Cruiser | 20 metal | 0 | 30 | Transport and colonisation |
| Destroyer | 50 metal | 4 | 0 | Heavy combat |

### Travel

| Travel Type | Gas Cost | Time |
|---|---:|---:|
| Same galaxy | 4 gas per ship | 1 round |
| Different galaxy | 12 gas per ship | 2 rounds |
| Same galaxy probe scout | 2 gas per probe | 1 round |
| Different galaxy probe scout | 6 gas per probe | 2 rounds |

Returning fleets become available at the start of the round after their mission resolves. Returning fleets do not defend during the round in which they resolve.

### Combat

| Rule | Value |
|---|---|
| Defender wins ties | Yes |
| Losing side loses all ships present | Yes |
| Losing defender loses defensive buildings | Yes |
| Winner losses | Equal to loser combat power; winner chooses eligible losses |
| Rocket launcher defence | 4 maximum defence each |
| Repair cost | 8 metal per defence point |
| Raid ownership removal | Occupied planets: never; colonies under construction: destroyed if defender loses |
| Capture requirement | Invade attacker must target an occupied planet and have at least 1 surviving non-probe ship |

### Mission Behaviour

| Mission | Behaviour |
|---|---|
| Scout | Probe returns from empty/own planets; destroyed after enemy-controlled scans |
| Raid | Attack, then surviving ships return without capturing; completed Hubs survive |
| Invade | Attack, then surviving ships stay if the target is captured; otherwise they return |
| Deliver | Transport cargo, then ships return and do not defend at the destination |
| Relocate | Transport cargo, then ships stay and may defend later that phase |
| Reinforce | Ships move to owned planet, stay, and may defend later that phase |
| Colonise | Cargo ships spend 10 metal to start a Hub; may spend 20 more metal on one Metal mine or Gas mine Starter Building; then remain stationed there |

Cargo may be carried only on Transport and Colonise missions.

### Megaprojects

| Project | Cost | Slots | Time | Public Reveal | Effect |
|---|---:|---:|---:|---|---|
| Blackhole Generator | 450 metal, 350 gas | 5 | 9 rounds | Galaxy at start, planet at 5 rounds, final warning at 2 rounds | Destroys its galaxy; requires another completed Hub outside the target galaxy |
| Research Facility | 450 metal, 450 gas | 5 | 10 rounds | Galaxy at start, planet at 5 rounds, final warning at 2 rounds | Wins by Singularity |

Megaprojects require a completed Hub and 5 unused slots.

Final warnings are issued at 2 rounds remaining, so same-galaxy attacks launched in the next Orders Phase can still arrive before completion.

### Victory and Elimination

| Rule | Value |
|---|---|
| Elimination timing | Victory Phase only |
| Elimination condition | 0 completed Hubs and 0 Hubs under construction |
| Travelling fleets prevent elimination | No |
| Simultaneous total elimination | Mutual destruction; no winner |
| Singularity priority | Checked before Blackhole activation in the same round |
| Multiple Singularity completions | Shared victory |
| Dominance victory | Control at least 60% of Developed Hubs for 3 consecutive Victory Phases |
| Outposts and Dominance | Bare Hubs prevent elimination but do not count toward Dominance |

---
## Design Notes

The current design emphasizes:

- Real galaxy names for a more evocative map.
- Fast decisions through a one-minute round timer.
- Strategic commitment through one decision per active planet.
- Clear planetary ownership through Hubs as core structures.
- Local logistics through planet-based resource storage.
- Unlimited stationed fleets to reduce bookkeeping.
- Uncertainty through fog of war.
- Affordable scouting through discounted probe travel, balanced by probes being destroyed after enemy scans.
- Mission-specific movement instead of a separate fleet stance system.
- Brutal combat where even the winner suffers full attrition from the loser.
- Dramatic endgames through public megaproject countdowns.
- Three clear victory paths: military Conquest, territorial Dominance, and technological Singularity.
