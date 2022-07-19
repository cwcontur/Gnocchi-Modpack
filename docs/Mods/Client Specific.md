---
layout: default
title: Client Specific
parent: Mods
---

# Client Improvement Mods
{: .no_toc }

Mods that make significant changes/improvements to the Minecraft client.
{: .fs-6 .fw-300 }

<details open markdown="block">
  <summary>
    Table of Contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

<!-- ## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc} -->

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

### LazyDFU

LazyDFU is an optimization mod that makes the initialization of DataFixerUpper "lazy" - that is, it will not immediately create the rules required to migrate data from older versions of *Minecraft* to newer versions until it actually needs to do so. It does not modify DFU and should be safe, but do exercise more than the usual caution.

The premise of LazyDFU is simple: most of the time, you will not need to convert data for every version of the game. As a result, DFU rule compilation occurs later, when the game is already up and running. This means it is possible you may see lag spikes if LazyDFU forces the game to compile migration rules, but once complete there is no performance penalty.

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

---

# QOL (Quality of Life)

## Bad Wither No Cookie

A lightweight universal mod to silence these nasty world wide broadcast sounds:

- Wither
- End Dragon
- Thunder
- and now any sound that any mod makes!

---

## Client Tweaks

This mod adds a bunch of optional tweaks to improve the Quality of Life during gameplay. Tweaks can be individually enabled or disabled and configured. Many of the tweaks are disabled by default, so make sure to enable the features you want for the most bestest experience possible.

---

## Climb Ladders Fast

Very simple and efficient mod to climb ladders faster.  Should also work with other climbing mechanics like vines

Let go of movement keys and look up to go up faster, look down to go down faster.

---

## Connectivity

Lightweight mod which solves several connection problems like Login-Timeouts, DecoderException, Packet size limits, Ghostblock issues, Payload too large and more. It also offers commands to analyze network traffic.

---

## Crash Utilities

 Crash Utilities adds a number of tools for finding and fixing common server problems.

---

## Debugify

