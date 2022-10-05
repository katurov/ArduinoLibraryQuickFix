# Arduino Library Quick Fix

Once in a while I have a problem with a "libraries" folder of Arduino IDE: after a library's update IDE creates files "* 2.cpp" (.h, etc.) and it crushed any attemp to compile the sketch.

Manual fix is: walt through the folder and its subfolders and delete all files with " 2" in a name. Boring and takes a lot of time.

The root of the problem is iCloud. 
  1. IDE install the liubrary
  2. Mac OS see they are untouced and unloads them into cloud
  3. Now the files are changed to name.icloud
  4. IDE wants to update library and see no files (as they are .icloud now). You can easy check this open Finder ("normal" files) and Terminal (.icloud ones)
  5. Mac OS by somehow make a mess here (unclear for me but this is true)
  6. Now you have "* 2.*" files
  
Before start it all: close the IDE
  
How I fix the problem in two steps:
  * Make sure all files are now downloaded from the cloud and are files not a links
  * Find and delete
  
How to "download" files from cloud to the disk and make 'em files again:
```
cd ~/Documents/Arduino/libraries
find . -type f -name "*.icloud" -exec brctl download {} \;
```
this will download 'em all. Make sure they are by searching ```find . -type f -name "*.icloud"``` the list have to be empty.

Now find and delete:
```
find ./ -name "* 2.*" -type f -delete
```
and make sure they are: ```find ./ -name "* 2.*" -type f``` once it also was a directory, so ```find ./ -name "* 2.*" -type d``` helps to find 'em. Be careful with folder deletion as far as sometims it can be legitime one in a code.

Now re-open IDE and update libraries.
