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

## Crash reports

If Minecraft crashes, a modified game is flagged in the crash report.

The crash report text includes one of these lines near the bottom:

```
Is Modded: Probably not. Jar signature remains and client brand is untouched
Is Modded: Very likely; Jar signature invalidated
Is Modded: Definitely: client brand changed to (present loader, such as "fml,forge", "modloader", or "fabric")
Is Modded: Unknown (can't tell)
```

The code that checks for mods is fairly simple, and it's not always correct; it may say 'probably not' even with mods installed. However, it's very difficult to get the 'very likely' message if you haven't modified your Minecraft .jar file somehow, so that's essentially a 'yes'. There's also a 'definitely' message, seen when a Bukkit server crashes and under other similar circumstances, like when the Minecraft Forge API is installed.

'Probably not' appears when the client/server brand appears to the in-game check to be unaltered (often termed 'vanilla') and the META-INF folder is still there. 'Very likely' appears when the META-INF folder is not present but the client/server brand seems to be vanilla. 'Definitely' plus the client name appears when the client is not vanilla:
`Is Modded: Definitely: Client brand changed to 'fml,forge'`

[^note]: Page info provided by [Mods](https://minecraft.fandom.com/wiki/Mods "minecraft.fandom.com/wiki/mods") Minecraft Wiki
