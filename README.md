![build](https://img.shields.io/github/workflow/status/cowboy-bebug/app-store-scraper/Build)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/cowboy-bebug/app-store-scraper/pulls)
[![PyPI](https://img.shields.io/pypi/v/app-store-scraper)](https://pypi.org/project/app-store-scraper/)
![downloads](https://img.shields.io/pypi/dm/app-store-scraper)
![license](https://img.shields.io/pypi/l/app-store-scraper)
![code style](https://img.shields.io/badge/code%20style-black-black)

```
   ___                _____ _                   _____
  / _ \              /  ___| |                 /  ___|
 / /_\ \_ __  _ __   \ `--.| |_ ___  _ __ ___  \ `--.  ___ _ __ __ _ _ __   ___ _ __
 |  _  | '_ \| '_ \   `--. \ __/ _ \| '__/ _ \  `--. \/ __| '__/ _` | '_ \ / _ \ '__|
 | | | | |_) | |_) | /\__/ / || (_) | | |  __/ /\__/ / (__| | | (_| | |_) |  __/ |
 \_| |_/ .__/| .__/  \____/ \__\___/|_|  \___| \____/ \___|_|  \__,_| .__/ \___|_|
       | |   | |                                                    | |
       |_|   |_|                                                    |_|
```

# Quickstart

Install:
```console
pip3 install app-store-scraper
```

Scrape reviews for an app:
```python
from app_store_scraper import AppStore
from pprint import pprint

minecraft = AppStore(country="nz", app_name="minecraft")
minecraft.review(how_many=20)

pprint(minecraft.reviews)
pprint(minecraft.reviews_count)
```

Scrape reviews for a podcast:
```python
from app_store_scraper import Podcast
from pprint import pprint

sysk = Podcast(country="nz", app_name="stuff you should know")
sysk.review(how_many=20)

pprint(sysk.reviews)
pprint(sysk.reviews_count)
```

# Extra Details

Let's continue from the code example used in [Quickstart](#quickstart).


## Instantiation

There are two required and one positional parameters:

- `country` (required)
  - two-letter country code of [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) standard
- `app_name` (required)
  - name of an iOS application to fetch reviews for
  - also used by `search_id()` method to search for `app_id` internally
- `app_id` (positional)
  - can be passed directly
  - or ignored to be obtained by `search_id` method internally

Once instantiated, the object can be examined:
```pycon
>>> minecraft
AppStore(country='nz', app_name='minecraft', app_id=479516143)
```
```pycon
>>> print(app)
     Country | nz
        Name | minecraft
          ID | 479516143
         URL | https://apps.apple.com/nz/app/minecraft/id479516143
Review count | 0
```

Other optional parameters are:

- `log_format`
  - passed directly to `logging.basicConfig(format=log_format)`
  - default is `"%(asctime)s [%(levelname)s] %(name)s - %(message)s"`
- `log_level`
  - passed directly to `logging.basicConfig(level=log_level)`
  - default is `"INFO"`
- `log_interval`
  - log is produced every 5 seconds (by default) as a "heartbeat" (useful for a long scraping session)
  - default is `5`


## Fetching App Details

The original library does not have other details besides review's data. So what this forked repository will have is a method called `app_details()` which essentially grabs the entire data about the app itself.

```pycon
>>> minecraft.app_details()
{.... 'kind': 'software', 'trackCensoredName': 'Minecraft', 'languageCodesISO2A': ['DA', 'NL', 'EN', 'FI', 'FR', 'DE', 'IT', 'JA', 'KO', 'NB', 'PL', 'PT', 'RU', 'ZH', 'ES', 'SV', 'ZH', 'TR'], 'fileSizeBytes': '1026025472', 'formattedPrice': '$6.99', 'contentAdvisoryRating': '9+', 'averageUserRatingForCurrentVersion': 4.49708, 'userRatingCountForCurrentVersion': 608097, 'averageUserRating': 4.49708, 'trackViewUrl': 'https://apps.apple.com/us/app/minecraft/id479516143?uo=4', 'trackContentRating': '9+', 'currency': 'USD', 'releaseNotes': 'Various bug fixes!', 'artistId': 479516146, 'artistName': 'Mojang', 'genres': ['Games', 'Simulation', 'Adventure'], 'price': 6.99, 'description': "Explore infinite worlds and build everything from the simplest of homes to the grandest of castles. Play in creative mode with unlimited resources or mine deep into the world in survival mode, crafting weapons and armor to fend off dangerous mobs. \n\nCreate, explore, and survive along or play with friends on all different devices. Scale craggy mountains, unearth elaborate caves, and mine large ore veins. Discover lush cave and dripstone cave biomes. Light up your world with candles to show what a savvy spelunker and master mountaineer you are! \n\nEXPAND YOUR GAME:\nMarketplace - Discover the latest community creations in the marketplace! Get unique maps, skins, and texture packs from your favorite creators.\n\nSlash commands - Tweak how the game plays: you can give items away, summon mobs, change the time of day, and more. \n\nAdd-Ons - Customize your experience even further with free Add-Ons! If you're more tech-inclined, you can modify data-driven behaviors in the game to create new resource packs.\n\nMinecraft Realms auto-renewable subscription info:\n\nMinecraft now comes with the option to buy Minecraft Realms. Realms is a monthly subscription service that lets you create your own always-online Minecraft world.\nThere are currently two subscription options to choose from depending on how many people you want to invite to play in your realm simultaneously. A realm for you and 2 friends costs 3.99 USD/month (or local equivalent) and a realm for you and 10 friends cost 7.99 USD/month (or local equivalent).\nA 30-day trial of Minecraft Realms for you and 10 friends is available. Any unused portion of a free trial period will be forfeited when the user purchases a subscription.\n\nThe payment will be charged to your iTunes account at confirmation of purchase and the subscription automatically renews unless auto-renew is turned off at least 24-hours before the end of the current period. Your account will be charged for renewal within 24-hours prior to the end of the current period, at the subscription price option you have previously selected.\n\nYour subscription can be managed by the user and auto-renewal may be turned off by going to the user's Account Settings after purchase. There is also a button in-game that take you to these settings. If you cancel after your subscription has activated, you won't be refunded for the remaining active period of the subscription.\n\nHere are links to our privacy policy and terms of use:\n- Privacy policy: https://account.mojang.com/terms#privacy\n- Terms of use: https://account.mojang.com/terms", 'genreIds': ['6014', '7015', '7002'], 'primaryGenreName': 'Games', 'primaryGenreId': 6014, 'releaseDate': '2011-11-17T08:00:00Z', 'sellerName': 'Mojang AB', 'bundleId': 'com.mojang.minecraftpe', 'trackId': 479516143, 'trackName': 'Minecraft', 'isVppDeviceBasedLicensingEnabled': True, 'currentVersionReleaseDate': '2023-06-21T15:39:05Z', 'minimumOsVersion': '11.0', 'version': '1.20.1', 'wrapperType': 'software', 'userRatingCount': 608097}
```

The app detail dictionary has the following important schema such as:
```python
{
    "contentAdvisoryRating": str,
    "description": str,
    "Privacy policy": str,
    "primaryGenreName": str,
    "bundleId": str,
    "version": str,
    "userRatingCount": int,
    # and many more....
 }
```

## Fetching Review

The maximum number of reviews fetched per request is 20. To minimise the number of calls, the limit of 20 is hardcoded. This means the `review()` method will always grab more than the `how_many` argument supplied with an increment of 20.

```pycon
>>> minecraft.review(how_many=33)
>>> minecraft.reviews_count
40
```

If `how_many` is not provided, `review()` will terminate after *all* reviews are fetched.

**NOTE** the review count seen on the landing page differs from the actual number of reviews fetched. This is simply because only *some* users who rated the app also leave reviews.

### Optional Parameters

- `after`
  - a `datetime` object to filter older reviews
- `sleep`
  - an `int` to specify seconds to sleep between each call

## Review Data

The fetched review data are loaded in memory and live inside `reviews` attribute as a list of dict.
```pycon
>>> minecraft.reviews
[{'userName': 'someone', 'rating': 5, 'date': datetime.datetime(...
```

Each review dictionary has the following schema:
```python
{
    "date": datetime.datetime,
    "isEdited": bool,
    "rating": int,
    "review": str,
    "title": str,
    "userName": str
 }
```