Debugify is a project that fixes over 60 bugs found on the [bug tracker](https://bugs.mojang.com/projects/MC/issues) in *Minecraft*. (and does nothing more!)

**"MC-147605" is switched off to false because it breaks JEI search bar.**

---

## DefaultSettings

This client mod offers the ability of creating and using modpacks which ship custom settings, entries in the server list or even custom keybindings without having them overwriting your local settings every time the modpack updates.

---

## Ding

Very simple mod. Clientside. Plays a configurable sound when Minecraft loads and reaches the Main Menu, or when the world loads when you connect to a server.

---

## DrawerFPS

Simple, efficient mod which lets you configure at which range Storage Drawers do render items to improve fps.

---

## Durability Tooltip

Durability Tooltip shows you the durability of an item!

---

## FallingTree

This mod will change the way you break trees. 2 modes are available:

- **Instantaneous:** Break one log and the whole tree will fall

- **Shift down:** Break a block and the log will slowly shift down as you cut it (good if you don't want to "cheat" too much but are lazy to go cut top log blocks 😛)

---

## Farsight

Farsight is a client-side util which lets you see farther on servers than the servers view distance. 

It works by having the client keep the chunk data, even when the server unloads that chunk up to a max distance of 32 chunks(configurable).

---

## Fix Experience Bug
When players travel to and from other modded dimensions, there is a bug in *Minecraft* where their experience is displayed as zero until they earn one new experience point or log out of the game and log back in.

This bug blocks players from enchanting items and using items that require experience.

This mod fixes this bug.  

---

## Forgiving Void

Have you ever wondered what would happen if instead of dying in the void, you just kept falling? Turns out you just come back out from the top (and the fall doesn't even kill you due to magic miracle power).

Instead of dying in the void, you will fall back down from the sky. Despite the large falling height, you can still survive as long as you had full health when landing.

---

## Inventory HUD +

This mod contains a few features, first of all - Inventory HUD, it shows your inventory while you are playing, you can switch between mods (mini/normal and horizontal/vertical), also you can change background transparency and toggle animation on/off 

Next feature is PotionHUD, it shows your potion effects with timer or duration bar if you are using mini mode, you can change gap between effects and background transparency in config, and you can enable horizontal mode as well

And last but not least feature is ArmorHUD, it shows durability of your armor and equipment, also shows how many free slots do you have in your inventory and how many arrows do you have. This HUD is fully customizable, you can change scale, type of damage indicator or turn on/off each part of your equipment

You can change a lot of options in config ("Mod" button in Main Menu, then "Config"), also you can change the position for each HUD by simply dragging and dropping them. To open ingame config screen you can use keybind ("O" by default)

---

## Inventory Profiles Next

This mod will:

- Help you keep your inventory sorted
- Replace your quasi-broken tool
- Dump everything in that chest with one click
- Move the items you have that are also already in the chest
- Lock item slots in place so that sorting ignores them
- Keep locked slots empty
- Allow you to press R+C to set your shortcuts
- Be pure client-side, so that it works everywhere

---

## Inventory Sorter

Some simple inventory sorting tweaks. Middle click sorts, mousewheel in and out of inventory one item at a time.

Quick note: the default keybindings for the mousewheel actions *are* the wheel. If you set them to something else, just reset to recover the wheel operation.

---

## Just Enough Items (JEI)

JEI is an item and recipe viewing mod for Minecraft, built from the ground up for stability and performance.

### JEI Enchantment Info

This mod adds JEI info entries for enchantments. Press R while hovering over a book with a single enchantment to view info about it.

### JEI Integration

JEI Integration, the successor to NEI Integration by Tonius, is an addon for Just Enough Items (JEI) for *Minecraft* 1.10 and above. The mod provides JEI recipe handlers for other mods where otherwise absent. In addition to additional recipe handlers, it adds configurable tooltips which can provide insightful information for pack developers and tech-savvy players.

### JEITweaker

This mod adds CraftTweaker support for Just Enough Items, such as the ability to hide items, hide categories and add JEI descriptions items.

### Just Enough Advancements

An addon for JEI which shows Advancements in JEI. You can search for them as they were items. They will tell you what you need to do to reach them, even if they aren't unlocked!

### Just Enough Effect Descriptions

Just Enough Effect Descriptions of JEED is a JEI plugin that provides useful information regarding status effects.

The mod adds a new Effects recipe category accessed either by clicking any of the newly added status effect icons on the JEI item screen or by clicking an active effect from its box on the inventory screen.

### Just Enough Resources

Adds JEI integration for world resources like ores and mob drops.

---

## Jade🔍

Jade is a UI improvement mod which shows information about what you are looking at. Jade is a fork of HWYLA by TehNut

- Item Handlers - Show items inside item handlers (chests, hoppers, ender chests...)

- Breaking Progress - Show block breaking progress as a small progress bar

- Brewing Stand - Show fuels and process time

- Mob Effects - Show what potion effects the mob has

- Entity Growth - Show growing time and breeding cooldown of animals

- Horse stats - Jump height and speed of horses, mules and donkeys, even strength of llamas

- Item Frame - Show item in item frame

- Hide Mod Names - Hide mod name in tooltip (Disabled by default)

- Beehive - Show bees and honey in beehive

- Armor Stand - Show armors on armor stand

- Chicken Egg - Show time before next egg

- Command Block - Show command line

- Trapped Chest - Hide as normal chest

- TNT - Show stability

- Note Block - Show pitch and instrument

- Painting - Show painting name

- Accurate Block Name - Shows "Potted Cactus" rather than "Cactus"

- Misc - Show boat, end crystal, armor stand and more

- For modders - Additional tooltip renderers

### Jade Addons

This mod adds more mod supports for Jade 🔍 1.18+.

---

## JourneyMap

JourneyMap is a client+server mod for Forge which maps your *Minecraft* world in real-time as you explore. You can view the map in a web browser or in-game as a Minimap or full-screen.

### JourneyMap Integration

This mod was made to let JourneyMap support some features from other mods to make your life easier.

And it's also included some mod tweaks and non-mod integration functions btw.

---

## Leap

*Take a leap forward with this simple mod that adds a new enchantment that allows you to double jump!*

The Leaping enchantment can be obtained just like any other treasure enchantment, being available as loot in chests, fishing, or from the Librarian Villager. It can only be obtained in one level. The enchantment is exclusive to boots. You can use a double jump anytime your motion is moving downward.

---

## Login Protection

Protects the player during login and dimension change/respawn teleport from any harm.

---

## Lootr

**What is Lootr? It's simple: unique inventories for every loot chest for every player on a server.**

**What does that mean?** When you open a loot chest (distinctly textured from Vanilla chests), what items you get are unique to you (as though you had opened an Ender Chest). This means no empty chests, and no picking up other people's trash!

**How does this help?** For multiplayer servers, especially those with mods that depend on items looted from chests, it means finding loot closer to home. No more extensive, server-draining trips generating hundreds of chunks in search of a fresh chest.

**How does it work?** Any time an eligible container is placed in the world, it is tested to see if it can be converted. This is now retroactive! You can add Lootr to a pre-existing world.

**What if I don't want all chests to be available to everyone?** Especially when it comes to mods that require you to pass through a dungeon and clear it to obtain loot, there can be balance issues. You can now block certain chests (based on dimension, loot table, loot table's mod ID, or structure), or set chests to Decay, meaning they can only be looted for a pre-determined (and configurable) period of time. See the Refreshing & Decaying section for more info.

---

## Mod Name Tooltip

Mod Name Tooltip shows which mod an ItemStack came from on its tooltip.

---

## Shutup Experimental Settings!

This simple mod is a forge port of the fabric mod "Disable Custom Worlds Advice" which disables the annoying "Experimental Features" advice that appears every time you create or load a world with custom dimensions or world settings. You can use it if either this screen annoys you as much as it does to me or you are creating a mod with custom worldgen!

---

## TipTheScales

Allows for more options when adjusting the GUIScale option as well as making it a slider.

---

## Toast Control

This mod allows you to control what toasts show up in Minecraft.  By default, Minecraft shows you all toasts, including toasts for Recipes, Advancements, the Narrator, and Tutorials.  

This mod, by default, disables toasts for Recipes and Tutorials.  It can disable any other kind of toast through the configuration file.

If you do not want to block toasts, but think they are in the way, you can change their backgrounds.  Toast Control allows for translucent or transparent backgrounds (vanilla toasts only).

---

## Traveler's Titles

Traveler's Titles is a simple client-side mod that adds RPG-like titles when entering biomes or dimensions.

---

## Vein Mining

Vein Mining is a mod that adds the titular Vein Mining enchantment, which allows the enchanted tool to break matching connected blocks. The enchantment and mining logic are highly configurable, letting players and modpack developers find their preferred method of balance.

---

## Wall-Jump!

Wall to wall platforming in *Minecraft*! This mod adds wall jumping and double jumping to the game.

**Wall Cling:** Jump towards a wall and hold the wall jump key (LSHIFT). Then...

**Wall Jump:** While wall clinging, keep holding W and let go of LSHIFT to wall jump.

**Double Jump:** Optional mid-air jump that you can use to your advantage.

---
