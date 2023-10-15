# KF-Launcher Mod API


> ## Get started

1. Create a folder in "YOUR-GAME-PATH/KF-Files/mods" a folder with the name of your mod (this is the name displayed on the app).

2. Open the new folder and add a file named "mod.json" in lowercase.

3. Open this file with the block note or a code editor.

4. Add this code :

        {
            "description": "mod description",
            "devmode": true
        }

5. You can edit the description to explain what your mod do (be sure to use a correct json syntaxe).

Now when you reload/restart the launcher your mod will be displayed, but your mod do nothing.
So go to the [section named features](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/KF-Launcher-Doc.md#list-of-features-) for learning how to add features to your mod.


> ## List of features :

### Inject SF scripts to the game :

Add a folder named "SF", in this folder add a file named "code.sf" and put in this file your script code.
To learn the .sf language you can go to this documentation by clicking [HERE](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/Docs.md).

**IMPORTANT** : the script are executed everywhere in the city.

**Note** : your file that include your code can be named by anything because when the launcher inject your file it make a file with another name.

### Create new characters :

The informations that you need to adding new characters are [HERE](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/Characters.md).

### Inject files into the game files :

Add a folder named "install".
In this folder, everything will be replaced when you enable your mod, example :
If you add in this folder a folder named "STUFF" and in the folder "STUFF" you add a file named "myfile.txt" when you enable your mod in the games file in the folder "STUFF" you can see your "myfile.txt".
**Note** : You don't need to backup your files because the launcher do it for you, if you disable your mod the launcher will put the old files.

### Add text into the list of text in the game

Add a folder named "text".
In this folder, you can add .txt files and in these files you can write a new line that will be added to the text list.
If you want to edit an existing line, add a "_" at the start of your file name, in this file you can write an line and the launcher will edit the line that starts with the same id.


### Execute JS code :

There is 2 methods :

1 : (Recommanded method) Execute your js file as a module so it will be executed by the nodeJS process of Kestrel-Fusion-Launcher

To do it add a folder named "js" and add in this folder your .js files.

IMPORTANT : Your js files must end with the character "_" else it don't will be launched as a module. (for example your file can be named "mycode\_.js")

For using the JS API go [HERE](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/JS-API.md)

2. Execute your js file forked by the launcher, the launcher will use the .fork() function but i don't recommand it.

To do it add "_fork" at the end of your file name.

### Execute python code :

**warn** : it don't work if the user haven't python

Add a folder named "python" and add in this folder your .py files.
To execute this file after that the game was started just add the character "\_" at the start of your python file.

### Execute bat script :

Add a folder named "bat" and add in this folder your .bat files.
To execute this file after that the game was started just add the character "\_" at the start of your bat file.