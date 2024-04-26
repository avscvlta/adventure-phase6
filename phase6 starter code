//Adventure Game
//Phase5 - Caves

document.body.style.zoom = "300%";
document.addEventListener("keydown",keyDownHandler, false);
document.addEventListener("keyup",keyUpHandler, false);

let canvas = document.getElementById("gameCanvas");
let ctx = canvas.getContext("2d");
let fps = 60;
let mapTiles = new Image();
mapTiles.src = "overworld.png";
let hero = new Image();
hero.src = "hero.png";
let rightPressed = false;
let leftPressed = false;
let upPressed = false;
let downPressed = false;
let lastButtonPressed = "up";
let animationCounter = 0;
let currentAnimation = 0;
let animationheroSpeed = 0;
let heroX = 116;
let heroY = 130;
let heroSpeed = 2;
//map
let leftTileEdge = 0;
let rightTileEdge = 0;
let topTileEdge = 0;
let bottomTileEdge = 0;
let leftCollapse = 6;
let rightCollapse = 7;
let topCollapse = 13;
let bottomCollapse = 3;
let mapColumns = ["A","B","C","D","E","F","G","H","I","J","K","L"];
let currentColumn = 6;
let currentRow = 8;
let currentMap = mapG8;
let currentMapName = "map" + mapColumns[currentColumn] + currentRow;
// HUD
let hudBackground = new Image();
hudBackground.src = "hud.png";
let healthSprite = new Image();
healthSprite.src = "health.png";
let maxHealth = 3;
let currentHealth = 3;
let attackSprite = new Image();
attackSprite.src = "attack.png";
let defenseSprite = new Image();
defenseSprite.src = "defense.png";
let currentDefense = [0,0,0,0];
let prizeSprite = new Image();
prizeSprite.src = "prize.png";
let currentPrize = 0;
// Asset Caves
let healthCaveEntranceX = 0;
let healthCaveEntranceY = 0;
let itemCaveEntranceX = 0;
let itemCaveEntranceY = 0;
let previousMap = mapG8;
let heroExitX = 0;
let heroExitY = 0;
let heroInHealthCave = false;
let heroInItemCave = false;
let healthInCave = false;
let healthX = 120;
let healthY = 120;
let itemX = 120;
let itemY = 120;
let healthMap;
let healthLocations = [
	["mapG7",true],//reg1a
	["mapI4",true],//reg1b
	["mapJ7",true],//reg1c
	["mapE7",true],//reg2a
	["mapD6",true],//reg2b
	["mapC7",true],//reg2c
	["mapC2",true],//reg3a
	["mapB5",true],//reg3b
	["mapE5",true],//reg3c
	["map",true],//reg4a
	["map",true],//reg4b
	["map",true] //reg4c
	]
let itemLocations = [
	["mapG8",false],//att reg1
	["mapL8",false],//def reg1
	["mapA8",false],//att reg2
	["mapC5",false],//def reg2
	["mapA1",false],//att reg3
	["mapD1",false],//def reg3
	["map",false],//att reg4
	["map",false] //def reg4
]
let currentAttack = 0;
let attackDamage = [1, 2, 4, 10];

function overworldBuilder()
{
	if(heroX < - 8 && lastButtonPressed == "left")
	{
		heroX = 248;
		currentColumn = currentColumn - 1;
		currentMap = eval("map" + mapColumns[currentColumn] + currentRow); //need function for all this
		currentMapName = "map" + mapColumns[currentColumn] + currentRow;
		mapHitCreator();
		healthCaveEntranceX = 0;
		healthCaveEntranceY = 0;
		itemCaveEntranceX = 0;
		itemCaveEntranceY = 0;
		currentMapEnemies = eval("enemyProfile" + enemyProfileAssignments[currentMapName]);
		createEnemies();
	}
	if(heroX > 248 && lastButtonPressed == "right")
	{
		heroX = -8;
		currentColumn = currentColumn + 1;
		currentMap = eval("map" + mapColumns[currentColumn] + currentRow);
		currentMapName = "map" + mapColumns[currentColumn] + currentRow;
		mapHitCreator();
		healthCaveEntranceX = 0;
		healthCaveEntranceY = 0;
		itemCaveEntranceX = 0;
		itemCaveEntranceY = 0;
		currentMapEnemies = eval("enemyProfile" + enemyProfileAssignments[currentMapName]);
		createEnemies();
	}
	if(heroY < 58 && lastButtonPressed == "up")
	{
		heroY = 226;
		currentRow = currentRow - 1;
		currentMap = eval("map" + mapColumns[currentColumn] + currentRow);
		currentMapName = "map" + mapColumns[currentColumn] + currentRow;
		mapHitCreator();
		healthCaveEntranceX = 0;
		healthCaveEntranceY = 0;
		itemCaveEntranceX = 0;
		itemCaveEntranceY = 0;
		currentMapEnemies = eval("enemyProfile" + enemyProfileAssignments[currentMapName]);
		createEnemies();
	}
	if(heroY > 226 && lastButtonPressed == "down")
	{
		heroY = 60;
		currentRow = currentRow + 1;
		currentMap = eval("map" + mapColumns[currentColumn] + currentRow);
		currentMapName = "map" + mapColumns[currentColumn] + currentRow;
		mapHitCreator();
		healthCaveEntranceX = 0;
		healthCaveEntranceY = 0;
		itemCaveEntranceX = 0;
		itemCaveEntranceY = 0;
		currentMapEnemies = eval("enemyProfile" + enemyProfileAssignments[currentMapName]);
		createEnemies();
	}
}

