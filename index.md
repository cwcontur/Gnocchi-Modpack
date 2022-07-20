---
layout: default
title: Home
nav_order: 1
description: "Gnocchi"
permalink: /
---
<img src="https://img.shields.io/github/license/cwcontur/gnocchi-modpack">
<img src="https://img.shields.io/badge/Mod%20Loader-Forge-blue">
# Gnocchi is a Minecraft Modpack
{: .fs-9 }

This is the documentation for Gnocchi mod pack to get you a jump-start on your adventures. 
{: .fs-6 .fw-300 }

---

Don't have *Minecraft*? Get it here: 
[Buy Minecraft](https://www.minecraft.net/en-us/store/minecraft-java-bedrock-edition-pc){: .btn .btn-blue }

## About Mods[^note]

Mods (short for modifications) change Minecraft​'s game content in some way, such as to make minor adjustments to the game's mechanics or implement entirely new features.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Purpose

Most mods add content to the game to alter gameplay, change the creative feel, or give the player more options in how they interact with the Minecraft world. Some mods may be bigger expansions, while others add more settings and options to optimize speed, graphics, or gameplay of the game. Server mods or plugins mainly give server admins more options and ease of use, and most mods for single-player have a server version that allows or enhances the mod in multiplayer. Notably, a significant amount of Java Edition item duplication glitches are not patched in Java Edition (either never patched, or in the case of TNT duplication, patched then reverted) but mods that patch them are available.

When the base game is updated, the creator of a mod must update the mod accordingly, otherwise the mod may no longer work.

An official way of creating mods called add-ons is available for Bedrock Edition.

---

## Types of Mods

### Client-based

Client mods are direct modifications of the Minecraft game files. They are not custom clients, as they require modification of the client.jar file. These require mod loaders such as Minecraft Forge or Fabric.

Because the Minecraft server software ignores custom content from the client side, most of the client mods which add new content to the game do not work in multiplayer unless a modification has also been installed on the server. Some authors of client mods have made server versions of their mods available, and others have not. A few of the Loader/API-type client mods and many of the functional client mods (e.g. OptiFine or TooManyItems) have effect in multiplayer straight away, without any modification on server side.

### Server-based

Server mods are modifications to the official Minecraft server software. They are commonly designed to make the administration of servers easier by implementing tiered privileges for commands (such as kicking, banning, etc.). They are frequently implemented as "wrappers" which do not modify the main server .jar file, instead of monitoring its output and sending commands to it.

### Mod packs

Mod packs are collections of mods that have been put together and configured so that they all work together. Mod packs are often centered around a general theme like tech, quests, or magic. Mod packs often have either custom launchers or installers that make installing and running the mod pack easy. Some popular mod packs include Feed The Beast, Tekkit, RLCraft, and Hexxit.

Many mod packs can be found on custom launchers, which make it easy to install and launch various mod packs. In addition to making it easy to install mod pack clients, certain launchers can also download server mod packs.

---

# Getting Started

## World Pregeneration

It's recommended to pregenerate portions of your world for the smoothest experience. *[Chunky]((https://www.curseforge.com/minecraft/mc-mods/chunky-pregenerator-forge))* is used to do this; by default, it uses `minecraft:overworld` as the dimension it is generating, but this can be changed.

1. `/chunky radius 500` (Radius is # of chunks; any number can be used, but the world size grows exponentially with larger numbers and the process takes longer)

2. `/chunky start`

   - A progress bar will appear at the top of the screen along with a timer in order to track pregeneration progress.

![](../docs/assets/chunky.png)

3. Once Chunky finishes, you can also use it to pregenerate other dimensions if desired using: `/chunky world [dimension]` (Replace dimension with the name of the desired dimension to pregenerate from the list below)
    - `allthemodium:mining`
    - `allthemodium:the_other`
    - `assemblylinemachines:chaos_planes`
    - `blue_skies:everbright`
    - `blue_skies:everdawn`
    - `minecraft:the_end`
    - `minecraft:the_nether`
    - `the_bumblezone:the_bumblezone`
    - `twilightforest:twilight_forest`

<div class="code-example" markdown="1">

**Please note, not all available dimensions are listed above, such as `dimdungeons:build_dimension` and `dimdungeons:dungeon_dimension`. Additionally, the dimension `bonsaitrees3:growtown` should *not* be pregenerated because it is not a dimension that players can visit; it exists for the backend of the mod to use.**

- *Additional Chunky commands can be found via `/chunky help`*
  
</div>

> This process doesn't take a lot of time and can significantly improve chunk loading performance of the game to make the overall experience faster + smoother.

---

## More Info

**This mod pack changes/improves the vanilla behavior of the game in terms of: player movement, player HUD, player inventory, and more. Check out '*[Introduction](https://mod.gnocchi.cc/docs/Introduction/)*' page for info on these changes which includes keybinds, gameplay behavior, etc.**

[Introduction](https://mod.gnocchi.cc/docs/Introduction/){: .btn .btn-blue}

*Wanna see which mods are in this pack? Check out the mods page:*

[Mods](https://mod.gnocchi.cc/docs/Mods){: .btn }

Info about client changes and server changes can be found under '*Configurations -> [Server](https://mod.gnocchi.cc/docs/Configurations/Server/)*' or '*-> [client](https://mod.gnocchi.cc/docs/Configurations/Client/)*' should you wish to know more about the specifics of the changes to the game.

[Server](https://mod.gnocchi.cc/docs/Configurations/Server/){: .btn }
[Client](https://mod.gnocchi.cc/docs/Configurations/Client/){: .btn }

---

[^note]: Page info provided by [Mods](https://minecraft.fandom.com/wiki/Mods "minecraft.fandom.com/wiki/mods") Minecraft Wiki
