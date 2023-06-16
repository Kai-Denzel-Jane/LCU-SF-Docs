# KF-Launcher Mod API


> ## Get started

1. Create a folder in "YOUR-GAME-PATH/KF-Files/mods" a folder with the name of your mod (this is the name displayed on the app).

2. Open the new folder and add a file named "mod.json" in lowercase.

3. Open this file with the block note or a code editor.

4. Add this code :

        {
            "description": "mod description"
        }

5. You can edit the description to explain what your mod do (be sure to use a correct json syntaxe).

Now when you reload/restart the launcher your mod will be displayed, but your mod do nothing.
So go to the file named features.md in the folder of the file that you actually read for learning how to add features to your mod.


> ## List of features :

### Inject SF scripts to the game :

Add a folder named "SF", in this folder add a file named "code.sf" and put in this file your script code.
To learn the .sf language you can go to this documentation by clicking [HERE](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/Docs.md).

**IMPORTANT** : the script are executed everywhere in the city.

**Note** : your file that includes your code can be named by anything because when the launcher inject your file it make a file with another name.

### Create new characters :

The informations that you need to adding new characters is [HERE](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/Characters.md).

### Inject files into the game files :

Add a folder named "install".
In this folder, everything will be replaced when you enable your mod, **example** :
If you add in this folder a folder named "STUFF" and in the folder "STUFF" you add a file named "myfile.txt" when you enable your mod in the games file in the folder "STUFF" you can see your "myfile.txt".
**Note** : You don't need to backup your files because the launcher do it for you, if you disable your mod the launcher will put the old files.

### Execute python code :

**warn** : it don't work if the user doesn't have python

Add a folder named "python" and add your .py files to this folder.
To execute the file after that the game was started just add the character "\_" at the start of your python file.

### Execute nodeJS code :

**warn** : it don't work if the user doesn't have nodeJS

Add a folder named "js" and add your .js files to this folder.
To execute the file after that the game has started just add the character "\_" at the start of your js file.


### Execute bat script :

Add a folder named "bat" and add your .bat files to this folder.
To execute the file after that the game was started just add the character "\_" at the start of your bat file.