function keyDownHandler(event)
{
	if(event.keyCode == 37)
	{
		leftPressed = true;
		lastButtonPressed = "left";
	}
	else if(event.keyCode == 39)
	{
		rightPressed = true;
		lastButtonPressed = "right";
	}
	else if(event.keyCode == 38)
	{
		upPressed = true;
		lastButtonPressed = "up";
	}
	else if(event.keyCode == 40)
	{
		downPressed = true;
		lastButtonPressed = "down";
	}
}

function keyUpHandler(event)
{
	if(event.keyCode == 37)
	{
		leftPressed = false;
	}
	else if(event.keyCode == 39)
	{
		rightPressed = false;
	}
	else if(event.keyCode == 38)
	{
		upPressed = false;
	}
	else if(event.keyCode == 40)
	{
		downPressed = false;
	}
}

function drawHero()
{
	// speed removed
	animationCounter++;
	
	if(leftPressed && !collision(heroX - heroSpeed, heroY, currentMap))
	{
		heroX -= heroSpeed;
		if(currentAnimation == 0)
		{
			ctx.drawImage(hero, 16, 0, 16, 16, heroX, heroY, 16, 16)
		}
		else if(currentAnimation == 1)
		{
			ctx.drawImage(hero, 16, 16, 16, 16, heroX, heroY, 16, 16)
		}
		if(animationCounter >= 6)
		{
			currentAnimation++;
			animationCounter = 0;
			if(currentAnimation > 1)
			{
				currentAnimation = 0;
			}
		}
	}
	else if(rightPressed && !collision(heroX + heroSpeed, heroY, currentMap))
	{
		heroX += heroSpeed;
		if(currentAnimation == 0)
		{
			ctx.drawImage(hero, 48, 0, 16, 16, heroX, heroY, 16, 16)
		}
		else if(currentAnimation == 1)
		{
			ctx.drawImage(hero, 48, 16, 16, 16, heroX, heroY, 16, 16)
		}
		if(animationCounter >= 6)
		{
			currentAnimation++;
			animationCounter = 0;
			if(currentAnimation > 1)
			{
				currentAnimation = 0;
			}
		}
	}
	else if(upPressed && !collision(heroX, heroY - heroSpeed, currentMap))
	{
		heroY -= heroSpeed;
		if(currentAnimation == 0)
		{
			ctx.drawImage(hero, 32, 0, 16, 16, heroX, heroY, 16, 16)
		}
		else if(currentAnimation == 1)
		{
			ctx.drawImage(hero, 32, 16, 16, 16, heroX, heroY, 16, 16)
		}
		if(animationCounter >= 6)
		{
			currentAnimation++;
			animationCounter = 0;
			if(currentAnimation > 1)
			{
				currentAnimation = 0;
			}
		}
	}
	else if(downPressed && !collision(heroX, heroY + heroSpeed, currentMap))
	{
		heroY += heroSpeed;
		if(currentAnimation == 0)
		{
			ctx.drawImage(hero, 0, 0, 16, 16, heroX, heroY, 16, 16)
		}
		else if(currentAnimation == 1)
		{
			ctx.drawImage(hero, 0, 16, 16, 16, heroX, heroY, 16, 16)
		}
		if(animationCounter >= 6)
		{
			currentAnimation++;
			animationCounter = 0;
			if(currentAnimation > 1)
			{
				currentAnimation = 0;
			}
		}
	}
	else	
	{
		if(lastButtonPressed == "down")
		{
			ctx.drawImage(hero, 0, 32, 16, 16, heroX, heroY, 16, 16)
		}
		else if(lastButtonPressed == "up")
		{
			ctx.drawImage(hero, 32, 32, 16, 16, heroX, heroY, 16, 16)
		}
		else if(lastButtonPressed == "right")
		{
			ctx.drawImage(hero, 48, 32, 16, 16, heroX, heroY, 16, 16)
		}
		else if(lastButtonPressed == "left")
		{
			ctx.drawImage(hero, 16, 32, 16, 16, heroX, heroY, 16, 16)
		}
	}
}

