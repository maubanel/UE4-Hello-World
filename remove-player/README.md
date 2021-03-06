<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

### Remove Player Control

<sub>[previous](../building-h/README.md#user-content-build-the-letter-h) • [home](../README.md#user-content-ue4-hello-world)</sub>

<img src="https://via.placeholder.com/1000x4/45D7CA/45D7CA" alt="drawing" height="4px"/>

Unreal autoamtically loads up a player in most templates.  That is why we place a **player start** because the largest preponderances of games use a controllable character.  What about puzzle games, where the user is just clicking a user interface and not controlling a character (like a crossword puzzle)?  Lets look at how we can set-up a camera, have it rotate around the letter(s) and default to it when starting the game.

<br>

---


##### `Step 1.`\|`SUU&G`|:small_blue_diamond:

Instead of having the camera on the player pawn that spawns, lets have a predefined camera.  Go to **Modes** and type `Camera` and drag a **Camera** into the scene.  

In Unreal you can take any existing actor and turn it into a **Blueprint** that you can reuse or add extra logitc that doesn't exist in the current actor.  This can be done in the **Details** panel.

Now we want to make a blueprint to add logic to it so that it rotates around its center.  Click on the <kbd>Blueprint / Add Script</kbd> button and call it `BP_CameraActor`. In the ***Creaet Blueprint from Selection** menu leave the defaults and press the <kbd>Select</kbd>button. Add it to the **Content | LearningKit Games | Blueprints | Game Framework** folder."

![drag camera actor to level](images/AddCamToLevel.jpg)
![turn actor to BP](images/TurnActorToBP.jpg)
![turn actor to BP](images/NameCamBP.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 2.`\|`FHIU`|:small_blue_diamond: :small_blue_diamond: 

Open the newly created **Blueprint**.  In the **Components** tab, press the **+ Add Component** button and search for `Billboard`.  Add this component to the scene.  This will act as the target that the camera looks at but will not be rendered in the level.  It will stay at the local **0, 0, 0** coordinate so this will be the rotation point for the camera to rotate around the level.

![add billboard component to scene](images/AddBillboard.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 3.`\|`SUU&G`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press **+ Add Component** again and add a `Rotating Movement` component.

![add rotating movement component to scene](images/RotatingMovement.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 4.`\|`SUU&G`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

The camera needs to be around 3/4 of the length of the ground surface away from the billboard.  The billboard will be in the middle of the floor and the camera will look at it and rotate around it.  This will take some trial and error but for now select the **Camera Component** and move it away with the **Red** arrow from the **Billboard**.

![move camera away from billboard](images/MoveCamBack.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 5.`\|`SUU&G`| :small_orange_diamond:

Drag the **BP_Camera_Actor** to the scene.  Make sure the billboard component is at **Location** at the point where you want to rotate.  Make sure the **Camera Component** is far enough away.  Go back to the blueprint and adjust the distance.  Use the camera preview to see the framing of the camera. I have it here so that the object is position and rotated with the pivot point in the right place.

![adjust position of camera in scene](images/AdjustPosition.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 6.`\|`SUU&G`| :small_orange_diamond: :small_blue_diamond:

Now we do not want to spawn the third person character.  This can be found in the **Game Mode** blueprint. We do not want to change the existing one as it works with the existing levels in our game.  Go to the **LearningKit_Games | Blueprints | GameFramework** folder and press the <kbd>Add/Import</kbd> button and select <kbd>Blueprint Class</kbd>. Now select the <kbd>Game Mode Base</kbd> class for this blueprint.  Call this blueprint `BP_HelloWorldGameMode`.

![add blueprint to Game Framework folder](images/AddBlueprint.jpg)

![select gamemode base](images/GameModeBase.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 7.`\|`SUU&G`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Open up the game mode blueprint and change the **Default Pawn** to `none`.

![set default to none](images/SetDefaultToNone.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 8.`\|`SUU&G`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

There are two places we can select the level blueprint.  In the **Project Settings | Maps & Modes** we can set it for the entire project.  We will leave this alone as it works with their test level in the framework we imported.  

We can have a unique gamemode for a specific level.  This is done by going to the **World Settings** tab (if it is not there go to **Settings | World Settings**) and selecting this new game mode as the one we will use for this single level.

![global game mode in project settings](images/GameModeProjectSettings.jpg)

![open up world settings tab](images/WorldSettingsTab.jpg)

![select bp_helloworldgamemode](images/WorldSettingsCustomForLEvel.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 9.`\|`SUU&G`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press the **Play** button and we no longer see the third person pawn.  We DO NOT see the camera rotate around the object.  Woops the camera is static.  What is happening?  The game is still using the spectator pawn camera will not use this camera unless you tell it to. Notice it spawns a second camera that in my case points at nothing.  It must be bound to the **Default Pawn** as the camera moves when I press **WASD** on the keyboard.  

This is default behavior in Unreal. It expects the user the be controlling a character and since we do not have one, it creates one for us using the default pawn so you can fly around the scene.  Notice that in the **World Outliner** that you see the other **Camera Actor**.  You will also still see the **BP_CameraActor** and if you click on it will see that the frame is changing so it is rotating.

Lets fix this and use our desired camera.

![spawns new camera actor](images/SpawnsNewCamActor.jpg)

![cam bp still there not running](images/CamBPStillThere.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 10.`\|`SUU&G`| :large_blue_diamond:

Every level comes with its own blueprint where you can put level specific scripts.  When you save a map/level the game automatically creates a level blueprint.  This is where we will tell the game to use our new camera.  You can load it by pressing the <kbd>Blueprints</kbd> button and select **Open Level Blueprint**.


![open level blueprint](images/OpenLevelBP.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 11.`\|`SUU&G`| :large_blue_diamond: :small_blue_diamond: 

Now you can see that the blueprint has the same name as the map.  Make sure you are in the **Event Graph**, this is where all your game logic will go.  Notice the **Begin Play Event**.  This event will run **once** when you start the game.  So our script needs to make our new camera the game camera instead of the spectator pawn.  Right click on the graph and search for a **GetPlayerController** node.

![get player controller](images/GetPlayerController.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>


##### `Step 12.`\|`SUU&G`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Pull off of the **Return Value** pin and add a **Set View Target with Blend** node.

![set view target with blend](images/SetViewTargetWithBlend.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 13.`\|`SUU&G`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Go to the game window and select the Camera blueprint actor in the scene.

![select camera actor in game level](images/SelectCameraActor.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 14.`\|`SUU&G`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Go back to the **Blueprint** and right click on the graph.  Select **Create a Reference to BP_Camera**.  Connect the **Execution** pin from the **Begin Play** node and send it to the **Set View Target With Blend** execution pin.  Connect the output of the camera node to the **Get Player Controller** pin in the **Target** node. 

Connect the output of the camera node to the **New View Target** pin in the **Set View Target with Blend** node.

![create a camera reference](images/CreateCameraReference.jpg)

![cconnect pins](images/ConnectPins.jpg)

![cconnect view target](images/SetNewViewTarget.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 15.`\|`SUU&G`| :large_blue_diamond: :small_orange_diamond: 

Compile the blueprint then go to the game and press run.  The camera should now rotate around the billboard showing off your work.  It is a bit fast though..

https://user-images.githubusercontent.com/5504953/125641441-45be20f1-9b1b-45eb-83aa-5f01ea4a9406.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 16.`\|`SUU&G`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

Lets adjust the speed and position of the camera.  Open the **BP_Camera_Actor** blueprint.  Select the **Rotating Movement** component. Change the  **Rotation Rate | Z** value from `180` degrees per second to `20`.

https://user-images.githubusercontent.com/5504953/125643100-a0516b9e-2196-4926-8ca9-6cdefb5c2014.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 17.`\|`SUU&G`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:


Now to reverse the direction we just make it `-20` degrees per second on the **Rotation Rate | Z** value and the camera will rotate in the opposite direction.

https://user-images.githubusercontent.com/5504953/125643160-362f4528-c409-40ba-b814-123ea675062a.mp4

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

##### `Step 18.`\|`SUU&G`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Create the rest of the letters to spell out the words **Hello World**.  Play around with the different static meshes and effects they provide to make it look as cool as you can.  You might have to adjust the size of the letters so they all fit on the ground (or expand the ground plane). Your final project should look something like this. Make sure you name your files appropriately and put all your cubes in folders that are clearly labelled.

![alt text](images/.jpg)

<img src="https://via.placeholder.com/500x2/45D7CA/45D7CA" alt="drawing" height="2px" alt = ""/>

| `hello.world`\|`THE END`| 
| :--- |
| **That's All Folks!** Thanks for sticking around. That's it for this lesson. |

<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

<img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Complete!">

<img src="https://via.placeholder.com/1000x4/dba81a/dba81a" alt="drawing" height="4px" alt = ""/>

| [previous](../building-h/README.md#user-content-build-the-letter-h)| [home](../README.md#user-content-ue4-hello-world) | 
|---|---|
