# Markdown Sebastiaan Tromper
## Week 2

## Week 3


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
