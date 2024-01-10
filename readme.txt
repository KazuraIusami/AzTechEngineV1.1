Project Started 8-12-2023 by UngaBunga Studios

For the record, we lost our third 'A' during a company garage sale where it was not meant to be sold. Thus, we are not a Triple A game company, but double A. Hopefully the scoring system works like golf. (This is a joke btw...)

HOW TO RUN: Go to https://github.com/KazuraIusami/Wendigo/tree/main and look for the green button called " <> CODE ", then click "DOWNLOAD ZIP." Extract to where ever you want, open the folder and launch "index.html" For the best experience, press F11 to go full screen. Enjoy! Thank you for playing!

DEV NOTES :

() The whole folder labeled "OG" is just the pre-created thing I made, not very useful. Title, logo, and prompt made in krita

() 10/27/23 Good foundation built for the Aztech engine. 

-Created a class called "Entity" to use to link sprites and data to the creature. 
Entity( URL, xPOS, yPOS, TYPE, NAME) URL = Source for entity sprite xPOS & yPOS = data values for placement TYPE = (MONSTER/NPC/PLAYER) NAME = Both gives the creature a name and makes it the ID of the sprite, linking them together
 -Created a class for a dev toolkit as well as a keylogger than toggles its visibility using Escape

() 11/1/23 CONTROLS So far, I have a developers log that can be toggled on and off using "Escape." Inside of it are (as of writing this) two buttons. Spawn player, and Clear All Entities 
Dev Note: Recently got rid of a "spawn random enemy" button due to some errors with EntityList array. Work to be done soon The "Player" sprite that spawns when you click "Spawn Player" in the dev log can be clicked! In which case, it will follow the mouse cursor around the browser screen! 
Using the great art by https://www.instagram.com/guiigs.art/ for the sprite I have been calling "Wendigo"

() 11/3/23 Got directional movement set up to work with sprites, as well as working with facedDirection so I can have Idle animations 
-Press SHIFT to speed up movement of selected sprite 
-Click on sprite to "pin" it in the spot you click.
-Major developements to the Entity Class such as taking urlFolder and dynamically choosing the appropriate gif based on functional variables like facedDirection
-Dev Tools now has two rooms, one for a Monster to spawn in the middle of the screen (useful for testing combat mechanics) and one for NPCs which can be used for other tests

()11/5/23 Created a pretty good foundation for rooms. Basically, using the devlog you have to spawn player, then you can spawn any of the rooms listed. The first room and second room is still pretty much the same as it was in the last dev log, but now I have a fun little "prison" scenario. And with that, INTRODUCING
	CONVERSATION TREES!
	When spawning a room with the dev log, I am hand creating each entity within the room. Much like the source engine loads maps and such, the rooms are the maps. When creating the entity, I am giving it a "conversationTree" tag. Eventually, I will make this more complicated. It will HOPEFULLY resemble 
	the fallout engine conversation tree. I have done it before, I can do it again:)

()11/14/23 Conversation Trees are basically implemented, after LOTS of trial and error. To think I thought of it as simple. HOPEFULLY there arent any cracks in it. Basically my biggest problem was having it update too fast?
	So basically, when I spawn a room, I also specify what entities are in the room. If the name matches up to a conversation tree in the list, and the player interacts with it, it should just "work"
	Also got the second sprite, hopefully the main character I am calling "Eugene Galliga".
	Also, extra little dev note: Im not actually having the player interact with the walls. The walls are not entities, and so do not exist in the collision list. I am straight up saying "if the player is outside limits => dont"
		now, this isnt a BAD thing...its just important to keep this in mind through further iterations

() 11/18/23 
	-Screwing around a lot with events. Made room 5, which is the outside of a house (background crudely made by me), and when you walk into the door (EntityList[0].x & y are near door), the background changes and the same listeners from room 4 are applied. This is done by hand, as the rooms are all
	     engineered inside the dev log. The dev log is almost becoming a console, but that would complicate things
	-Getting death animations made for the characters, and also working on getting death listeners to work.
	-Inventory system is pretty much working, although I am still inexperienced with using it in my code first try.
	-WASD controls are also working pretty well, although there are still plenty of bugs. There are often times the character will  get stuck moving in a direction (I assume because of problems in the pressedKeys array)


