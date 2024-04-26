function drawEnemies()
{
	if(heroInItemCave != true && heroInHealthCave != true )
	{
		for(i = 0; i < mapEnemies.length; i++)
		{
			if([mapEnemies[i].positionY] == 0 && [mapEnemies[i].positionX] == 0)
			{
				while(map2d[mapEnemies[i].positionY][mapEnemies[i].positionX] == 0)
				{
					mapEnemies[i].positionX = Math.floor(Math.random()*16);
					mapEnemies[i].positionY = Math.floor(Math.random()*11);
					mapEnemies[i].startPathX = mapEnemies[i].positionX;
					mapEnemies[i].startPathY = mapEnemies[i].positionY;
				}
			}
			if(mapEnemies[i].getNewPath)
			{
				while(result == null || result.length == 0)
				{
					mapEnemies[i].endPathX = Math.floor(Math.random()*16);
					mapEnemies[i].endPathY = Math.floor(Math.random()*11);
					var start = routefindingInput.grid[mapEnemies[i].startPathY][mapEnemies[i].startPathX];
					var end = routefindingInput.grid[mapEnemies[i].endPathY][mapEnemies[i].endPathX];
					var result = astar.search(routefindingInput, start, end);
					pathNodes = [...result];
				}
				result = null;
				mapEnemies[i].startPathX = mapEnemies[i].endPathX;
				mapEnemies[i].startPathY = mapEnemies[i].endPathY;
				mapEnemies[i].path = [...pathNodes];
				if(mapEnemies[i].nextNodeX == 0)
				{
					mapEnemies[i].nextNodeX = mapEnemies[i].path[0].y * 16;
					mapEnemies[i].nextNodeY = mapEnemies[i].path[0].x * 16 + 64;
				}
				mapEnemies[i].getNewPath = false;
			}
			if(mapEnemies[i].enemyFrame == 0)
			{
				mapEnemies[i].previousNodeX = mapEnemies[i].nextNodeX;
				mapEnemies[i].previousNodeY = mapEnemies[i].nextNodeY;
				mapEnemies[i].nextNodeX = mapEnemies[i].path[0].y * 16;
				mapEnemies[i].nextNodeY = mapEnemies[i].path[0].x * 16 + 64;
				mapEnemies[i].path.shift();
			}
			if(mapEnemies[i].enemyFrame >= 0)
			{
				enemyIncrement = .25;
				enemySpriteRow = mapEnemies[i].spriteRow;
			}
			if(mapEnemies[i].enemyFrame >= enemyFrameReset * .25)
			{
				enemyIncrement = .50;
				enemySpriteRow = mapEnemies[i].spriteRow + 16;
			}
			if(mapEnemies[i].enemyFrame >= enemyFrameReset * .5)
			{
				enemyIncrement = .75;
				enemySpriteRow = mapEnemies[i].spriteRow;
			}
			if(mapEnemies[i].enemyFrame >= enemyFrameReset * .75) 
			{
				enemyIncrement = 1;
				enemySpriteRow = mapEnemies[i].spriteRow + 16; 
			}
			mapEnemies[i].enemyFrame = mapEnemies[i].enemyFrame + 1;
			if(mapEnemies[i].enemyFrame >= enemyFrameReset)
			{
				mapEnemies[i].enemyFrame = 0;
			}
			mapEnemies[i].positionX = mapEnemies[i].previousNodeX + (enemyIncrement * (mapEnemies[i].nextNodeX - mapEnemies[i].previousNodeX));
			mapEnemies[i].positionY = mapEnemies[i].previousNodeY + (enemyIncrement * (mapEnemies[i].nextNodeY - mapEnemies[i].previousNodeY));
			if(mapEnemies[i].previousNodeX > mapEnemies[i].nextNodeX)
			{
				enemySpriteDirection = "left";
				enemySpriteColumn = 16;
			}
			if(mapEnemies[i].nextNodeX > mapEnemies[i].previousNodeX)
			{
				enemySpriteDirection = "right";
				enemySpriteColumn = 48;
			}
			if(mapEnemies[i].previousNodeY > mapEnemies[i].nextNodeY)
			{
				enemySpriteDirection = "up";
				enemySpriteColumn = 32;
			}
			if(mapEnemies[i].nextNodeY > mapEnemies[i].previousNodeY)
			{
				enemySpriteDirection = "down";
				enemySpriteColumn = 0;
			}
			ctx.drawImage(enemySprite, enemySpriteColumn, enemySpriteRow, 16, 16, mapEnemies[i].positionX, mapEnemies[i].positionY, 16, 16);
			if(mapEnemies[i].path.length <= 0)
			{
				mapEnemies[i].getNewPath = true;
			}
		}
	}
}
