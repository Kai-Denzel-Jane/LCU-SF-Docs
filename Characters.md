# Adding new characters in the game

**THIS WORK ONLY ON THE VERSION 1.0 OR LATER OF [KF-LAUNCHER](https://github.com/AntoineUserName/Kestrel-Fusion-Launcher/)**


> # Start

1. Open the app

2. On the top bar, click on "Characters" > "new character"

3. Now you are in the character editor, you can add your textures and edit the game attributes of your character


> # The attributes

At the left you have the character attributes, you can choose your mod name, the character id (DON'T USE AN ID THAT IS ALREADY USED IN THE GAME), the cheat code to get this character and other.
Other attributes modify the player statistics when you use this character, for example there are "sprint speed", "air gravity" and "jump speed".


> # The textures

To create your textures first copy-paste the template, go to "LAUNCHERPATH/resources/app/" and copy the folder named "template character".
Paste this folder where you want and rename it by you character name or other.

Next you need a program that edit .dds files, I use [Gimp](https://www.gimp.org/) but you can using other program if you want.

Now you can modify the textures in the folder that you have copy-pasted, if you view that there are files with just 1 pixel its normal because some assets require just a color so replace this pixel by the color that you want.


> # Adding lines to the .TXT file

WARN : **you need to know how the JSON syntaxe works**

All characters has a .txt file, the launcher auto-generate this file but if you want to add a custom line you can :

1. Save you character mod.
2. Open your mod folder at "GAME-PATH/KF-Files/mods/YOUR-MOD-NAME" and in this folder there is a mod.json file.
3. Open this file with a text editor (like the notepad for example) and you will see a json object. This object has an list named "attributes" and this list contain the lines that will be added to the .TXT game file. So you just need to add a string value in this list like "myvariable=5.2"
