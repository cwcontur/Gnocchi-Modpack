---
layout: default
title: Server Specific
parent: Mods
---

# Server Specific Mods
{: .no_toc }

Mods which are specific to server profiles.
{: .fs-6 .fw-300 }

<details markdown="block">
  <summary>
    Table of Contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

---

# Performance

## AI Improvements

Simplified AI modification mod focused on performance and low-level modifications to AIs in the game. Picking up the slack for the base game and improving it for a modded ecosystem. Handling common problems such as too many animals, performance hits from swarms of zombies, and simple remove tasks skipped by larger AI improvement mods.

---

## Clumps

Clumps groups XP orbs together into a single entity to reduce lag when there are many in a small area. On top of this, it also makes the player immediately collect the orbs once they touch the player, so you are not stuck with a bunch of orbs in your face.

---

## FastFurnace

FastFurnace utilizes mixins to edit the functionality of the Furnace, Blast Furnace, and Smoker, improving their TPS performance (not smelting speed!)

Similar to FastWorkbench, it caches the last recipe used, and checks this recipe first before re-scanning the entire registry.  This is significantly faster due to the vanilla furnace scanning the entire furnace registry each tick, which may be fine for vanilla, but in a modded environment, gets very large very quickly.

These changes apply to the Furnace, Blast Furnace, and Smoker.  Any mod utilizing AbstractFurnaceTileEntity will also receive the benefits of having this mod installed.

---

## FastSuite

Similar to the projects FastWorkbench and FastFurnace, FastSuite is a mod about improving recipe performance.  However, unlike those two mods, it improves upon all mods that use the JSON recipe system, rather than just a specific subset of recipes.  It does this by turning the list of recipes from a Set into a LinkedList.  This list is then able to be reordered when a recipe is accessed, making accesses to it in the future much faster.  Recipes that are close enough to the front of the list (that are within the "cache size") are not moved to avoid churning.  The cache size is configurable, and each type of recipe has it's own cache space.

On the first access to a recipe, FastSuite will have identical performance to vanilla.  However, past that first access, the time spent to access a recipe will decrease.  This decrease can be substantial depending how far back in the list the recipe originally was.  The impact is also more dramatic depending on how many recipes are loaded into the game, as then there is a greater range for movement of recipes.  Below, we can see the performance improvements across access times to a few recipes, along with their index in the original recipe list order.  The following series of 6 tables is organized as such:
The leftmost column states the recipe, it's original index in the recipe list, and the current trial.  The next two columns compare FS/Vanilla recipe seek times in microseconds.  The default Cache Size is 100, and is applied here.  This means that entries that are not more than index 100 are not moved.

There is a dramatic change in recipes that are normally found towards the end of the recipe list, as seen in Acacia Planks.  Recipes that are already towards the front of the list, such as Iron or Gold Nuggets, see minimal or no improvements.  As such, we can see that there is no harm in applying the benefits that FastSuite provides, as it has exceptional performance benefits when it is useful (>95% improvement on acacia planks), and no impact when it would otherwise provide no benefit (as seen in the case of attempting a Failure match).  We actually see slight detriments in Iron and Gold nuggets as they were within the Cache Size, and were actually pushed back by the operation of caching Acacia Planks, Sticks, and Crafting Tables.  However, there is little to no performance lost due to that, especially not as compared to the benefit from caching the later recipes.

---

## FastWorkbench

This is a mod aimed at improving performance of all crafting-related functions.  It fixes the bug introduced in *Minecraft* 1.12 where shift-click crafting a stack of items could cause momentary freezes.  However, it does slightly more than just fixing that issue.

FastWorkbench causes all crafting operations to cache the last recipe used.  On top of this, it reduces calls to that cached recipe, by only detecting changes when the stored item in the crafting matrix actually changes (vanilla retries every time anything changes, such as stack size).  This results in the number of matching operations being reduced to one, instead of anywhere between one and nearly 600.

