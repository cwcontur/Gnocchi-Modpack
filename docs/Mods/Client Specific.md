---
layout: default
title: Client Specific
parent: Mods
---

# Client Improvement Mods
{: .no_toc }

Mods that make significant changes/improvements to the Minecraft client.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Performance

## Better FPS Render Distance

Better FPS Render Distance is a mod which adds a few performance improvements to increase fps.

By default *Minecraft* renders everything in a square radius(cylinder in 1.18), this is changed to a 3d circular radius which can be stretched horizontally via config or video option(video options button is not available with optifine). The higher the stretch the less caves below you will be rendered, esp distant ones. Provides about 10-35% less chunk sections to be rendered and thus gives a neat fps boost.

---

## Better Biome Blend

Better Biome Blend is a Client-Side performance and bug-fix mod. It adds support for smooth, large scale, sRGB correct biome color transitions. With the mod installed you can set the "Biome Blend" setting in your video options from 0x0 to 29x29. Compared to Vanilla, this setting no longer impacts performance.

---

## Clumps

Clumps groups XP orbs together into a single entity to reduce lag when there are many in a small area. On top of this, it also makes the player immediately collect the orbs once they touch the player, so you are not stuck with a bunch of orbs in your face.

---

## EntityCulling

Using async path-tracing to skip rendering Block/Entities that are not visible.

*Minecraft* skips rendering things that are behind you, so why is it rendering everything that you still can't see because of a wall in the way? This mod utilizes your other CPU cores/threads to do really quick path-tracing from your camera to all block/-entities to determine rather they are visible or not. During the rendering, the not visible ones will be skipped the same way entities behind you are.

---

## FerriteCore

This mod reduces the memory usage of Minecraft in a few different ways. A high-level technical description of the changes is available [here](https://github.com/malte0811/FerriteCore/blob/main/summary.md).

---

## Krypton Reforged

Krypton (from Ancient Greek kryptos, "the hidden one") optimizes the *Minecraft* networking stack, meaning it mostly improves server performance with lots of clients, but is also required on the client.

Krypton contains several optimizations, including:

- **Highly optimized Netty handlers** derived from the Velocity proxy, which I am the developer of. These handlers have sen real-world usage and extensive profiling, and strategically deploy native code where it makes the most sense.
- **Flush consolidation** to lower server CPU usage (and reducing the impact from hardware security vulnerabilities which exploit speculative execution) and lower server tick times.
- **Micro-optimizations** to reduce memory usage and improve packet serialization speeds.

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

## Rubidium

Rubidium is an Unofficial Fork of CaffeineMC's "Sodium", made to work with Forge Mod Loader.

- A modern OpenGL rendering pipeline for chunk rendering that takes advantage of multi-draw techniques, allowing for a significant reduction in CPU overhead (~90%) when rendering the world. This can make a huge difference to frame rates for most computers that are not bottle-necked by the GPU or other components. Even if your GPU can't keep up, you'll experience much more stable frame times thanks to the CPU being able to work on other rendering tasks while it waits.

- Vertex data for rendered chunks is made much more compact, allowing for video memory and bandwidth requirements to be cut by almost 40%.
Nearby block updates now take advantage of multi-threading, greatly reducing lag spikes caused by chunks needing to be updated.

- Chunk faces which are not visible (or facing away from the camera) are culled very early in the rendering process, eliminating a ton of geometry that would have to be processed on the GPU only to be immediately discarded. For integrated GPUs, this can greatly reduce memory bandwidth requirements and provide a modest speedup even when GPU-bound.

- Plentiful optimizations for chunk loading and block rendering, making chunk loading significantly faster and less damaging to frame rates.

- Many optimizations for vertex building and matrix transformations, speeding up block entity, mob, and item rendering significantly for when you get carried away placing too many chests in one room.

- Many improvements to how the game manages memory and allocates objects, which in turn reduces memory consumption and lag spikes caused by garbage collector activity.

- Many graphical fixes for smooth lighting effects, making the game run better while still applying a healthy amount of optimization.
  
- Smooth lighting for fluids and other special blocks.

- Smooth biome blending for blocks and fluids, providing greatly improved graphical quality that is significantly less computationally intensive.
Animated textures which are not visible in the world are not updated, speeding up texture updating on most hardware (especially AMD cards.)

---

## Rubidium Extras

- **Better Performance.** This mod fixes multiple issues with Sodium and Forge itself to improve performance. It has a patch mitigating random lag spikes in highly modded environments, and a patch fixing a Forge bug that was slowing down Sodium's chunk updating.
Better FPS Counter. Looks nicer, and can be customized to display minimum frametimes (useful for debugging lag on tick) and average frametimes over the last 15 seconds (for accurate benchmarking)

- **Zoom key!** A port of "Ok Zoomer" from Fabric, bound to C, allows you to view far away objects more easily.
Borderless Fullscreen. Minecraft's default mode makes it hard to tab out. This is off by default, but replaces the vanilla Sodium fullscreen option.

- **True Darkness.** Has options to make night time & caves realistically dark. Can be configured or turned off.

- **Entity Culling.** Improve performance in modpacks drastically by not rendering far away entities. Includes a configurable Y value so you can disable rendering mobs in caves while you're on the surface. Can be configured or disabled. Incompatible with Out Of Sight, because that mod does the same thing, and doesn't support Sodium anyway.

- **Chunk Fade In.** A port of "Fade In Chunks" from Fabric, this applies the Bedrock effect to reduce the pop-in effect from newly loaded chunks, either when you load in the game, switch worlds, or are just flying around. Can be configured or disabled.
  
- **Fog Toggle.** An option to turn off all fog, which is missing from vanilla Sodium.

- **Configurable Cloud Height.** Vanilla clouds are quite low, and there's no other mod to raise them on Forge. This mod defaults them to being a bit higher.

- **Integration With Magnesium/Rubidium Dynamic Lights.** This mod works perfectly with MDL, and improves its performance drastically with its optimizations. If you have MDL, you'll want to install this mod.