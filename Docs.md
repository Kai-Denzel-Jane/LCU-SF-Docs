# The basics :


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


# Interact with the game


For get players characters :

    Global Character cPlayer1;
    Global Character cPlayer2;


To get position and direction of a player :

    Position pPlayerPos;
    Number nPlayerRot;

    pPlayerPos = cPlayer1.GetPosition();
    nPlayerRot = cPlayer1.GetDirection();


Verify if city is loaded :

    WorldLevel wlCity("Lego_City");

    if( wlCity.IsLoaded() ) {};


Verify if this is safe to interrupt gameplay :

    if( wlCity.SafeToInterruptGameplay() ) {};


Declarate a position :
    Position myPosition(-180, 5, -221);

In a character code to get the reference to the npc we use the function "GetCharacter()" like this :

    Character me(GetCharacter());



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
    RegisterEvent("VehicleTakenDamage", "MyFunction", vehicle);

    


Make npc arestable :
    
    npc.SetArrestable(true);

Start fight / battle with NPC :

    Character npc(GetCharacter()); // Character npc( CreateAICharacter( "Robber", "Criminal", position, 2) );

    Global AttackManager amEncounter1("");

    npc.SetPushable(false);
    npc.SetInvulnerable(false);

    amEncounter1.AddAttacker(npc);
    
    npc.Attack(cPlayer1);

To get if an NPC is handcuffed :

    if( npc.InContext("Handcuffed") ) {}


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


