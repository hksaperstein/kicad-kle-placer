# KiCAD KLE Placer
A plugin for KiCAD used to place switches based on a KLE. Tested (and should work) in KiCAD 6. Based on [kicad-kbplacer](https://github.com/adamws/kicad-kbplacer).

NOTE:
- Rotated keys in KLE are NOT SUPPORTED (I'm working on it, read at the bottom of the page) 
- Diode placement is NOT SUPPORTED (I'm working on it) 
- Plugin is not fully tested
- I tested this plugin with [marbastlib](https://github.com/ebastler/marbastlib)

# Installation
Download the github code and place it into `C:\Users\<user>\Documents\KiCad\6.0\scripting\plugins\kicad-kle-placer` (or wherever your plugins folder is located):

![image](https://user-images.githubusercontent.com/23428162/175076873-44e1a3c8-77f8-4e67-b2b9-29ffcd3559e7.png)

You can then refresh your plugins and it should show up (you can also find a shortcut to the plugins folder here):

![image](https://user-images.githubusercontent.com/23428162/175077103-d6da1715-4924-4cf6-aa6d-9c0848566184.png)

What the dialog looks like:

![image](https://user-images.githubusercontent.com/23428162/175072304-ee220f69-a435-49fd-82b6-745fc88c3ca1.png)

## Example KLE
**There should be the SAME number of footprints/symbols (in your KiCAD project) as there are keys (in the KLE).**

The script takes in the `json` file of a KLE, downloaded as shown:

![image](https://user-images.githubusercontent.com/23428162/168476867-7477de1c-a342-41e8-b515-0a1d21b097b8.png)

How the KLE can look like (either squish all the keys together or you can mark the multi-layout as indicated below):

![image](https://user-images.githubusercontent.com/23428162/175071359-8efe603d-4247-41ba-902d-a013f40f2fec.png)

With the marked multilayout (colour is irrelevant, learn more about my [firmware script](https://github.com/zykrah/firmware-scripts)):

![image](https://user-images.githubusercontent.com/23428162/175078367-db26a163-4054-4f3a-b31a-999e45c68390.png)

## Example Schematic

In terms of **stabilizers**, if the switch footprint library you're using has *separate switch and stabilizer footprints*: use the same reference for the stabilizer as the switch it corresponds to (e.g. `SW54` and `S54`) 

**IMPORTANT: See the rules mentioned below for an explanation on how you should order your schematic (order by the horizontal centers of switches).**

Schematic from the same example as earlier:

![image](https://user-images.githubusercontent.com/23428162/175074701-5625581c-6e57-44ce-9565-85b540ad7a5f.png)

## Order of keys in KLE/Schematic
NOTE: The plugin counts by footprint reference (i.e. `SW1`, `SW2`, etc...) starting from the top left-most key. It then goes left to right (based on the horizontal center of the key), then up to down (based on the top edge of the key).

Example of how it's ordered:

![image](https://user-images.githubusercontent.com/23428162/175075883-9574b95c-706f-4cd3-a435-6e02f111af60.png)

Another example with multilayout. See how the 2u key is in the middle of the 1u keys when overlapped, so it goes in between those in the order (NOTE: I didn't mark the multilayout value/indices here, but you need to for the script to work):

![image](https://user-images.githubusercontent.com/23428162/175077847-c7cd4149-db20-4e18-9a28-31ee0bcc9925.png)

You can annotate your KiCAD schematic in a similar way with this option (follow the placement/ordering as in the example schematic above):

![image](https://user-images.githubusercontent.com/23428162/175082731-60ad769c-7e5f-448e-983e-6148822883f3.png)

## Regarding rotated keys
I haven't fully tested/figured out rotated switches. It's hard to do rotated switches because of how the plugin works currently (it goes left to right based on the order of switches, `SW1`, `SW2`, and so on). But the order in KLE gets mixed up/is hard to interpret once you introduce rotated keys, so I would have to find a nicer option for accurately relating keys on the KLE to footprints on the PCB.
