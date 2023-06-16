# Inject my code in the game if I don't have [KF-Launcher](https://github.com/Kai-Denzel-Jane/LCU-SF-Docs/edit/dev/KF-Launcher-Doc.md) :

1. Add this line (in lowercase) into the file at LEVELS/LEGO_CITY/LEGO_CITY/AI/SCRIPT.TXT :

        level31

2. In the same folder, add a file named LEVEL31.SF (in uppercase)

3. Open the LEVEL31.SF file created with a code editor and start coding


# The basics :

Start your code :
In general, there are the main first class in a code
Named "Base" and at the end of the code we call it like this :

    State Base() {
    
	    Conditions
	    {
            // Your code here (executed every frames)
	    };
	    Actions
	    {
            // Your code here (execute one frame)
	    };
    }

    Base();


To declare variables :

    // For primitive variables :
    
    Number variableNumber(4);
    Number variableFloat(4.9);
    Text textVar("abcdef");
    Bool booleanVar(false);


    // For object of class variables :

    ClassName varName( functiontogetthisvariable() );
    Character npc(GetCharacter());
    Position myPos(2, 1, 3);
    Character characterNull; // < this variable is null



To get this variables in the code just enter her names :

    variableNumber > variableFloat

To set the value of a variable do this :

    variable = 5
    variable = true


there are ";" in the end of a line BUT if you missed a ";" the script can't work,
the ";" is only for instruction, example :

    if( true ) { // No ";" need here
        myCode(); // Must finish with ";"
    }
    else // No ";" need here
    {
        myCode(); // Must finish with ";"
    }


We can make if else instructions like this :

    if( true == true && false == true ) {
        // code
    } elseif( false ) {
        // code
    } else {
        // code
    }

if we do if(NOTBooleanVariable) that work like JS, for examples :

    if( null ) { // null == false
        // code
    }
    if( object ) { // if object is null => false else => true
        // code
    }


To wait seconds in the code there are the function "wait" :

    wait(2); // wait 2 seconds


So to get global variable there are this syntaxe :

    Global VariableType myVariableName;




To making class :

    State MyClassName()
    {
	    Conditions // !!   This is executed every frames
	    {
		    if ( player.loveCheese() ) {
			    // To execute a class in another use "goto ClassName();"
			    goto EatCheese();
		    };
	    };
	    Actions // !!   This is executed one frame
	    {
	    };
    };


    State EatCheese()
    {
	    Actions
	    {
		    player.EatCheese(8);
	    };
    };


Make a function :

    Function myFunctionName (text param1, number param2) returns Bool // !! <-- "Bool" is the type returned, so if you want to return a number put "Number"
    {
	    if ( true )
	    {
	    	    return true;
	    }
	    else
	    {
		    return false;
	    }
    }


Get a random number :

    RandomInt(1,3);
    RandomFloat(0, 2);

We can make timer by this :

    Timer LineTimer(50);

    if( LineTimer < 2 ) {
        LineTimer.Reset(); // Reset the timer
    }

Make a while loop :

    while( true == false ) {
        // code 1
    }
    // code 2
    // ! the code 2 is executed when the while loop is finish !


Make an array and using it :

    CityArray exampleArray;

    exampleArray = CityArray_Create("Number"); // Number is the type of values in this array

    exampleArray.Add(3); // Add 3 at the index 0
    exampleArray.Add(25); // Add 25 at the index 1
    exampleArray.Add(7); // Add 7 at the index 2

    exampleArray.Remove(3); // Remove value at the index 3

    exampleArray.Set(2, 123); // Set the index 2 at 123

    exampleArray.Get(2); // Return 123

    // Other misc functions:
    exampleArray.Clear(); // Empties the array
    exampleArray.Size(); // Returns size


# Interact with the game :


### Most common functions/variables used

For get players characters :

    Global Character cPlayer1;
    Global Character cPlayer2;


Verify if city is loaded :

    WorldLevel wlCity("Lego_City");

    if( wlCity.IsLoaded() ) {};


Verify if this is safe to interrupt gameplay :

    if( SafeToInterruptGameplay() ) {};


### Character objects

First, you need to know that players and npc are an object of the class "Character".

To get position and direction of a character :

    Position pPlayerPos;
    Number nPlayerRot;

    pPlayerPos = cPlayer1.GetPosition();
    nPlayerRot = cPlayer1.GetDirection();


Make npc arestable :
    
    npc.SetArrestable(true);


