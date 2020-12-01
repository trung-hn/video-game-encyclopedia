# Video Game Encyclopedia
<p align="center">
  <img src="https://user-images.githubusercontent.com/39042628/69937490-f246aa00-14a8-11ea-89ad-073891b7b4a9.png" alt="Gaming">
</p> 

Visit [Kaggle page](https://www.kaggle.com/jummyegg/rawg-game-dataset) for the full Game Dataset


### Directory Tree
```
.
|-- src
|   |-- Combine_game_info.ipynb
|   |-- Get_game_id.ipynb
|   `-- Get_game_info.ipynb
|
`-- data
    |-- game_id.csv
    |-- game_info.csv
    |-- game_id
    |   |-- 1.json
    |   |-- 2.json
    |   `-- *.json
    |
    `-- game_info
        |-- 1.json
        |-- 2.json
        `-- *.json
```
### How to Start
`pip3 install -r requirements.txt`

### Steps to replicate the dataset:
1. Run `Get_game_id.ipynb`. This makes request to all pages in https://api.rawg.io/api/games?page=1 and save one JSON file for **each page** in `./data/game_id/*.json` where `*` is the page number. At the end, `./data/game_id.csv` is created which contains the name and id of each game which is needed for step 2.
2. Run `Get_game_info.ipynb`. Using the id from Step 1, this script makes request to https://api.rawg.io/api/games/ and save one JSON file for **each game** in `./data/game_info/*.json` where `*` is the game id.
3. Run `Combine_game_info.ipynb`. This combines data in `./data/game_info/` and saves it as `./data/game_info.csv`. `game_info.csv` contains the **final** data set

#### Important Notes:
- Only wanted information are saved in JSON files: 
    - `./data/game_id` with 17000 files has the size of ~10MBs. 
    - `./data/game_info` with 350000 files has the size of ~170MBs
- To increase the speed of obtaining the data from RAWG API, concurrent programming is applied to step 1 and 2. 
    - Step 1 takes ~40 minutes with 50 threads
    - Step 2 takes ~100 minutes with 100 threads
    - Step 3 takes ~5 minutes
- When 1 thread fails while requesting data, it will skip to next game/page **without** any notification. To make sure you get all games from RAWG, you can run Step 1 and Step 2 multiple times. Downloaded files are **skipped** automatically.

#### Limitations:
- To reduce the file size of downloaded files and the final CSV dataset, **not all** JSON information is downloaded. If you want more customization, you will need to change how the JSON is handled in Step 2
- Although Multithreading is applied, the whole process can take up to ~3 hours to finish because of the large amount of data.

___
### Context
This is a game data set containing 345667 games on over 50 platforms including mobiles. All games information is obtained using Python with [RAWG API](https://rawg.io/apidocs). This data set was last updated on Nov 10th 2019. If you are interested in obtaining more recent games, visit the [GitHub](https://github.com/trung-hn/game-encyclopedia) page for more information.

### Content
Each row contains information about one game. There are several columns that have multiple values like platforms, genres, ... In those cases, values are separated by double pipes `||`.

### Column definitions:
- `id`: An unique ID identifying this Game in RAWG Database
- `slug`: An unique slug identifying this Game in RAWG Database
- `name`: Name of the game
- `metacritic`: Rating of the game on [Metacritic](https://www.metacritic.com/game)
- `released`: The date the game was released
- `tba`: To be announced state
- `updated`: The date the game was last updated
- `website`: Game Website
- `rating`: Rating rated by RAWG user
- `rating_top`: Maximum rating
- `playtime`: Hours needed to complete the game
- `achievements_count`: Number of achievements in game
- `ratings_count`: Number of RAWG users who rated the game
- `suggestions_count`: Number of RAWG users who suggested the game
- `game_series_count`: Number of games in the series
- `reviews_count`: Number of RAWG users who reviewed the game
- `platforms`: Platforms game was released on. **Separated** by `||`
- `developers`: Game developers. **Separated** by `||`
- `genres`: Game genres. **Separated** by `||`
- `publishers`: Game publishers. **Separated** by `||`
- `esrb_rating`: ESRB ratings
- `added_status_yet`: Number of RAWG users had the game as "Not played"
- `added_status_owned`: Number of RAWG users had the game as "Owned"
- `added_status_beaten`: Number of RAWG users had the game as "Completed"
- `added_status_toplay`: Number of RAWG users had the game as "To play"
- `added_status_dropped`: Number of RAWG users had the game as "Played but not beaten"
- `added_status_playing`: Number of RAWG users had the game as "Playing"

### Acknowledgements
Thanks to [RAWG](https://rawg.io/) for providing easy to use and fast [API](https://rawg.io/apidocs) \
Icon made by <a href="https://www.flaticon.com/authors/good-ware" title="Good Ware">Good Ware</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a>

### Inspiration
With this data, one can create a game recommendation platform as well as drawing insights about the gaming industry and gaming trends.