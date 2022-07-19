---
layout: default
title: Server Specific
parent: Mods
---

# Server Specific Mods
{: .no_toc }

Mods which are specific to server profiles.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Performance

### AI Improvements

---

### Clumps

---

### FastFurnace

---

### FastSuite

---

### FastWorkbench

---

### Get It Together, Drops!

---

### Krypton Reforged

---

### Observable

---

### Radium Reforged

#### About

Radium Reforged is an Unofficial Fork of CaffeineMC's "Lithium", made to work with Forge Mod Loader. It's a general-purpose optimization mod for Minecraft which works to improve a number of systems (game physics, mob AI, block ticking, etc) without changing any behavior. It works on both the client and server, and can be installed on servers without requiring clients to also have the mod. With the mod installed, you can see on average a 45% improvement to server tick times, resulting in a much leaner game.

Even in single-player, your game runs an "integrated server" which ticks the world your player is in. Through optimizing the server-side of the game, this can free up your computer's processor to focus on other tasks, resulting in improved frame rates and responsiveness. For multiplayer servers, administrators can expect a sizeable improvement to tick times, allowing their hardware to support more loaded entities, chunks, and players.

<div class="code-example" markdown="1">

#### Physics Optimizations

Entity collision detection has seen significant improvements through reducing the collision resolution complexity for simple, cuboid blocks. A more accurate algorithm is also used to reduce the number of blocks being checked every tick, especially in cases where entities are moving very quickly.

</div>

<div class="code-example" markdown="1">

#### Mob AI optimizations

We make use of an event-based system for some tasks in order to reduce the CPU usage incurred by constantly polling the world for changes. Mob "brains" have also been optimized to select between different AI tasks much, much quicker than before. Comparison before and after here.

</div>

<div class="code-example" markdown="1">

#### World generation optimizations

Many calculations in vanilla's world generation are unnecessary and do not affect the final result, which gives ample opportunity for Lithium to optimize this overhead away.

</div>

<div class="code-example" markdown="1">

#### Chunk loading optimizations

The temporary data structures used in block palette compaction have been changed to be much more efficient. This results in fewer TPS drops while players are exploring terrain and provides a modest boost to world load times. We also batch some verification operations to reduce unnecessary disk I/O.

</div>

<div class="code-example" markdown="1">

#### Mob farm optimizations

Mob cramming is significantly less expensive as resolving collisions between entities has been optimized to take advantage of the fact that simple boxes are involved. This makes mob farms considerably less harmful for server tick rates.

</div>

<div class="code-example" markdown="1">

#### Block ticking optimizations

Less overhead, making things such as block update settling after generating chunks and other Redstone contraptions faster. This also reduces the amount of time it takes for a block to determine if it is ticking by schedule from O(n), where n is the number of ticking blocks, to O(1), providing a significant speedup when many blocks are being ticked.

</div>

<div class="code-example" markdown="1">

#### Explosion optimizations

Many optimizations have been applied to TNT and explosions alike, reducing their associated lag without changing how they behave. In particular, ray-tracing is optimized to take advantage of the fact that multiple steps through a way will occur in the same block position, allowing us to quickly re-use the previous step's results. We also make use of a faster position tracking algorithm which avoids many excessive allocations.

</div>

<div class="code-example" markdown="1">

#### Point of Interest optimizations

Complex mob AIs in Minecraft, primarily those belonging to Villagers and Pillagers, often need to find relevant points of interest in the world in order to choose the most appropriate AI task. In vanilla, querying all points within a chunk requires 16 separate retrievals through stream-heavy code. With Lithium present, this task is reduced to a single simple retrieval that makes use of a much faster (and traditional) iterator based approach, yielding anywhere from a 16-22x improvement for queries.

</div>

<div class="code-example" markdown="1">

#### Data Tracker optimizations

The internal data manager used for tracking some entity state and properties has been optimized to use flat arrays and avoid expensive locking, providing a decent boost whenever these attributes are accessed during a game tick.

</div>

<div class="code-example" markdown="1">

#### Redstone Wire optimizations

Calculating the new power level of redstone wire after a block update is costly. Reducing the number of blockstate checks without any change in behavior reduces redstone dust lag by about 35%.

</div>

---

### Starlight

Starlight is a Forge mod for rewriting the light engine to fix lighting performance and lighting errors. 

Starlight can be installed either on the dedicated server or client. It is not required to be installed on both sides. If you have Starlight on the server, clients can use Vanilla/Starlight to connect. Likewise, if you have Starlight on the client, you can connect to Vanilla/Starlight servers.

Browsing through [Starlight's Issue Tracker](https://github.com/PaperMC/Starlight/issues) will show further mod incompatibilities. Starlight is a rather destructive light engine rewrite, so it should be expected to break mods more often.

Starlight was developed for higher scale dedicated servers, as they suffered performance problems due to how ungodly slow the light engine was. The only solution was to create an extremely invasive mod which rewrote the entire light engine. I ported the mod to fabric so that I can update it during snapshots, and decided that publishing it for all users, especially client users, would be beneficial. However, it does have the downside of being an invasive mod: Being invasive didn't affect higher scale servers because they run on Bukkit.

Further reading on the technical details of how Starlight achieves its performance can be read here: [TECHNICAL_DETAILS.md](https://github.com/PaperMC/Starlight/blob/fabric/TECHNICAL_DETAILS.md)