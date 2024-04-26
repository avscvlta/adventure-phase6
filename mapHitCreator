function mapHitCreator()
{
	map2d = [];
	wallMap = [...currentMap];
	for(let i = 0; i <= wallMap.length; i++)
	{
		if(
			wallMap[i] == 4 ||
			wallMap[i] == 8 ||
			wallMap[i] == 10 ||
			wallMap[i] == 34 ||
			wallMap[i] == 40 ||
			wallMap[i] == 64 ||
			wallMap[i] == 65 ||
			wallMap[i] == 70 ||
			wallMap[i] == 74
		)
		{
			wallMap[i] = 1;
		}
		else if(wallMap[i] > 0)
		{
			wallMap[i] = 0;
		}
	}
	map2d = [];
	for(let i = 0; i < 11; i++)
	{
		for(let j = 0; j < 16; j++)
		{
			map2dRow.push(wallMap[i*16+j]);
		}
		map2d.push(map2dRow);
		map2dRow = [];
	}
	routefindingInput = new Graph([
		eval(map2d[0]),
		eval(map2d[1]),
		eval(map2d[2]),
		eval(map2d[3]),
		eval(map2d[4]),
		eval(map2d[5]),
		eval(map2d[6]),
		eval(map2d[7]),
		eval(map2d[8]),
		eval(map2d[9]),
		eval(map2d[10])
		]);
}