Make npc flee an Character :

    npc.Flee( cPlayer1, speedNumber, #USEPARKOUR );


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

    // More info in the "basics" section

To move npc :

    Locator myLocator;
    npc.MoveTo(myLocator, 1, #STRAIGHTLINE);
    
    npc.MoveTo(cPlayer1, 1);

Get distance between 2 Locators / Characters :

    char1.DistanceTo(char2);
    loc1.DistanceTo(loc2);

    char1.DistanceToXZ(char2);
    loc1.DistanceToXZ(loc2);

Get x, y and z variables of position / locator :

    position.GetX();
    position.GetY();
    position.GetZ();


To get the nearest player

    Global Character cPlayer1;
    Global Character cPlayer2;

    if ( !cPlayer2 )
    {
        return cPlayer1;
    }
    else
    {
        if ( cPlayer1.DistanceTo( ennemyPos ) <= cPlayer2.DistanceTo( ennemyPos ) )
        {
            return cPlayer1;
        }
        else
        {
            return cPlayer2;
        };
    };

To get if character is in a vehicle :

    character.InVehicle( vehicle );

Eject character from vehicle :

    vehicle.ExitVehicle();

Spawn vehicle :
    
    StreamedCharacterPreLoad(vehicleType); // Load vehicle

    Wait(1); // Wait for loading vehicle

    Position vehiclePos(0, 1, 0);
    Number vehicleDirection(0);

    Vehicle vVehicle;
    vVehicle = CreateAiVehicle("Hero", "Enforcer", vehiclePos, vehicleDirection);
    // To get vehicle type and name, go to STUFF/AI/AITYPES.TXT

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


Make npc down :

    npc.LockInPlace(true,"idle");
    npc.CutDownCharacter(true);


playing a sound :

    PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");

Show / print a text :

    // Show 3 :
    UI_SetMissionMessage("MISSION_GENERIC_COUNTDOWN_3", 1 );
    // Show 2 :
    UI_SetMissionMessage("MISSION_GENERIC_COUNTDOWN_2", 1 );
    // Show 1 :
    UI_SetMissionMessage("MISSION_GENERIC_COUNTDOWN_1", 1 );
    
    PrintToScreen("Hello World"); // WARN this is possible that this function not work


Teleport a player / character :

    cPlayer1.Teleport(position (its a Locator), rotation (its a Number) );

Disable collisions of a character :

    npc.SetNoCollision(true);

Change the sky :

    SetTimeOfDay( "DAWN" );
    SetTimeOfDay( "NOON" );
    SetTimeOfDay( "DUSK" );

Get a key pressed :

    PlayerPressedButton("L3"); // return true / false
    PlayerPressedButton("A");

Get vehicle speed :

    v1 = cPlayer1.GetVehicle();
    if ( v1.GetSpeed() > nDrivingVelocity ) {};

Force character to enter into a vehicle :
    
    character.EnterVehicle( vehicle );

Destroy / Remove a vehicle :

    vehicle.Destroy();

Set vehicle traffic density :

    OverrideTrafficDensity(0); // Stop the traffic (1 or 0)
    KillSpawnedTraffic(); // Kill all traffic

Activate the slow-motion :

    SlowMo( 4, 0.25 );

Set screen opacity :

    FadeScreen(true); // If true : show screen If false : show black screen

Detect when npc is on the screen / window :

    npc.OnScreen();

Make character opacity down to 0 :

    npc.FadeOut(2.3); // it will disable the opacity in 2.3 seconds

Give coins / studs to player :

    PlayerGiveStuds( 5 );


Show and manager damage bar ui :
    
    Number maxPoints(5);
    Number totalPoints(2);

    UI_SetMissionDamageBarText("MISSION_COMBINE_HARVESTER_BAR_NAME");
    UI_ShowMissionDamageBar(true);

    UI_SetMissionDamageBar ( (maxPoints - totalPoints), maxPoints );
    }
    else // No ";" need here
    {
        myCode(); // Must finish with ";"
    }


We can make if else instructions like this :

    if( true == true && false == true ) {
        // code
    } else {
        // code
    }

if we do if(nobooleanvariable) that work like JS, for examples :

    if( null ) { // null == false
        // code
    }
    if( object ) { // if object is null => false else => true
        // code
    }


To wait seconds in the code there are the function Wait :

    Wait(200);


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

    Function myFunctionName () returns Bool // !! <-- "Bool" is the type returned, so if you want to return a number put "Number"
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


# Interact with the game


For get players characters :

    Global Character cPlayer1;
    Global Character cPlayer2;


To get position and direction of a player :
    Position pPlayerPos;
    Number nPlayerRot;

    pPlayerPos = cPlayer1.GetPosition();
    nPlayerRot = cPlayer1.GetDirection();


Declarate a position :
    Position myPosition(-180, 5, -221);

In a character code to get the reference to the npc we use the function "GetCharacter()" like this :

    Character me(GetCharacter());



Register an event :

    Function myFunctionName(Character cSplat)
    {
        PrintToScreen("aa");
    };

	RegisterEvent("eventName", "myFunctionName", cPlayer1 );

    // List of some events :

	RegisterEvent("ArrivedToBouncePadTarget", "myFunctionName", cPlayer1 );
    RegisterEvent("PlayerJackedVehicle", "fnGotInCar");
    RegisterEvent("PlayerExitedVehicle", "fnGotOutOfCar");
    RegisterEvent("PlayerVehicleHitProp", "fnCarHitProp");
    RegisterEvent("PlayerVehicleHitTraffic", "fnCarHitTraffic");
    RegisterEvent("PlayerVehicleAndAIVehicleCollision", "fnCarHitAIVehicle");
    RegisterEvent("PlayerVehicleHitKrawlie", "fnCarHitKrawlie");
    RegisterEvent("PlayerVehicleOnRoof", "function");
    RegisterEvent("PlayerVehicleWaterRespawn", "function");
    RegisterEvent("PlayerVehicleDestroyed", "function");
    RegisterEvent("PlayerVehicleNearlyWrecked", "function");
    RegisterEvent("PlayerVehicleJumping", "function");


Make npc arestable :
    
    npc.SetArrestable(true);

Start fight / battle with NPC :

    Character npc(GetCharacter()); // Character npc( CreateAICharacter( "Robber", "Criminal", locationSpawnChar, 2) );

    Global AttackManager amEncounter1("");

    npc.SetPushable(false);
    npc.SetInvulnerable(false);

    amEncounter1.AddAttacker(npc);
    
    npc.Attack(cPlayer1);


Get driver in a vehicle :
    vehicle.GetDriver();


Make npc flee an Character :
    npc.Flee( cPlayer1, speedNumber, #USEPARKOUR );


In general, there are the main first class in a code
Named "Base" and at the end of the code we call it like this :

    State Base() {
    
	    Conditions
	    {
            // Your code here
	    };
	    Actions
	    {
            // Your code here
	    };
    }

    Base();

To move npc :

    Locator myLocator;
    npc.MoveTo(myLocator, 1, #STRAIGHTLINE);
    
    npc.MoveTo(cPlayer1, 1);


To get the nearest player

    Global Character cPlayer1;
    Global Character cPlayer2;

    if ( !cPlayer2.IsOn() )
    {
        return cPlayer1;
    }
    else
    {
        if ( cPlayer1.DistanceTo( gNearestTo ) <= cPlayer2.DistanceTo( gNearestTo ) )
        {
            return cPlayer1;
        }
        else
        {
            return cPlayer2;
        };
    };

To get if character is in a vehicle :

    character.InVehicle( vehicle );

Eject character from vehicle :
    vehicle.ExitVehicle();

Spawn vehicle :
    
    StreamedCharacterPreLoad(vehicleType); // Load vehicle

    Wait(1); // Wait for loading vehicle

    Position pPlayerPos;
    Number nPlayerRot;

    pPlayerPos = cPlayer1.GetPosition(); // Position of the vehicle
    nPlayerRot = cPlayer1.GetDirection(); // Direction of the vehicle

    Vehicle vVehicle;
    vVehicle = CreateAiVehicle("Hero", "Enforcer", pPlayerPos, nPlayerRot);

Spawn NPC :

    Locator lFrankSpawn("");

    lFrankSpawn = "Mission01_FrankSpawn";

    StreamedCharacterPreLoad("FrankHoney");
    Wait(1);
    nDirection = lFrankSpawn.GetDirection();
    cFrankHoney = CreateCharacter("FrankHoney", lFrankSpawn, "SM01_FrankArrive", nDirection);

Make NPC moving to location :

    Locator locationGoal("Mission01_Frank_EnterVehicle");    
    npc.MoveTo( locationGoal );

Spawn AI in vehicle : (there are CreateAICharacter but there are too CreateAIVehicle)

    Text tFighterType("Collectable");

    fighter = CreateAICharacter("Bandit", tFighterType, fighterSpawnLocation, fighterSpawnLocation.GetDirection()  );
    fighter.MoveTo( lRunTo_05, 4, #STRAIGHTLINE );

    RegisterEvent("ArrivedAtTarget", "StartFight", fighter);

Make npc down :

    npc.LockInPlace(true,"idle");
    npc.CutDownCharacter(true);


playing a sound :

    PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");

Show / print a text :

    PrintToScreen("Hello World");


Teleport a player / character :

    cPlayer1.Teleport(position (its a Locator), rotation (its a Number) );

Disable collisions of a character :
	npc.SetNoCollision(true);

Change the sky :
    SetTimeOfDay(200);

Get a key pressed :

    PlayerPressedButton("L3"); // return true / false
    PlayerPressedButton("A");

Get vehicle speed :

    v1 = cPlayer1.GetVehicle();
    if ( v1.GetSpeed() >  nDrivingVelocity )

Set vehicle traffic density :
	OverrideTrafficDensity(0); // Stop the traffic

Activate the slow-motion :

    SlowMo( 4, 0.25 );

Detect when npc is on the screen / window :

    npc.OnScreen();

Make character opacity down to 0 :

    npc.FadeOut(2.3); // it will disable the opacity in 2.3 seconds
