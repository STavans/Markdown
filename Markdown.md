# Markdown Sebastiaan Tromper
## Week 2
### Beslissingen
- Lessen worden door één leraar gegeven.
	- Dit is normaal voor een gebruikelijke les en voor de simpelheid.
- Één groep per les.
	- Dit is normaal voor een gebruikelijke les.
- Één les vindt plaats in één lokaal
	- Dit is normaal voor een gebruikelijke les.
- Er zijn maximaal 12 leerlingen per klas.
	- I.v.m. overzichtelijkheid.
- Er zijn 6 groepen studenten.
	- I.v.m. overzichtelijkheid.
- Er zijn 6 leslokalen.
	- Er is voor deze hoeveelheid gekozen om het gelijk te houden aan het aantal klassen en leraren.
- De dag begint om 08:00 tot 17:00.
	- Hiervoor is gekozen om een vaste begin en eindtijd vast te stellen voor de simulatie.
- De lessen kunnen ingeroosterd worden van 8:30 tot 16:30.
	- Dit is normaal voor een schooldag.
- Er zijn maximaal 6 docenten.
	- Er is voor deze hoeveelheid gekozen om het gelijk te houden aan het aantal klassen.
- Gaan we tabs, view venster gebruiken of laten we het zo?
	- Tabs, het is dan een stuk meer overzichtelijker, simpeler en netter.
- Hoe worden groepen aangemaakt in de GUI? Zit daar een maximum aan? Een minimum?
	- Groepen worden voorgeprogrammeerd.
- Zijn de vakken vast voor geprogrameerd. Zo ja, welke vakken zijn er?
	- Ja, welke wordt nog gediscusseerd.
- Als een groep leeg is, wat gebeurt er als een leraar les geeft aan een lege groep. (Als dat gebeurt)
	- Die zijn niet leeg.
- Wat gebeurt er als alle groepen vol zijn en 'Generate Random' wordt gedrukt?
	- Dan wordt er een fout melding gegeven.
	
![Start scherm](https://github.com/STavans/Markdown/blob/master/Start%20Scherm.png "Start scherm")
![Person manager](https://github.com/STavans/Markdown/blob/master/Person%20Manager.png "Person Manager")
![Roster frame](https://github.com/STavans/Markdown/blob/master/Roster%20Frame.png "Roster frame")
![Simulation](https://github.com/STavans/Markdown/blob/master/Simulation.png "Simulation")

## Week 3

Tilemap gemaakt:
![School simulatie tilemap](https://github.com/STavans/Markdown/blob/master/School%20simulatie%20tilemap.png "School simulatie tilemap")

## Week 4



  ``` Java code
  public class Map {
	private int width;
	private int height;

	private int tileHeight;
	private int tileWidth;

	private ArrayList<BufferedImage> tiles = new ArrayList<>();

	private int[][] map;

	public Map(String fileName)
	{
		JsonReader reader = null;
		reader = Json.createReader(getClass().getResourceAsStream(fileName));
		JsonObject root = reader.readObject();

		this.width = root.getInt("width");
		this.height = root.getInt("height");

		//load the tilemap
		try {
			BufferedImage tilemap = ImageIO.read(getClass().getResourceAsStream(root.getJsonArray("tilesets").getJsonObject(0).getString("image")));

			tileHeight= root.getJsonArray("tilesets").getJsonObject(0).getInt("tileheight");
			tileWidth= root.getJsonArray("tilesets").getJsonObject(0).getInt("tilewidth");

			for(int y = 0; y < tilemap.getHeight(); y += tileHeight)
			{
				for(int x = 0; x < tilemap.getWidth(); x += tileWidth)
				{
					tiles.add(tilemap.getSubimage(x, y, tileWidth, tileHeight));
				}
			}
		} catch (IOException e) {
			e.printStackTrace();
		}

		map = new int[height][width];
		for(int y = 0; y < height; y++)
		{
			for(int x = 0; x < width; x++)
			{
				map[y][x] = root.getJsonArray("layers").getJsonObject(0).getJsonArray("data").getInt(x);
			}
		}
	}
  ```
