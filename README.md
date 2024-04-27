# Kometa Configs (formerly Plex Meta Manager)
Public Kometa configs by TheChrisK

<a href="https://www.buymeacoffee.com/thechrisk" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-green.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

This config is what I use to produce the below collection examples. It is installed on Docker in Linux. Your install, paths and setup will vary. It is not advised to use this config as-is, but rather to pick and choose which parts you wish to use.

Credit to [@meisnate12](https://github.com/meisnate12) for Kometa and related images, [@s0len](https://github.com/s0len/meta-manager-config) for the TV overlay images, and to [@pterisaur](https://github.com/pterisaur) for the people posters.

These setups may not work unless you are on the `develop` or `nightly` branch of Kometa.

<img src="https://github.com/TheChrisK/PMM/blob/main/images/Collections.png?raw=true">

# Movies

## Collections

### Cities Collection

This collection includes films where the city plays a character role in the story. For now this is only in the U.S.
The films come from my own Trakt collections. If you have a movie that needs to be added, please let me know.

The below posters were created by me using the Kometa default template provided by [@meisnate12](https://github.com/meisnate12).

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/cities.png">

```yaml
#####################
#     TEMPLATES     #
#####################
templates:
  City:
    url_poster: https://raw.githubusercontent.com/TheChrisK/PMM/main/assets/posters/cities/<<city>>.png
    sort_title: "!105_<<collection_name>>"
    collection_order: title.asc
    content_rating: R
    summary: "A selection of films where the City of <<city>> plays a character role."
    sync_mode: sync
    schedule: weekly(saturday)

#####################
#    COLLECTIONS    #
#####################
collections:
  Chicago Collection:
    template: 
      name: City
      city: Chicago
    trakt_list: https://trakt.tv/users/oldmankestis/lists/chicago
      
  Detroit Collection:
    template: 
      name: City
      city: Detroit
    trakt_list: https://trakt.tv/users/oldmankestis/lists/detroit

  Las Vegas Collection:
    template: 
      name: City
      city: Las Vegas
    trakt_list: https://trakt.tv/users/oldmankestis/lists/las-vegas

  Los Angeles Collection:
    template: 
      name: City
      city: Los Angeles
    trakt_list: https://trakt.tv/users/oldmankestis/lists/los-angeles
      
  New York Collection:
    template: 
      name: City
      city: New York
    trakt_list: https://trakt.tv/users/oldmankestis/lists/new-york
    
  Washington D.C. Collection:
    template:
      name: City
      city: Washington DC
    trakt_list: https://trakt.tv/users/oldmankestis/lists/washington-dc
```

### Weekly Random Collection
I created a simple config to generate a "Weekly Random" collection. It searches all your Plex movies, grabs 10 at random and adds them to the collection. This is scheduled to run on Mondays in the 6am to 7am hours. 
If you have your Kometa run more than once per day, you will need to adjust the schedule as it will reset on each run for Monday.

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/weekly.png">

```yaml
#####################
#     TEMPLATES     #
#####################
templates:
  random:
    url_poster: https://raw.githubusercontent.com/TheChrisK/PMM/main/assets/plex/Collections/Weekly%20Random%20Movies/poster.png
    sort_title: "!058_<<collection_name>>"
    summary: "A weekly collection of 10 random movies. Changes every Monday."
    sync_mode: sync
    schedule: all[weekly(monday), hourly(06-07)]

#####################
#    COLLECTIONS    #
##################### 

collections:
  Weekly Random Movies:
    template:
      name: random
    plex_search:
      all:
        title.not: "`" #USING THE BACKTICK AS A SEARCH PARAMETER SINCE NO FILM CONTAINS THIS CHARACTER
      sort_by: random
      limit: 10
```

### Top Actors and Directors

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/top-people.png">
<sup>People posters courtesy of @pterisaur.</sup>

This config will add dynamic collections for the top rated actors and directors that exist in your library.

For **Actors**, it will search TMDb for the top 200 actors who are at least in the top 5 cast of a movie `(depth = 5)` and will only create a collection if 10 or more titles exist.

For **Directors**, it will search TMDb for the top 10 primary directors `(depth = 1)` with a limit of 5 collections total, also only creating if 10 or more exist.

Add the following to your **Movie** `collection_files:` section:

```yaml
collection_files:
  - url: https://raw.githubusercontent.com/TheChrisK/PMM/main/People/People.yml
```
If you wish to customize this config, you may [download it](https://raw.githubusercontent.com/TheChrisK/PMM/main/People/People.yml) and reference it locally.

## Overlays

### Media Stinger

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/mediastinger-text.png">

**[Media Stinger](https://mediastinger.com)** is a website that tells you if a mid-credit or post-credit scene exists.

Add the following to your library block in your `config.yml`

```yaml
    - default: mediastinger
      template_variables:
        url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/bottom-left/mediastinger-bottom-left.png
       #url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/bottom-left/mediastinger-bottom-left-notext.png #USE THIS IF YOU WANT JUST THE LOGO AND NO TEXT
        vertical_align: bottom
        vertical_offset: 0
        horizontal_align: right
        horizontal_offset: 0
        back_width: 1000
        back_height: 1500
        back_color: 00
```

### Movie Audio and Video Codec Ribbon

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/av-top-left.png">

This configuration will add the audio codec and video resolution to the top left of your posters. These are designed to work together to remain centered. 

**NOTE:** [This config adds a black background prior to the audio and video overlays.](https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Background.yml) If you use this overlay, the Background must be run before the `-pmm: resolution` and `-pmm: audio_codec` defaults

Add the below to your 'Movies' section of your `config.yml`

```yaml
  Movies:
    #schedule_overlays: hourly(06-07) #RUNS DAILY DURING THE 6AM and 7AM HOURS. UNCOMMENT AND UPDATE AS NEEDED
    overlay_files:
    - url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Background.yml #REQUIRED: PLACES A BLACK BACGROUND IN THE TOP LEFT CORNER BEFORE THE RESOLUTION AND CODEC OVERLAYS
    - default: resolution
      template_variables:
        url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/resolution-top-left-45deg/<<overlay_name>>.png
        horizontal_align: left
        horizontal_offset: 0
        vertical_offset: 0
        vertical_align: top
        final_horizontal_offset: 0
        final_vertical_offset: 0
        back_width: 1000
        back_height: 1500
        back_color: 00
        #use_4k_dvhdrplus: false #UNCOMMENT THE BELOW LINES IF YOU WISH TO EXCLUDE CERTAIN RESOLUTIONS OR CHANGE TO "TRUE"
        #use_dvhdrplus: false
        #use_1080p: false
        #use_720p: false
        #use_576p: false
        #use_480p: false
        #use_edition: false
    - default: audio_codec
      template_variables:
        url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/audio-top-left-45deg/<<key>>.png
        horizontal_align: left
        horizontal_offset: 0
        vertical_offset: 0
        vertical_align: top
        back_width: 1000
        back_height: 1500
        back_color: 00
    - remove_overlays: false
```

### Movie Top Ranked Ribbon

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/top-bottom-right.png">

This will add top lists in the bottom right. The [config](https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Top.yml) optionally has bottom ranked lists but for now those are commented out.

The lists include:

* IMDb Top 250
* Letterbox Top 1000
* Metacritic's Must See
* Rotten Tomatoes Certified Fresh

These top lists are applied in that order. **Ex:** If a movie is in the Metacritic's Must See but is also an IMDb Top 250, the IMDb overlay will take precedence.

Add the below to your 'Movies' section of your `config.yml`

```yaml
overlay_files:
  - url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Top.yml #BOTTOM RIGHT OVERLAY FOR IMDB TOP 250, RT FRESH, MC MUST SEE AND LETTERBOX 1000
```
# TV Shows

## Overlays

### TV Show Network and Status

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/status-top-left.png">

**This will add the network and status of the show in the top left corner of the poster**

Add the below to your 'TV Shows' section of your `config.yml`
```yaml
    overlay_files:
    - remove_overlays: false
    - url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Status.yml #AIRING STATUS OVERLAY CONFIG
    - default: network #PMM DEFAULT NETWORK OVERLAY USING CUSTOM IMAGES
      template_variables:
        horizontal_align: left
        horizontal_offset: 0
        vertical_offset: 0
        vertical_align: top
        back_width: 1000
        back_height: 1500
        url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/network-top-left/<<key>>.png
        back_color: 00
```

### Movie Top Ranked Ribbon

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/images/top-bottom-right-show.png">

Same config as the [Movies](https://github.com/TheChrisK/PMM/main/README.md#movie-top-ranked-ribbon), this will add top rankings in the bottom right. The config is [here](https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Top.yml).

The lists include:

* IMDb Top 250
* Metacritic's Must See
* Rotten Tomatoes Certified Fresh

These top lists are applied in that order. **Ex:** If a movie is in the Metacritic's Must See but is also an IMDb Top 250, the IMDb overlay will take precedence.

Add the below to your 'Movies' section of your `config.yml`

```yaml
overlay_files:
  - url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Top.yml #BOTTOM RIGHT OVERLAY FOR IMDB TOP 250, RT FRESH AND MC MUST SEE.
```