() 11/21/23
	-Big news! Its possible with gifs to play once and then stop. That is huge news, because it would look really weird if the characters would die, then be back up, then die again. although that is a funny thought
	-Starting work on rooms. Currently creating a class for rooms, and a function to load these rooms. 

() 11/29/23
	I created a backup folder so that I could try scraping a chunk of the rooms and remake them using the new room class. I'm pretty sure it was successful, didnt somehow destroy the code while trying to redesign it. So heres how the room class works
	room( ImgURL, outerLimits, EntitiesToSpawn, SpawnPoint, staticCollisions)
	ImgURL = background image for the room (think pre-rendered backgrounds from the resident evil games)
	outerLimits = map Limits to stop the player from breaking the walls. In the format of {xMax: 1980, xMin: 0, yMax: 1280, yMin: 0 }, where xMax is the furthest right a player can go, and yMax is the furthest down a player can go
	EntitiesToSpawn = Experimental variable, ideally an array, that holds objects to create entities. (SEE ENTITIES TO SPAWN)
	SpawnPoint = Place for the player to spawn
	staticCollisions = Experimental variable, ideally an array, that holds objects to create collision points around the map. (SEE STATIC COLLISIONS)

		ENTITIES TO SPAWN: 
			let testEntitiesToSpawn = [
				{urlFolder, x, y, size, type, name, facedDirection, linkToConversationTree},
				{urlFolder, x, y, size, type, name, facedDirection, linkToConversationTree},
				...
			]
		STATIC COLLISIONS:
			let testStaticCollisions2 = [
				{xMin: 650, xMax: 1260, yMin: 0, yMax: 440}, 
				{xMin: 490, xMax: 650, yMin: 50, yMax: 160} 
			];


	The room class has a method called "generate()" which serves to "set the current room to the targeted one." There were a few complications at first, because the generate method was clearing all entities and then spawning the player again, which re-initialized the inventory. So, the generate
	method doesnt use the global "clearEntities()" function, instead, it clears ALL ENTITIES AFTER EntityList[0].

	Working on developing a better combat engine. At the moment, if the program detects two entities colliding, it checks to see if one is the player, and if it is, it checks too see if the other is a monster or an NPC...yadda yadda.
	While this works for "walk into combat", that can be very boring. So I added a very basic click function to the entity class. While "click combat" isnt a whole lot better than "walk into combat," it is a step in the right direction.

() 11/30/23
	Changed the way the Inventory is rendered. 
		BEFORE: Anytime an enemy is killed, give loot and set inventory.
		AFTER: There is an interval now attached to the player that is constantly setting the inventory to the current state of the inventory. MUCH better.
 
() 11/4/23
	Talking to a story writer about helping to write for this, very excited about that. Also working on building some test locations and refining the code. Started working on a location for the bar. Using an AI image, so its still WIP, but there are a few things I wanna try to get right. Story writer had the idea of 
		Wendigo always being there, except being invisible until the player drinks. I REALLY liked this idea because I also want it to be possible to play in "pacifest mode" and not see Wendigo. So I created a variable called "drunkMeter". This is not permanant and I need to make this better
	
() 12/6/23
	Got started building pre rendered backgrounds in blender, pretty simple work but its not easy. 
	I also got some of the bottle sprites, very interesting stuff. 
	Also working to give the inventory element the same "move around" capability, its been a little more difficult than I originally thought, but this is mostly just quality of life stuff.

() 12/10/23
	Still havent gotten the inventory the same functionality as the conversation node. Still needs attention.
	BUT, I added a select tag to the devkit that has a list of the rooms, along with a submit button that will automatically generate the room. HOWEVER, it does look like it would hinder me from being able to script things the same way. Currently, I am doing a LOT of the scripting
		in the same function that I load the room in. Its not really the best way to do things, but I am worried that it will cost me a lot more creative control I want to let down.
	I spent a little while tinkering with the combat system, and I ended up really changing the way I was doing it.
		BEFORE: When two entities ring true on CheckCollision, wildly decrease both entities health based on the attack. I had no control over how fast the attacks where happening, and it may have even been directly linked to FPS (in the computer, not the engine). 
		AFTER: When two entities ring true on CheckCollision, call the startAttack method, which is constantly checking to see if the "attack interval is active." If it is, then we do nothing. If not, then we start one and call it active so it wont keep on creating them. This is also where loot is managed.
			Also, added another method to the Entity class. The distanceToEntity(target) method is similar to the distanceToTarget variable also attached to the Entity class, however it actually uses Pythagorean formula to get its distance. It uses this to test whether or not the
			Entities are close enough to continue attacking.
	Also added a roomName variable to the room class, in order to make the select tag work.

