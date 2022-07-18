---
layout: default
title: Server
parent: Configurations
---

# Server Configuration
{: .no_toc }

Server settings and mod configs which have been changed. A basic description of each is provided in case changes are desired.
{: .fs-6 .fw-300 }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## JVM Server Arguments

```java
-Xmn32G -Xmx32G -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8 -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15  -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 
```

## JVM Arguments Explained
`-Xmn10G`
<div class="code-example" markdown="1">
Minimum java heap size. Oracle recommends that -Xmn and -Xmx be set to the same value. This eliminates potentially costly heap reallocations, and can reduce the amount of heap fragmentation that can occur. Setting -Xms is then unnecessary since the heap size itself is static.
</div>

---

`-Xmx24G`
<div class="code-example" markdown="1">
The max memory GC will use. Setting a low maximum heap value compared to the amount of live data decrease performance by forcing frequent garbage collections.
</div>

---

`-XX:+UseG1GC`
<div class="code-example" markdown="1">
The Garbage-First (G1) garbage collector is a server-style garbage collector, targeted for multiprocessor machines with large memories. It attempts to meet garbage collection (GC) pause time goals with high probability while achieving high throughput. Whole-heap operations, such as global marking, are performed concurrently with the application threads. This prevents interruptions proportional to heap or live-data size.
</div>

---

`-XX:+ParallelRefProcEnabled`
<div class="code-example" markdown="1">
Enables parallel reference processing. By default, this option is disabled.
</div>

---

`-XX:MaxGCPauseMillis=200`
<div class="code-example" markdown="1">
The time that the garbage colector will take to clear the memory. The goal for the maximum pause time.
</div>

---

`-XX:+UnlockExperimentalVMOptions`
<div class="code-example" markdown="1">
Experimental flags able to be turned on.
</div>

---

`-XX:+DisableExplicitGC`
<div class="code-example" markdown="1">
Another way that applications can interact with garbage collection is by invoking full garbage collections explicitly by calling System.gc(). This can force a major collection to be done when it may not be necessary (for example, when a minor collection would suffice), and so in general should be avoided. The performance effect of explicit garbage collections can be measured by disabling them using the flag -XX:+DisableExplicitGC, which causes the VM to ignore calls to System.gc().
</div>

---

`-XX:+AlwaysPreTouch`
<div class="code-example" markdown="1">
Enables touching of every page on the Java heap during JVM initialization. This gets all pages into the memory before entering the main() method. The option can be used in testing to simulate a long-running system with all virtual memory mapped to physical memory. By default, this option is disabled and all pages are committed as JVM heap space fills.
</div>

---

`-XX:G1NewSizePercent=30`
<div class="code-example" markdown="1">
Sets the percentage of the heap to use as the minimum for the young generation size. The default value is 5 percent of your Java heap.
</div>

---

`-XX:G1MaxNewSizePercent=40`
<div class="code-example" markdown="1">
Sets the percentage of the heap size to use as the maximum for young generation size. The default value is 60 percent of your Java heap.
</div>

---

`-XX:G1HeapRegionSize=8`
<div class="code-example" markdown="1">
The size of the heap regions. The default value is based on the maximum heap size and it is calculated to render roughly 2048 regions. The size must be a power of 2, and valid values are from 1 to 32 MB.
</div>

---

`-XX:G1ReservePercent=20`
<div class="code-example" markdown="1">
Sets the amount of heap that is reserved as a false ceiling to reduce the possibility of promotion failure. The default value is 10.
</div>

---

`-XX:G1HeapWastePercent=5`
<div class="code-example" markdown="1">
Sets the percentage of heap that you are willing to waste. The Java HotSpot VM does not initiate the mixed garbage collection cycle when the reclaimable percentage is less than the heap waste percentage. The default is 10 percent.
</div>

---

`-XX:G1MixedGCCountTarget=4`
<div class="code-example" markdown="1">
Sets the target number of mixed garbage collections after a marking cycle to collect old regions with at most G1MixedGCLIveThresholdPercent live data. The default is 8 mixed garbage collections. The goal for mixed collections is to be within this target number. 
</div>

---

`-XX:InitiatingHeapOccupancyPercent=15`
<div class="code-example" markdown="1">
Sets the Java heap occupancy threshold that triggers a marking cycle. The default occupancy is 45 percent of the entire Java heap.
</div>

---

`-XX:G1RSetUpdatingPauseTimePercent=5`
<div class="code-example" markdown="1">
G1 tries to schedule concurrent processing of the remembered set updates so that the Update RS phase takes approximately -XX:G1RSetUpdatingPauseTimePercent percent of the allowed maximum pause time. By decreasing this value, G1 usually performs more remembered set update work concurrently.
</div>

---

`-XX:SurvivorRatio=32`
<div class="code-example" markdown="1">
Ratio of eden/survivor space size. The default value is 8.
</div>

---

`-XX:+PerfDisableSharedMem`
<div class="code-example" markdown="1">
Forces JVM to use anonymous memory for Performance Counters instead of a mapped file. This helps to avoid random VM pauses caused by spontaneous disk I/O.
</div>

---

`-XX:MaxTenuringThreshold=1`
<div class="code-example" markdown="1">
Maximum value for tenuring threshold. The default value is 15.
</div>

---

## Optional JVM Arguments
- **AggressiveHeap**
<div class="code-example" markdown="1">
Enables Java heap optimization. This sets various parameters to be optimal for long-running jobs with intensive memory allocation, based on the configuration of the computer (RAM and CPU). By default, the option is disabled and the heap is not optimized.
</div>

---

- **AggressiveOpts**
<div class="code-example" markdown="1">
Enables the use of aggressive performance optimization features, which are expected to become default in upcoming releases. By default, this option is disabled and experimental performance features are not used.
</div>

---

- **UsePerfData**
<div class="code-example" markdown="1">
Enables the perfdata feature. This option is enabled by default to allow JVM monitoring and performance testing. Disabling it suppresses the creation of the hsperfdata_userid directories. To disable the perfdata feature, specify -XX:-UsePerfData.
</div>

---

- **UseCompressedOops**
<div class="code-example" markdown="1">
Disables the use of compressed pointers. By default, this option is enabled, and compressed pointers are used when Java heap sizes are less than 32 GB. When this option is enabled, object references are represented as 32-bit offsets instead of 64-bit pointers, which typically increases performance when running the application with Java heap sizes less than 32 GB. This option works only for 64-bit JVMs.
</div>

---

- **ParallelGCThreads**
<div class="code-example" markdown="1">
The maximum number of threads used for parallel work during garbage collection pauses. This is derived from the number of available threads of the computer that the VM runs on in the following way: if the number of CPU threads available to the process is fewer than or equal to 8, use that. Otherwise add five eighths of the threads greater than to the final number of threads. At the start of every pause, the maximum number of threads used is further constrained by maximum total heap size: G1 will not use more than one thread per -XX:HeapSizePerGCThread amount of Java heap capacity.
</div>

---

- **ConcGCThreads**
<div class="code-example" markdown="1">
he maximum number of threads used for concurrent work. By default, this value is -XX:ParallelGCThreads divided by 4.
</div>