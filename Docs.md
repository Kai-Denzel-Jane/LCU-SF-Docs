/ For get players characters :

    Global Character cPlayer1;
    Global Character cPlayer2;


// To declare variables :

    Number variableNumber(4);
    Number variableFloat(4.9);
    Text textVar("AAAA");
    Bool booleanVar(false);

// To get this variables in the code just enter her names :

    variableNumber > variableFloat

// So to get global variable there are this syntaxe :

    Global VariableType myVariableName;


// there are ";" in the end of a line like JS


// we can make if else code :

    if( true == true && false == true ) {
        // code
    } else {
        // code
    }

// if we do if(nobooleanvariable) that work like JS


// To wait seconds in the code there are the function Wait :

    Wait(200);


// In a character code, the var that make reference to the npc is "me" and to get it we need to make this :

    Character me(GetCharacter());


// In the character code i have found this, i think this is to attack the player :

    me.Attack(cPlayer1);


// We can make timer by this :

    Timer LineTimer(50);

    if( LineTimer < 2 ) {
        LineTimer.Reset(); // Reset the timer
    }

// To making class :

    State MyClassName()
    {
	    Conditions
	    {
		    if ( player.loveCheese() ) {
                // To execute a class in another use "goto ClassName();"
			    goto EatCheese();
		    };
	    };
	    Actions
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

// Make npc arestable :
    
    npc.SetArrestable(true);

// Start fight / battle with NPC :

    Character npc(GetCharacter()); / Character npc( CreateAICharacter( "Robber", "Criminal", lSpawnChar, 2) );

    Global AttackManager amEncounter1;

    npc.SetPushable(false);
    npc.SetInvulnerable(false);

    amEncounter1.AddAttacker(npc);


    // In general, there are the main first class in a code
    // named "Base" and at the end of the code we call it like this :

    State Base() {
    
	    Conditions
	    {
            
	    };
	    Actions
	    {

	    };
    }

    Base();

// To move npc :

    Locator lGoto ("ExitLift");
    npc.MoveTo(lGoto, 1, #STRAIGHTLINE);


// To get the nearest player

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

// To get if character is in a vehicle :

    character.InVehicle( vehicle )

// Spawn vehicle :

    Text vehicleType("Police_Rino"); // Put the vehicle name
    Locator vehicleSpawnLocation("");
    Number vehicleDirection(0);
    Character myCar("");


    vehicleSpawnLocation = "Mission01_CarSpawn";

    StreamedCharacterPreLoad(vehicleType); // Load vehicles


    Wait(1); // Wait for load vehicles

    myCar = CreateCharacter( vehicleType, vehicleSpawnLocation, "default", vehicleDirection);

// Spawn NPC :

    Locator lFrankSpawn("");

    lFrankSpawn = "Mission01_FrankSpawn";

    StreamedCharacterPreLoad("FrankHoney");
    Wait(1);
    nDirection = lFrankSpawn.GetDirection();
    cFrankHoney = CreateCharacter("FrankHoney", lFrankSpawn, "SM01_FrankArrive", nDirection);

// Make NPC moving to location :

    Global Locator gLocMoveTo("");
    Locator lMoveTo("Mission01_Frank_EnterVehicle");
    Text tMoveTo("moveToSubstitute");

    gLocMoveTo = lMoveTo;
    npc.SetScript( tMoveTo );

// Spawn AI in vehicle : (there are CreateAICharacter but there are too CreateAIVehicle)

    Text tFighterType("Collectable");

    fighter = CreateAICharacter("Bandit", tFighterType, fighterSpawnLocation, fighterSpawnLocation.GetDirection()  );
    fighter.MoveTo( lRunTo_05, 4, #STRAIGHTLINE );

    RegisterEvent("ArrivedAtTarget", "StartFight", fighter);

// Make npc down :

    npc.LockInPlace(true,"idle");
    npc.CutDownCharacter(true);

// Get a random number :
    RandomInt(1,3);


// Make a function :

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

// playing a sound :

    PlaySFX(sfx="UI_CodeBreak_CheatUnlocked");

// Show / print a text :

    UI_SetMissionMessage("PONG_NOT_READY", 4);
    PrintToScreen("Press A to tell Robber to Flee");


// Teleport a player / character :

    cPlayer1.Teleport(position (its a Locator), rotation (its a Number) );

// Change the sky :
    SetTimeOfDay(200);

// Get a key pressed :

    PlayerPressedButton("L3"); // return true / false
    PlayerPressedButton("A")

// Modify speed :

    v1 = cPlayer1.GetVehicle();
    if ( v1.GetSpeed() >  nDrivingVelocity )

// Activate the slow-motion :

    SlowMo( 4, 0.25 );

// Detect when npc is on the screen / window :

    npc.OnScreen()

// Make character opacity down to 0 :

    npc.FadeOut(2.3); // it will disable the opacity in 2.3 seconds