function tileEdgeFinder(mapArrayIndex)
{
	leftTileEdge = (mapArrayIndex%16) * 16;
	rightTileEdge = leftTileEdge + 16;
	topTileEdge = Math.floor(mapArrayIndex/16) * 16 + 64;
	bottomTileEdge = topTileEdge + 16;	
}

function drawMap(level)
{
	for(let i=0; i < level.length; i++)
	{
		tileEdgeFinder(i);
		ctx.drawImage(mapTiles,
		(((level[i]-1)%10) *16), //x location on overworld.png
		(Math.floor((level[i]-1)/10)) *16, //y location on overworld.png
		16, 16, leftTileEdge, topTileEdge, 16, 16);
	}
}

function collision(x, y, map)
{
	for(let i=0; i < map.length; i++)
	{
		tileEdgeFinder(i);
		if(
		map[i] != 4 &&
		map[i] != 8 &&
		map[i] != 10 &&
		map[i] != 34 &&
		map[i] != 40 &&
		map[i] != 64 &&
		map[i] != 65 &&
		map[i] != 70 &&
		map[i] != 74
		) //don't check collision on these tiles
		{
			if(
				x + leftCollapse <= rightTileEdge &&
				x + 16 - rightCollapse >= leftTileEdge &&
				y + topCollapse <= bottomTileEdge &&
				y + 16 - bottomCollapse >= topTileEdge
			)
			{
				return true; //collison is occuring
			}
		}			
	}
}

function drawHUD()
{
	ctx.drawImage(hudBackground, 0, 0, 256, 64, 0, 0, 256, 64); //draw HUD background
	for(let i = 0; i <= 15; i++) //draw 16 uncollected health
	{
		ctx.drawImage(healthSprite, 32, 0, 16, 16, i*16, 48, 16, 16);
	}
	for(let i = 0; i <= maxHealth - 1; i++) //draw collected health
	{
		ctx.drawImage(healthSprite, 16, 0, 16, 16, i*16, 48, 16, 16);
	}
	for(let i = 0; i <= currentHealth - 1; i++) //draw current health
	{
		ctx.drawImage(healthSprite, 0, 0, 16, 16, i*16, 48, 16, 16);
	}
	for(let i = 0; i < 7; i = i+2) //draw attacks
	{
		if(itemLocations[i][1] == true)
		{
		ctx.drawImage(attackSprite, i*16, 0, 32, 32, 16, 16, 32, 32); // current attack
		ctx.drawImage(attackSprite, 16 * ((i/2)%2) + 128, Math.floor(i/4) * 16, 16, 16, 48 * ((i/2)%2), (Math.floor(i/4) + 1) * 16, 16, 16); // collected attacks
		}
	}
	for(let i = 1; i < 8; i = i+2) //draw defense
	{
		if(itemLocations[i][1] == true)
		{
		ctx.drawImage(defenseSprite, (i-1)*16, 0, 32, 32, 208, 16, 32, 32); // current defense
		ctx.drawImage(defenseSprite, 16 * (((i-1)/2)%2) + 128, Math.floor((i-1)/4) * 16, 16, 16, 48 * (((i-1)/2)%2) + 192, (Math.floor((i-1)/4) + 1) * 16, 16, 16); // collected defense
		}
	}
	for(let i = 0; i < currentPrize; i++) //draw prizes
	{
		ctx.drawImage(prizeSprite, i*32, 0, 32, 48, (i*32) + 64, 0, 32, 48); // current defense
	}
	
}

