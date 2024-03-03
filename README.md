# Plex Meta Manager Config
Public PMM configs by TheChrisK

This config is what I use to produce the below collection examples. It is installed on Docker in Linux. Your install, paths and setup will vary. It is not advised to use this config as-is, but rather to pick and choose which parts you wish to use.

Credit to [@meisnate12](https://github.com/meisnate12) for Plex-Meta-Manager and related images, [@s0len](https://github.com/s0len/meta-manager-config) for the TV overlay images, and to [@pterisaur](https://github.com/pterisaur) for the people posters.

<img src="https://github.com/TheChrisK/PMM/blob/main/Collections.png?raw=true">

## Movies

### Cities Collection

This collection includes films where the city plays a character role in the story. For now this is only in the U.S.
The films come from my own Trakt collections. If you have a movie that needs to be added, please let me know.

<img src="https://github.com/TheChrisK/PMM/blob/main/cities.png?raw=true">

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
