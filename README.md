# Plex Meta Manager Config
Public PMM configs by TheChrisK

This config is what I use to produce the below collection examples. It is installed on Docker in Linux. Your install, paths and setup will vary. It is not advised to use this config as-is, but rather to pick and choose which parts you wish to use.

Credit to [@meisnate12](https://github.com/meisnate12) for Plex-Meta-Manager and related images, [@s0len](https://github.com/s0len/meta-manager-config) for the TV overlay images, and to [@pterisaur](https://github.com/pterisaur) for the people posters.

<img src="https://github.com/TheChrisK/PMM/blob/main/Collections.png?raw=true">

## Movies

### Cities Collection

This collection includes films where the city plays a character role in the story. For now this is only in the U.S.
The films come from my own Trakt collections. If you have a movie that needs to be added, please let me know.

The below posters were created by me using the PMM default template provided by [@meisnate12](https://github.com/meisnate12).

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/cities.png">

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
I created a simple config to generate a "Weekly Random" collection. It searches all your Plex movies, grabs 10 at random and adds them to the collection. This is scheduled to run on Mondays. 
If you have your PMM run more than once per day, you will need to adjust the schedule as it will reset on each run for Monday.

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/weekly.png">

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
    schedule: weekly(monday)

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

## Overlays

### Media Stinger

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/mediastinger-text.png">

**[Media Stinger](https://mediastinger.com)** is a website that tells you if a mid-credit or post-credit scene exists.

Add the following to your library block in your `config.yml`

```yaml
    - pmm: mediastinger
      template_variables:
        url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/bottom-left/mediastinger-bottom-left.png
       #url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/bottom-left/mediastinger-bottom-left.png #USE THIS IF YOU WANT JUST THE LOGO AND NO TEXT
        vertical_align: bottom
        vertical_offset: 0
        horizontal_align: right
        horizontal_offset: 0
        back_width: 1000
        back_height: 1500
        back_color: 00
```

### TV Show Network and Status

<img src="https://raw.githubusercontent.com/TheChrisK/PMM/main/status-top-left.png">

**This will add the network and status of the show in the top left corner of the poster**

Add the below to your 'TV Shows' section of your `config.yml`
```yaml
TV Shows:
    template_variables:
      use_separator: false
    overlay_files:
    - remove_overlays: false
    - url: https://raw.githubusercontent.com/TheChrisK/PMM/main/overlays/Status.yml #AIRING STATUS OVERLAY CONFIG
    - pmm: network
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