Back in 1.12, FastWorkbench fully removed the recipe book, which meant recipes were no longer forcibly synced on login so that the client could see them in the book.  This resulted in a huge boost in login times. In 1.13 and higher, the recipes are synced anyway as part of the new recipe system. In these versions, FastWorkbench visually removes the recipe book button by default, but it can be configured back on.

---

## FerriteCore

This mod reduces the memory usage of *Minecraft* in a few different ways. A high-level technical description of the changes is available [here](https://github.com/malte0811/FerriteCore/blob/main/summary.md).

---

## Get It Together, Drops!

This mod adds two configuration options to control how dropped items combine on the ground. This can significantly improve performance in areas with lots of dropped items, like explosion craters or farms. In 1.15+, these config settings can be found in the serverconfig folder of your world's folder.

**radius** - This is a value from 0.5 to 500 and defines the size of the area in which a dropped item will search for other dropped items to combine with. Example: Setting this to 5.0 will search in an area of 5 blocks (in all directions) around the dropped item. "0.5" is vanilla behavior. Do note, that this behavior does not take walls into account.

**checkY** - Set this to true if you want dropped items to also check above and below them, set to false if not. "false" is vanilla behavior.

You can also tell the mod to ignore certain items by creating a datapack and adding the items you want ignored to the **getittogetherdrops:ignored** item tag. This will result in items in the tag not merging at all.

---

## Krypton Reforged

Krypton (from Ancient Greek kryptos, "the hidden one") optimizes the *Minecraft* networking stack, meaning it mostly improves server performance with lots of clients, but is also required on the client.

Krypton contains several optimizations, including:

- **Highly optimized Netty handlers** derived from the Velocity proxy, which I am the developer of. These handlers have sen real-world usage and extensive profiling, and strategically deploy native code where it makes the most sense.
- **Flush consolidation** to lower server CPU usage (and reducing the impact from hardware security vulnerabilities which exploit speculative execution) and lower server tick times.
- **Micro-optimizations** to reduce memory usage and improve packet serialization speeds.

---

## Observable

A spiritual successor to LagGoggles for *Minecraft* 1.16+, Observable profiles (tile) entities and shows you what's taking up tick time and where. Forge and Fabric compatible. (Note: default keybind to open profiler GUI is r.)

---

## Radium Reforged

Radium Reforged is an Unofficial Fork of CaffeineMC's "Lithium", made to work with Forge Mod Loader. It's a general-purpose optimization mod for *Minecraft* which works to improve a number of systems (game physics, mob AI, block ticking, etc) without changing any behavior. It works on both the client and server, and can be installed on servers without requiring clients to also have the mod. With the mod installed, you can see on average a 45% improvement to server tick times, resulting in a much leaner game.

Even in single-player, your game runs an "integrated server" which ticks the world your player is in. Through optimizing the server-side of the game, this can free up your computer's processor to focus on other tasks, resulting in improved frame rates and responsiveness. For multiplayer servers, administrators can expect a sizeable improvement to tick times, allowing their hardware to support more loaded entities, chunks, and players.

<div class="code-example" markdown="1">

### Physics Optimizations

Entity collision detection has seen significant improvements through reducing the collision resolution complexity for simple, cuboid blocks. A more accurate algorithm is also used to reduce the number of blocks being checked every tick, especially in cases where entities are moving very quickly.

</div>

<div class="code-example" markdown="1">

### Mob AI optimizations

We make use of an event-based system for some tasks in order to reduce the CPU usage incurred by constantly polling the world for changes. Mob "brains" have also been optimized to select between different AI tasks much, much quicker than before. Comparison before and after here.

</div>

<div class="code-example" markdown="1">

### World generation optimizations

Many calculations in vanilla's world generation are unnecessary and do not affect the final result, which gives ample opportunity for Lithium to optimize this overhead away.

</div>

<div class="code-example" markdown="1">

### Chunk loading optimizations

The temporary data structures used in block palette compaction have been changed to be much more efficient. This results in fewer TPS drops while players are exploring terrain and provides a modest boost to world load times. We also batch some verification operations to reduce unnecessary disk I/O.

</div>

<div class="code-example" markdown="1">

### Mob farm optimizations

Mob cramming is significantly less expensive as resolving collisions between entities has been optimized to take advantage of the fact that simple boxes are involved. This makes mob farms considerably less harmful for server tick rates.

</div>

<div class="code-example" markdown="1">

### Block ticking optimizations

Less overhead, making things such as block update settling after generating chunks and other Redstone contraptions faster. This also reduces the amount of time it takes for a block to determine if it is ticking by schedule from O(n), where n is the number of ticking blocks, to O(1), providing a significant speedup when many blocks are being ticked.

</div>

<div class="code-example" markdown="1">

### Explosion optimizations

Many optimizations have been applied to TNT and explosions alike, reducing their associated lag without changing how they behave. In particular, ray-tracing is optimized to take advantage of the fact that multiple steps through a way will occur in the same block position, allowing us to quickly re-use the previous step's results. We also make use of a faster position tracking algorithm which avoids many excessive allocations.

</div>

<div class="code-example" markdown="1">

### Point of Interest optimizations

Complex mob AIs in Minecraft, primarily those belonging to Villagers and Pillagers, often need to find relevant points of interest in the world in order to choose the most appropriate AI task. In vanilla, querying all points within a chunk requires 16 separate retrievals through stream-heavy code. With Lithium present, this task is reduced to a single simple retrieval that makes use of a much faster (and traditional) iterator based approach, yielding anywhere from a 16-22x improvement for queries.

</div>

<div class="code-example" markdown="1">

### Data Tracker optimizations

The internal data manager used for tracking some entity state and properties has been optimized to use flat arrays and avoid expensive locking, providing a decent boost whenever these attributes are accessed during a game tick.

</div>

<div class="code-example" markdown="1">

### Redstone Wire optimizations

Calculating the new power level of redstone wire after a block update is costly. Reducing the number of blockstate checks without any change in behavior reduces redstone dust lag by about 35%.

</div>

---

## Radon

Radon is an Unofficial Fork of CaffeineMC's "Phosphor", made to work with Forge Mod Loader.

Phosphor is a *Minecraft* mod which works to optimize one of game's most inefficient areas-- the lighting engine. It works on both the client and server, and can be installed on servers without requiring clients to also have the mod. With Phosphor, the amount of time the game takes to generate chunks can be halved for some dimensions, and frame stuttering experienced while traversing the world can be significantly reduced. It's a no-compromises solution for improving performance either in single-player or large multi-player servers, and changes no features or behaviors of the vanilla game.

---

## Starlight

Starlight is a Forge mod for rewriting the light engine to fix lighting performance and lighting errors.

Starlight can be installed either on the dedicated server or client. It is not required to be installed on both sides. If you have Starlight on the server, clients can use Vanilla/Starlight to connect. Likewise, if you have Starlight on the client, you can connect to Vanilla/Starlight servers.

Browsing through [Starlight's Issue Tracker](https://github.com/PaperMC/Starlight/issues) will show further mod incompatibilities. Starlight is a rather destructive light engine rewrite, so it should be expected to break mods more often.

Starlight was developed for higher scale dedicated servers, as they suffered performance problems due to how ungodly slow the light engine was. The only solution was to create an extremely invasive mod which rewrote the entire light engine. I ported the mod to fabric so that I can update it during snapshots, and decided that publishing it for all users, especially client users, would be beneficial. However, it does have the downside of being an invasive mod: Being invasive didn't affect higher scale servers because they run on Bukkit.

Further reading on the technical details of how Starlight achieves its performance can be read here: [TECHNICAL_DETAILS.md](https://github.com/PaperMC/Starlight/blob/fabric/TECHNICAL_DETAILS.md)