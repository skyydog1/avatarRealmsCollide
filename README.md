# Avatar Realms Collide data and reverse engineering

This repository documents research and analysis of publicly available extracted data from the mobile game Avatar Reamls Collide. The data was gathered through inspection of app files in the Android environment.

# Usage

If you don't want to deal with sorting through the individual files, just download the combined sheets excel file

# Data mining and reverse engineering process

Initially I had only planned to grab the data in csv format and leave it at that, however I ended up analyzing the game's files.

I wanted the game's asset id files in order to match up in game asset names to their ids in the csv files, but this information was not readily availabe.

## Overview of the process

### Initial file extraction:
1. Extract game data from bluestacks 5 in program files X86, program files, appdata, and program data. Most of this information was either encrypted or not relevant to my uses.

### Gaining root access
2. Gain root access to bluestacks 5. I originally intened to use Kitsune mask/Magisk to gain root access to bluestacks, but I found a simpler method in modifying the root access flags in the Bluestacks conf file under ProgramData to be true.

### File transfer via ADB
3. Use adb and root access to copy game files from bluestacks to my personal computer. This was difficult because even though I had root access I coudln't find a way to move files directly from bluestacks in the adb shell. I had to copy the files over to the SD card directory using tar, then use adb to move those files to my local system.

### Decrypting and analyzing files
4. The game is built using Unity and like most Unity games uses IL2cpp. I used IL2cpp dumper, a tool for analyzing unity assets, to reconstruct readable source code from compiled binaries. I also used JADX to parse the DEX files for useful source code.

### Data extraction and cleaning
5. I was now able to use parsed data to find the asset ids I wanted, as well as the rest of the game's code, which was a whole lot of fun. I used python pandas and csv writer to format the data in a legible manner.

### What I learned
- Bluestack internals
- ADB and the Android filesystem
- Unity asset structures and IL2CPP decompilation
- Pandas and csv write for data cleaning
