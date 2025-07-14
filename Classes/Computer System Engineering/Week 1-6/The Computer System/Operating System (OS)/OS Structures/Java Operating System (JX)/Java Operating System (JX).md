---
aliases:
  - JX
---
written almost entirely in Java*
- runs in a single address space - no [[Virtual Memory]], no [[Memory Management Unit (MMU)]]
- difficulties in memory protection

![[Java Operating System (JX)-1.webp|321x202]]

Each domain represents an independent Java Virtual Machine (JVM)
- * Domain 0 is written in C and assembly language; everything else is Java
- Communication between domains is done through **portals**
