# Technical Implementation

## How Actors Are Managed

- Dekaron's protocol treats NPCs and PCs as the same actor entity
- When an actor is rendered into your client, its name and other attributes are assigned
- When any action involves an actor which has not yet been discovered, it will be buffered as an "Unknown Actor" entity. Sadly this happens quite often due to Dekaron's tiny render distance.
- Walking out of render distance and loading the actor back into your client migrates the entity and updates all instances referencing it

## How Actions Are Managed

- Dekaron's protocol does not provide skill references for damage instances
- It does not provide hp/mp/shield offset values, it only updates the actor's current value
(This makes exact heal values impossible. They could still be calculated but the values would be inaccurate due to regeneration or infrequent updates)
- It does not provide source actors for effect instances
- Generally, it does not provide various fields which then have to be omitted (like target's hp/shield after a missed hit, etc.)

## How Actions Reference Skills

- Every actor has its current animation state and animation type tracked
- Whenever an actor starts performing an action, the animation state for the entity will be updated to represent that action's animation
- All damage instances occurring after this animation state will be assigned to represent the referenced skill
- Limitation: if any lingering damage effect is used (think of Segnale's curse field) and the animation state of the actor is afterwards updated to anything else like an auto attack, all following curse field instances will be assigned to be auto attacks.
(This could be partially avoided through applying heuristics on the damage values, but this is too convoluted and not precise)

## How Auto-Detection Is Managed

- Dekaron's protocol does not contain a protocol version value (at least none that I could find)
- Protocol version is determined through distinguished packet structures between A9 and A40
- Different client connections are determined through the port
- New server connections are determined in multiple ways through certain patterns within TCP packets
- After a valid connection is identified, the network listener is restarted and limited to that IP
- If your client is forwarded to a different server/channel (like DKS) through an expected packet, your network listener is reset to that IP
- Changing servers/channels or relogging assigns your client a new actorId, resulting in a new actor appearing in the UI. Your former actor is renamed to visualize the difference

## Development Methodology

DekaDux was developed through binary disassembly and manual static/dynamic protocol analysis, supported through the in-app Traffic Analyzer. All names and structures within DekaDux are not guaranteed to be exact replications of the original sources, but instead educated guesses. Be aware of this when considering the OpCode names—some lesser researched ones are very rough estimates.\
I'm aware of a client being around containing debug symbols baked in - this was not (yet) used for development.