# AV1-Media-Transcode-Guide
 Handbrake-Tdarr-Setup-Customization

This guide is intended to be viewed RAW.
﻿Here is a written version of the guide in a step by step readable and organized format:
System Requirements
Windows 10/11 machine OR VM running on unRAID.
Additional nodes can be added if you have multiple Windows machines.
For a VM you will need to go to "Tools", "System Devices" 
and find your 4000 series GPU IOMMU group and attach vfio at boot and reboot.
NVIDIA GeForce RTX GPU (4050-4090)
Decent processor
Preparation

Update your NVIDIA drivers to the latest version.
Shut down Tdarr Node and Server.
Download and extract Tdarr files to C:\Tdarr.
Install Handbrake GUI 1.8.2 or above from https://handbrake.fr/rotation.php?file=HandBrake-1.8.2-x86_64-Win_GUI.exe
Extract the Command Line version of Handbrake (HandBrakeCLI.exe) to your desktop via https://handbrake.fr/downloads2.php
Overwrite the three instances of HandBrakeCLI.exe in different locations:
C:\Tdarr\HandBrakeCLI.exe
C:\Tdarr\Tdarr_Node\assets\app\HandBrakeCLI.exe
C:\Tdarr\Tdarr_Server\assets\app\HandBrakeCLI.exe
Do this for each additional node as well if any.
Create a folder called C:\cache
Handbrake GUI
Open Handbrake and select any video file.
Click [Tools] > [Preferences] > [Video].
Checkmark "Allow use of the Nvidia NVENC Encoders" and set "Prefer use of..." to your desired setting.
Set the format to MKV, resolution limit to None, and dimensions as needed.
Configure video settings:
Video Encoder: AV1 10-bit (NVEnc)
Framerate: Same as source & Constant Framerate
Encoder Option: Encoder Present: Slowest (slide right)
Quality: Your desired setting (note that a lower number results in a larger file size)
Configure audio settings:
Codec: E-AC Passthru
Save the preset with the following settings:
Name: t1
Resolution Limit: None
Audio:
Track Selection Behavior: All Matching Selected Languages
'Auto Passthru' Behavior: Check all of them (yes, all of them)
Fallback Encoder: None
Audio encoder settings for each chosen track: Codec > Auto Passthru
Testing
You can skip this step if you want to test the results before executing the rest of the process.
Run Handbrake with your selected preset and video file.
Tdarr Library
At the top, click Library (and yes, you can create multiple ones later).
Click Library+ and configure the mini tabs:
[Source]: Turn on folder watch and select where your media is located.
[Filters]: Codes to Skip: AV1 (or AV1,HEVC if you want to leave x265 files alone)
Configure Transcode Options:
Disable all options or delete them except for New File Size Check!
Add the following custom transcode option:
Community: Video Transcode Customisable
Set codecs to exclude: av1 (or av1,hevc if you want to leave x265 files alone)
Set transcode arguments: --preset-import-gui -Z "t1"
Set output container: .mkv
Click New Container Check.
Change upperbound to 99 and lowerBound to 5
Click the big green options button and click NEW FRESH SCAN!
Final Notes
If you don't see transcoding happening, it may be because something was named incorrectly.
I recommend rebooting your system if it doesn't work the first time (it's happened to me too!).
Go to the very bottom and sort your queue by whatever option you prefer.