function healthCaves()
{
	for(let i = 0; i <= currentMap.length; i++)
	{
		if(
		currentMap[i] == 9  ||
		currentMap[i] == 44 ||
		currentMap[i] == 73
		) // find coordinates of health door panels
		{
			tileEdgeFinder(i);
			healthCaveEntranceX = leftTileEdge;
			healthCaveEntranceY = topTileEdge;
		}
	}
	if(
			heroX <= healthCaveEntranceX + 6 &&
			heroX + 6 >= healthCaveEntranceX &&
			heroY <= healthCaveEntranceY + 6 &&
			heroY + 2 >= healthCaveEntranceY &&
			lastButtonPressed == "up"
		)
	{
		heroInHealthCave = true;
		previousMap = currentMap;
		heroExitX = heroX;
		heroExitY = heroY;
		heroX = 120;
		heroY = 220;
	}
	if(heroInHealthCave)
	{
		currentMap = mapHealth;
		for(let i = 0; i < healthLocations.length; i++)
		{
			if(healthLocations[i][0] == "map" + mapColumns[currentColumn] + currentRow && healthLocations[i][1] == true)
			{
				ctx.drawImage(healthSprite, 0, 0, 16, 16, healthX, healthY, 16, 16);
				healthMap = i;
			}
		}
		if(healthLocations[healthMap][1] == true)
		{
			if(
				heroX <= healthX + 8 &&
				heroX + 16 >= healthX &&
				heroY <= healthY + 8 &&
				heroY + 16 >= healthY
			)
			{
				currentHealth = currentHealth + 1;
				healthLocations[healthMap][1] = false;
			}
		}
		if(heroY > 226)
		{
			heroX = heroExitX;
			heroY = heroExitY;
			currentMap = previousMap;
			heroInHealthCave = false;
			healthInHealthCave = false;
			createEnemies();
		}
	}
}

function itemCaves()
{
	for(let i = 0; i <= currentMap.length; i++)
	{
		if(
		currentMap[i] == 14 ||
		currentMap[i] == 39 ||
		currentMap[i] == 63
		) // find coordinates of health door panels
		{
			tileEdgeFinder(i);
			itemCaveEntranceX = leftTileEdge;
			itemCaveEntranceY = topTileEdge;
		}
	}
	if(
			heroX <= itemCaveEntranceX + 6 &&
			heroX + 6 >= itemCaveEntranceX &&
			heroY <= itemCaveEntranceY + 6 &&
			heroY + 2 >= itemCaveEntranceY &&
			lastButtonPressed == "up"
		)
	{
		heroInItemCave = true;
		previousMap = currentMap;
		heroExitX = heroX;
		heroExitY = heroY;
		heroX = 120;
		heroY = 220;
	}
	if(heroInItemCave)
	{
		currentMap = mapHealth;  //change this
		for(let i = 0; i < itemLocations.length; i++)
		{
			if(itemLocations[i][0] == "map" + mapColumns[currentColumn] + currentRow && itemLocations[i][1] == false)
			{
				itemNumber = i;
				if(i%2 == 0)
				{
					ctx.drawImage(attackSprite, 16 * ((i/2)%2) + 128, Math.floor(i/4) * 16, 16, 16, itemX, itemY, 16, 16);
					itemNumber = i;
				}
				else
				{
					ctx.drawImage(defenseSprite, 16 * (((i-1)/2)%2) + 128, Math.floor((i-1)/4) * 16, 16, 16, itemX, itemY, 16, 16);
				}
			}
		}
		if(healthLocations[itemNumber][1] == true)
		{
			if(
				heroX <= healthX + 8 &&
				heroX + 16 >= healthX &&
				heroY <= healthY + 8 &&
				heroY + 16 >= healthY
			)
			{
				currentattack = attackDamage[itemNumber/2]
				itemLocations[itemNumber][1] = true;
			}
		}
		if(heroY > 226)
		{
			heroX = heroExitX;
			heroY = heroExitY;
			currentMap = previousMap;
			heroInItemCave = false;
			createEnemies();
		}
	}
}

function developerSettings()
{
	ctx.fillStyle = "#c7c700";
	ctx.fillText("map" + mapColumns[currentColumn] + currentRow, 10, 80);
	heroSpeed = 4;
	//itemLocations[0][1] = true; //att reg1
	//itemLocations[1][1] = true; //def reg1
	//itemLocations[2][1] = true; //att reg2
	//itemLocations[3][1] = true; //def reg2
	//itemLocations[4][1] = true; //att reg3
	//itemLocations[5][1] = true; //def reg3
	//itemLocations[6][1] = true; //att reg4
	//itemLocations[7][1] = true; //def reg4
	//maxHealth = 16; // max 16
	//currentHealth = 16; // max 16
	//currentPrize = 4; // max 4
}

function draw () {
	setTimeout(function() {
	requestAnimationFrame(draw);
	ctx.fillStyle = "rgb(20,20,20)";
	ctx.fillRect(0,0,256,240);
	drawMap(currentMap);
	overworldBuilder();
	drawHero();
	drawHUD();
	healthCaves();
	itemCaves();
	developerSettings();
	},1000/fps);
}
draw();
