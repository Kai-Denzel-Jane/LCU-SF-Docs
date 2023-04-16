# The basics


To declare variables :

    // For primitive variables :
    
    Number variableNumber(4);
    Number variableFloat(4.9);
    Text textVar("abcdef");
    Bool booleanVar(false);


    // For object of class variables :

    ClassName varName( functiontogetthisvariable() );
    Character npc(GetCharacter());
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