Start fight / battle with NPC :

    Character npc( CreateAICharacter( "Robber", "Criminal", position, 0) );

    Global AttackManager amEncounter1("");

    npc.SetPushable(false);
    npc.SetInvulnerable(false);

    amEncounter1.AddAttacker(npc);
    
    npc.Attack(cPlayer1);

To get if an NPC is handcuffed :

    if( npc.InContext("Handcuffed") ) {}


Make npc flee an Character :

    npc.Flee( cPlayer1, speedNumber, #USEPARKOUR );


To move npc :

    Locator myLocator;
    npc.MoveTo(myLocator, 1, #STRAIGHTLINE);
    
    npc.MoveTo(cPlayer1, 1);


Spawn NPC :

    Position npcPos(0, 1, 0);
    Number npcDirection(0);

    Character myNPC;
    
    StreamedCharacterPreLoad("npcname");

    Wait(1); // Wait to load the character

    // Make NPC without AI :
    myNPC = CreateCharacter("npcname", "npctype", npcPos, npcDirection);

    // Make npc with AI :
    myNPC = CreateAICharacter("npcname", "npctype", npcPos, npcDirection);

    // To get npc type and name, go to STUFF/AI/AITYPES.TXT

Make NPC moving to location :

    Position myPos(0, 0, 0);   
    npc.MoveTo( myPos, 2 );

Teleport a character :

    cPlayer1.Teleport(position (of the class Position), rotation (of the class Number) );

Disable collisions of a character :

    npc.SetNoCollision(true);

Make npc down :

    npc.LockInPlace(true, "idle");
    npc.CutDownCharacter(true);


Detect when npc is on the screen / window :

    npc.OnScreen();

Force character to enter into a vehicle you have 2 function :
    
    // IDK if there are a difference but you can use one of this 2 functions
    character.EnterVehicle( vehicle, #DRIVER );
    character.SetVehicle( vehicle, #DRIVER );

Play animation :

    character.PlayContextAnimation("celebration", 1);

To get the nearest player

    Global Character cPlayer1;
    Global Character cPlayer2;

    if ( !cPlayer2 )
    {
        return cPlayer1;
    }
    else
    {
        if ( cPlayer1.DistanceTo( myPos ) <= cPlayer2.DistanceTo( myPos ) )
        {
            return cPlayer1;
        }
        else
        {
            return cPlayer2;
        };
    };


In a character code to get the reference to the npc we use the function "GetCharacter()" like this :

    Character me(GetCharacter());

To get if character is in a vehicle :

    character.InVehicle( vehicle );



### Vehicle objects

Note : to set specific things of a vehicle (like the vehicle speed for example) you must put a Character in the vehicle and use functions on this character.


Spawn vehicle :
    
    StreamedCharacterPreLoad(vehicleType); // Load vehicle

    Wait(1); // Wait for loading vehicle

    Position vehiclePos(0, 1, 0);
    Number vehicleDirection(0);

    Vehicle vVehicle;
    vVehicle = CreateAiVehicle("Hero", "Enforcer", vehiclePos, vehicleDirection);
    // To get vehicle type and name, go to STUFF/AI/AITYPES.TXT

Make race pursuit :

    Global Character cPlayer1;
    Vehicle copCar;
    Character cCop;

    Position carPos(0, 0, 0);

    Function CopReady() {

        // Start the race when the cop is in vehicle :
        copCar.ForceMaxDetail(true);
        cCop.Pursue(cPlayer1, 15, #MATCHSPEED, #IGNORETRAFFICLIGHTS);
    }

    Function spawnNPC() {
        // Spawn the npc :
        cCop = CreateAICharacter("CopB", "Enforcer", carPos, 0);

        // Spawn his car :
        copCar = CreateAIVehicle("Hero", "Enforcer", carPos, 0);
        
        RegisterEvent("EnteredVehicle", "CopReady", cCop);
        
        // Put the npc into the car :
        cCop.EnterVehicle(copCar, #DRIVER);
    }

    spawnNPC();


Get driver in a vehicle :

    vehicle.GetDriver();

Get vehicle speed :

    v1 = cPlayer1.GetVehicle();
    if ( v1.GetSpeed() > nDrivingVelocity ) {};

Set vehicle speed :

    npcDriver.SetDriveSpeed( 4 );
    npcDriver.SetDriveToBoost(0.25);

Set and get health of vehicle :
    
    vehicle.GetHealth(#Max);
    vehicle.SetHealth(#Set, 4);

Drive vehicle to position :

    Position myPos(0, 0, 0);
    Number speed(5);

    characterNPC.DriveTo( myPos, speed, #STRAIGHTLINE );

Destroy / Remove a vehicle :

    vehicle.Destroy();

Set vehicle traffic density :

    OverrideTrafficDensity(0); // Stop the traffic (1 or 0)
    KillSpawnedTraffic(); // Kill all traffic


Eject character from vehicle :

    character.ExitVehicle();

Get if vehicle is on the screen :

    vehicle.OnScreen();

Make car invulnerable

    SetInvulnerable(myVehicle, true);

Let ai the control of the car :

    cActive.SetAiOverride(true);

Start a race pursuit without manually spawning car :

    Character playerToPursuit( cPlayer1 );

    // Make new car that spawn :
    AddTrafficVehicleModel(Name="Enforcer_Hero", #Common, PursueTarget=playerToPursuit, MaxInstances=1, MinSpeed=3.5, MaxSpeed=4.5, CanSpawnParked=0, #IgnoreRoadRules, #ShowOnMap, #Overwrite);
    
    // Make these cars dangerous :
    EnablePursueFromTraffic("Hero", "Enforcer", 20.0, 2, playerToPursuit, 3, #SHOWONDRC);

Stop a pursuit :

    DisablePursueFromTraffic(tPursuitVehicleType1, tPursuitVehicleClass1, #DESTROYPURSUERS);
    DisablePursueFromTraffic("Hero", "Enforcer", #DESTROYPURSUERS);

### Position objects

Declarate a position :

    Position myPosition(-180, 5, -221);

Get distance between 2 Characters :

    char1.DistanceTo(char2);

    char1.DistanceToXZ(char2); // Get the distance without including the Y axe


Get x, y and z variables of position / locator :

    position.GetX();
    position.GetY();
    position.GetZ();



### Random things


Register an event :

    Function myFunctionName(Character cSplat)
    {
        // code
    };

    RegisterEvent("eventName", "myFunctionName", cPlayer1 );

    // List of some events :

    RegisterEvent("ArrivedToBouncePadTarget", "myFunctionName", cPlayer1 );
    RegisterEvent("PlayerJackedVehicle", "function");
    RegisterEvent("PlayerExitedVehicle", "function");
    RegisterEvent("PlayerVehicleHitProp", "function");
    RegisterEvent("PlayerVehicleHitTraffic", "function");
    RegisterEvent("PlayerVehicleAndAIVehicleCollision", "function");
    RegisterEvent("PlayerVehicleHitKrawlie", "function");
    RegisterEvent("PlayerVehicleOnRoof", "function");
    RegisterEvent("PlayerVehicleWaterRespawn", "function");
    RegisterEvent("PlayerVehicleDestroyed", "function");
    RegisterEvent("PlayerVehicleNearlyWrecked", "function");
    RegisterEvent("PlayerVehicleJumping", "function");

    RegisterEvent("AllGoldBricksCollected", "function");

    RegisterEvent("VehicleTakenDamage", "MyFunction", vehicle);
    RegisterEvent("ArrivedAtTarget", "function", charDriver); // Work with the drivers


Show / print a text :

    // Show 3 :
    UI_SetMissionMessage("MISSION_GENERIC_COUNTDOWN_3", 1 );
    // Show 2 :
    UI_SetMissionMessage("MISSION_GENERIC_COUNTDOWN_2", 1 );
    // Show 1 :
    UI_SetMissionMessage("MISSION_GENERIC_COUNTDOWN_1", 1 );
    
    PrintToScreen("Hello World"); // WARN this is possible that this function not work


Show and manage damage bar ui :
    
    Number maxPoints(5);
    Number totalPoints(2);

    UI_SetMissionDamageBarText("MISSION_COMBINE_HARVESTER_BAR_NAME");
    UI_ShowMissionDamageBar(true);

    UI_SetMissionDamageBar ( (maxPoints - totalPoints), maxPoints );

Change the sky :

    SetTimeOfDay( "DAWN" );
    SetTimeOfDay( "NOON" );
    SetTimeOfDay( "DUSK" );

Get a key pressed :

    PlayerPressedButton("L3"); // return true / false
    PlayerPressedButton("A");


Activate the slow-motion :

    SlowMo( 4, 0.25 );


playing a sound :

    PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");

Set screen opacity :

    FadeScreen(true); // If true : hide screen If false : show screen

Make character opacity down to 0 :

    npc.FadeOut(2.3); // it will disable the opacity in 2.3 seconds

Give coins / studs to player :

    PlayerGiveStuds( 5 );

Play battle music :

    PlayActionMusic( true );

Panic all pedestrian :

    TriggerKrawliesMassPanic(position, 7.5);