() 12/11/23
	Dedicating time to plan the door addition to the room class. I think I will have an array for every room that starts empty, and then a method called addDoor which will add an Interval to the array that will check for door collision. And when I change rooms, I can use the array to clear all the intervals.
	Hopefully thats a sound plan.

	Okay, so the room class now has a method called addRoom. It has the arguments : (xMin, xMax, yMin, yMax, destination). I also have a "link doors" function to call after the rooms have been created. The linkDoors function is interesting, because it just starts an interval that will end itself and generate the next 
		room. Then, in the generate function, the linkDoors function is called. Almost seamless.
	Also added a really fun little test function set, takeBeer() and placeBeer()

() 12/19/23
	Been doing a lot of QoL stuff, and just getting a better understanding of what I have thus far. 
	I am dedicating time to change how the direction faced with the entities works. Its a strange thing to put time toward, but itll be worth it.
	BEFORE: When trying to move diagonally, the sprite would revert to the idle position. This was happening because the distanceToTarget.x and distanceToTarget.y were the same and that makes the computer wizards angry.
	AFTER: The program instead sets the direction faced only, and THEN checks to see if the distance is greater than 1 on either axis. If it is, set it to the walking animation. The faced direction happens because of the already existing code.

() 12/20/23
	Discovered a strange bug where Wendigo isnt despawning when I leave the bar...work to be done.

	Also discovered  hue-rotate in css so of course I added a "drunk effect" to eugene where his colors cycle through. Kinda fun and quirky but its nothing special. I am considering using this to create some sort of "magic" system or something?

() 12/24/24
	The previous bug where the Entity List wasnt clearing is fixed, pretty sure it had a lot to do with the clearEntities function, so I changed it a little bit "let i = EntityList.length ; i > 0; i--" So it goes DOWN the entity list rather than up. Little bit more effecient plus to wont remove the player.
	
	I changed the fun little test function takeBeer() and placeBeer() to instead be takeEntity(entityName) and placeEntity(entityName). Still not perfect, as putting down a bottle doesnt apply the conversation tree yet, and the functions need to be called manually from the console...but that would be an easy plug and play
	Added a new interval to the entity class that is constantly making the this.attackPower = (weapon.tier * weapon.type)*(weapon.tier * weapon.type);

	Yep, time for weapons and stuff. So get your glasses on old man, time to read up. 
	A weapon is an object with three main variables. I DO NOT have a class set up for weapons yet, although that might come later. So far it is just an object assigned to an entity under the this.weapon name. 
	this.weapon = {NAME, TIER, TYPE}
	A weapons damage is calculated as this.attackPower = (weapon.tier * weapon.type)*(weapon.tier * weapon.type); or dmg=(tier*type)squared. Eventually, I want the entity to be given a strength value to decides what PERCENT OF FULL DAMAGE TO DO.

() 1/1/24
	Working on the "distance seizure" glitch. Basically, if I set the players movespeed to anything above 1, then the player will spaz out rather than stop. Kind of hard to really explain, but it is an intuitive problem. If my movespeed is 2, and my target is 1 away, then I can ONLY overshoot it. 

() 1/2/24
	Still need to work on the distance seizure glitch, its a tough shell to crack. Also trying something interesting. Basically, I want to make the Entity size dependant on the y value, which would give the illusion of distance between the camera and the entity. Big problems though, as changing the size of the entity will also 
	make it go a little to the left...and it isnt as simple as adding half of the size to the x, as much as I wish that would work.

() 1/10/24
	Progress is slow, but I have added a weapon selector with a weapon container that you can choose from in the dev tools. Still fun. But the size thing is still a big problem. 
