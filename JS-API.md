# JS API

**THIS WORK ONLY ON THE VERSION 1.3.0 OR MORE OF [KF-LAUNCHER](https://github.com/AntoineUserName/Kestrel-Fusion-Launcher/)**

# Get started

Warn : I recommend knowing how to use JS, if you are a beginner you can learn with this : [https://www.w3schools.com/js/js_syntax.asp](https://www.w3schools.com/js/js_syntax.asp)

1. First, create a mod. If you haven't did it all are explained [HERE](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/KF-Launcher-Doc.md#get-started)

2. In the folder of the mod, add a folder named "js" and add a file that a .js file that end with "_.js" it's important (don't forget the underscore "\_")

Tips : If you want that your file is executed after that the game is started add "_" at the start of the js file.

3. Now you have to code so you can start with this code base :

```js

exports.onStart = async () => {
    console.log("Hello world!");
}

exports.onClosed = async () => {
    console.log("Game stopped");
}
```

4. Interact with the game :


First, in the function "exports.onStart" add a "shortcut" for use easly the gameAPI object :

```js
exports.onStart = async () => {
    const gameAPI = exports.modInfos.gameScriptToJSAPI;
}
```

Actually you need to wait that the city is loaded AND that the mods are connected so after created the "shortcut" add this :

```js
gameAPI.onConnected(async()=>{
    console.log('mod connected!');
});
```

So you can replace the "console.log('mod connected!');" by a code that interact with the game!

For example if you want to teleport the player you can do this :

```js
// teleport the player to x=0 y=70 z=0 :
gameAPI.player.position.set(0, 70, 0);
```

You can also just increment the initial position like this :

```js
// Here "playerY" is equal to the Y player position
let playerY = gameAPI.player.position.getY();

// Adding 20 to the Y player position :
gameAPI.player.position.setY(playerY + 20);
```

Now you can teleport the player but there is more usefull, you can communicate with a custom .SF script!

To do this, first add a SF script to your mod by adding in your mod folder a folder named "SF" and in this new folder a text file with the extension ".SF"

In this file add this code :

    Global Character cPlayer1;
    Global Character cPlayer2;

    Function onJSMessage (CityArray textArgs, CityArray numberArgs) {
        // The first argument :
        Text actionType( textArgs.Get(0) );
    };

    State Base() {
        Conditions
        {
            @ifMessage "MY-MOD-ID" onJSMessage;
        };
        Actions
        {
        };
    };

    Base();

IMPORTANT : replace the "MY-MOD-ID" by a unique id which makes a reference to your mod, for example if you do a banana mod use "banana_mod", "banana_world" ....


Actually in this code the function "onJSMessage" is executed when you send a message by your JS code.

If you don't know how works the SF scripts there is a doc [HERE](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/blob/main/Docs.md)

So in your JS code add your mod id like this :

```js
let modId = "MY-MOD-ID"; // Replace "MY-MOD-ID" by the same id that you use in your .SF script
```

To interact you can do this :

```js
await gameAPI.sendMessage(modId, "jumping");
```

Now to intercept the message in the .SF script replace the "onJSMessage" function by this :

    Function onJSMessage (CityArray textArgs, CityArray numberArgs) {
        // The first argument :
        Text actionType( textArgs.Get(0) );

        if(actionType == "jumping") {
            PressButton(Character=cPlayer1, #Jump);
        }
    };

Actually your JS code tell to your .SF script to make the player jumping.

If you want you can send integers and floats :

In the JS code :

```js
await gameAPI.sendMessage(modId, "jumping");

await gameAPI.sendMessage(modId, "spawnNPC", 5); // Sending "spawnNPC" and the number 5
```

In the .SF script :

    Function onJSMessage (CityArray textArgs, CityArray numberArgs) {
        // The first argument :
        Text actionType( textArgs.Get(0) );

        if(actionType == "jumping") {
            PressButton(Character=cPlayer1, #Jump);
        }
        
        if(actionType == "spawnNPC") {

            // Get the first number sended (for the first use .Get(0), the second .Get(1) ...)
            Number numberOfNPCToSpawn( numberArgs.Get(0) );

            While( numberOfNPCToSpawn > 0) {
                numberOfNPCToSpawn = numberOfNPCToSpawn - 1;
                // Spawn NPC :
                CreateAiCharacter("FrankHoney", "Special", cPlayer1.GetPosition(), 0);
            }

        }
    };

Now you know how to use this api, if you want to know all the features I did a list of all functions here :


# All API Features

Detect when the mod is called

```js
exports.onStart = async () => {
    console.log("Hello world!");
}
```

Detect when the game is closed

```js
exports.onClosed = async () => {
    console.log("Game stopped");
}
```


**the gameAPI object**

To get the api

(do it in the exports.onStart function)

```js
const gameAPI = exports.modInfos.gameScriptToJSAPI;
```


Functions of connections :

```js
// The function gived will be executed when the JS-API is connected and reconnected(the API is reconnected when the player reload the city), if the JS-API is already connected the function will be directly executed
gameAPI.onConnected( async (ev) => {
    console.log('mod connected!');
    
    // To never execute this function again :
    ev.unsubscribe();
});

// The function gived will be executed when the JS-API is disconnected
gameAPI.onDisconnected( async (ev) => {
    console.log('mod disconnected');
    
    // To never execute this function again :
    ev.unsubscribe();
});
```

```js
gameAPI.isConnected() // Return true or false
```

Player functions :

```js
// **************************** The position : ****************************
const playerPos = gameAPI.player.position;

let posX = playerPos.getX();
let posY = playerPos.getY();
let posZ = playerPos.getZ();

playerPos.setZ(posZ + 5);

playerPos.set(-5, 70, 20);

// **************************** The rotation : ****************************
let playerRotation = gameAPI.player.rotation.get();
```

Interact with .SF scripts :

```js
const modId = "UNIQUE_MOD_ID";
await gameAPI.sendMessage(modId, "hello", 5, 1.3, "hello");

// the gameAPI.sendMessage() function return a promise, when the message is totally received the promise end
```