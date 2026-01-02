## What this is

The 8BitDo Zero 2 can act like a tiny keyboard, which is hilarious and extremely useful: you can do Anki reviews one-handed (or two-thumbed) without hovering over your laptop keyboard. This repo contains a Karabiner-Elements complex modification that **translates the keys the controller *sends*** (its default “keyboard mode” outputs) into **Anki-friendly shortcuts**. 

This mapping is designed around Anki’s common/default shortcuts while reviewing:

* **1 / 2 / 3 / 4** → Again / Hard / Good / Easy
* **Space** → Show answer / confirm
* ***** → Mark (star) card
* **Cmd+Z** → Undo last grade
* **A / B / E / S / D** → Common navigation actions (Add, Browse, Edit, Study, Deck list) 

---

## Requirements

* macOS
* [Karabiner-Elements](https://karabiner-elements.pqrs.org/) installed
* 8BitDo Zero 2 connected and working as an input device
* Anki (desktop)

---

## Installation

1. **Find your device Vendor ID / Product ID**

   * Open **Karabiner-Elements → Devices**
   * Look for the 8BitDo Zero 2 entry and note the `vendor_id` and `product_id` (mine are `11720` and `36888`). 

2. **Create the complex modification**

   * Put the JSON rule into a file at:
     `~/.config/karabiner/assets/complex_modifications/8bitdo-zero2-anki.json`
   * Make sure the `vendor_id` and `product_id` match *your* device. 

3. **Enable it**

   * Karabiner-Elements → **Complex Modifications** → **Add rule**
   * Enable the “8BitDo Zero 2: remap device-sent keys to Anki shortcuts” rule.

## Keyboard Mode
* Press R and start: the blue led light at the base of the controller will blink 5 times.
* Once you confirm the 5 blinks, press and hold select until the led light starts blinking non-stop.
* Connect as bluetooth device.

## 8bitDo Zero 2 Original Key mapping

```
8BitDo Zero 2 Controller Key,Keyboard Key Pressed (Original)
D-Pad Up,c
D-Pad Down,d
D-Pad Left,e
D-Pad Right,f
Button X,h
Button Y,i
Button A,g
Button B,j
L Shoulder,k
R Shoulder,m
Select,n
Start,o
```
## Modified 8bitDo Zero 2 Mapping for Anki

```
Original Button,Original Mapping (Key Sent),New Mapping (Key Output),Anki Behavior Description
D-Pad Up,c,d,Deck: Back to the deck list.
D-Pad Down,d,a,Add: Create a new card.
D-Pad Left,e,s,Study: Start the session.
D-Pad Right,f,*,Mark: Star card for review.
Button X,h,1,Again: Review immediately (Yikes!).
Button Y,i,4,Easy: Longest interval (Easy-Peasy).
Button A,g,2,Hard: Short interval (Tough).
Button B,j,3,Good: Standard interval (Alright).
L Shoulder,k,b,Browse: Open the card browser.
R Shoulder,m,e,Edit: Edit current card.
Select,n,Space,Flip: Show answer/confirm.
Start,o,Cmd+Z,Undo: Revert last grade.
```
---

## Notes / gotchas (because reality is a gremlin)

* **This mapping is device-scoped.** The `device_if` condition means your laptop keyboard won’t be affected—only the Zero 2 will trigger these remaps. 
* **The `*` (mark/star) mapping** is implemented as **Shift+8** (that’s the normal “asterisk” on US keyboards). 

  * If your keyboard layout is different, or Anki expects a different star key, you may want to adjust this.
* **Controller modes matter.** If your Zero 2 is in a different mode (XInput/Switch/etc.), it may send different keycodes than the “original mapping” list. If the remap “does nothing,” check what key events the controller is actually emitting (Karabiner has an **EventViewer** for this).

---

## What’s included

* The controller’s **original key outputs** (what the Zero 2 sends by default in this setup). 
* A **clean remap table** showing: controller button → original key → new key → intended Anki behavior. 
* The **Karabiner-Elements JSON rule** implementing those remaps. 

---

### Tiny formatting fix you’ll want

In your “Original Key mapping” section, you open a code fence but don’t close it right after the list (the closing ``` currently appears at the very end). Consider wrapping that CSV in its own fenced block for readability. 
