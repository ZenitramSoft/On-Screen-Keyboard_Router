# On Screen Keyboard Router for Q SYS

A Q SYS User Component that routes text from a single QSC On Screen Keyboard to multiple destinations using toggle buttons. It also persists names across Core reboots.

**Creator note**  
I built this in my own free time. It is not work related.

## Why I built this

The stock QSC On Screen Keyboard plug in supports only one to one connections. There was no simple way to use a single On Screen Keyboard to update multiple string controls at the same time. This User Component solves that by letting one keyboard feed many destinations with simple selection logic.

---

## What it does

* Takes the single **StringInput** from the QSC On Screen Keyboard plug in.
* Routes the text to the **StringOutput[i]** that corresponds to the **Selection[i]** toggle that is high.
* Clears the On Screen Keyboard text and the active **StringOutput** whenever a different **Selection** goes high.
* Stores a persistent copy of each output in **StringOutputFB[i]** and restores all values on startup.

You can scale the array size up or down as needed. Keep the array sizes of **StringOutput**, **StringOutputFB**, and **Selection** the same.

---

## Features

* Live input routing to the selected destination in real time
* Persistent storage and automatic restore on startup using **StringOutputFB[i]**
* Backspace key support for clean clears and edits
* Sample design that demonstrates 15 arrayed controls ready to expand or shorten

---

## Repository contents

* User Component file
* Sample Q SYS design with 15 arrayed controls
* Lua script that powers the routing and persistence
* This README

---

## Requirements

* QSC On Screen Keyboard plug in  
  Get it from the Q SYS Designer Asset Manager
* Script Access enabled on the keyboard component  
  Required so Lua can interact with its controls
* A **KeyboardName** String control in this User Component  
  Set its value to the exact component name of your On Screen Keyboard

---

## Controls used by this User Component

**Inputs and settings**

* `KeyboardName`  
  String control. Must match the component name of your On Screen Keyboard.

* `StringInput`  
  String control that receives text from the On Screen Keyboard.

**Selection and outputs**  
All three sets must share the same array size.

* `Selection[i]`  
  Boolean toggle controls. The high selection determines the active destination.

* `StringOutput[i]`  
  String outputs that receive the routed text.

* `StringOutputFB[i]`  
  String feedback outputs used for persistence across Core reboots.

---

## Setup

1. Add the QSC On Screen Keyboard to your design from the Q SYS Designer Asset Manager.
2. Enable Script Access in the properties of the keyboard component.
3. Add this User Component to your design.
4. Set the **KeyboardName** control to the exact name of the keyboard component.
5. Wire **StringInput** to the keyboard string output.
6. Connect **StringOutput[i]** to the destinations that should receive text.
7. Size the arrays for **Selection**, **StringOutput**, and **StringOutputFB** to the same length.
8. Optionally load the sample design to see a working setup with 15 arrayed controls.

---

## Usage

* Press one **Selection[i]** toggle to choose the active destination.
* Type on the On Screen Keyboard. The active **StringOutput[i]** updates in real time.
* Change the selection to another destination. The component clears the keyboard text and the previously active output, then routes new input to the newly selected output.
* After a Core reboot, all names are restored from **StringOutputFB[i]**.
