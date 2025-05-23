---
hide:
  - toc
---

# Plex Builders

Plex has two categories of builders - Smart and Dumb (non-smart).

Smart Builders use rules (filters) to automatically include items that match the criteria of the Builder. When new media is added to your library, or if metadata of any item in your library changes to match the Builder's rules, the media is automatically included in the collection without the need to run Kometa again. 

Dumb (non-Smart) Builders are static in nature and will not dynamically update as new media is added/metadata criteria changes across your library - you will have to run Kometa any time you want the Builder to re-run.

Smart Builders are usually the recommended approach as they are lightweight and faster to process than Dumb Builders.

???+ important

    The `Smart Builders` and `Dumb Builders` tabs below will give examples of how to use the Builders, whilst the `Search Options`, `Sort Options` and `Builder Attributes` will give the full list of attributes and customizations available for use with the Builders.

=== "Smart Builders"
 
    Smart Builders allow Kometa to create Smart Collections in two different ways.
    
    The results of these builders are dynamic and do not require Kometa to re-run in order to update, instead they will 
    update automatically as the data within your Plex Library updates (i.e. if new media is added)

    Smart Filter and Smart Label are the two methods available for Smart Builders.

    Smart Filter Bulders use Plex's [Advanced Filters](https://support.plex.tv/articles/201273953-collections/) to create a smart collection based on the filter parameters provided. Any Advanced Filter made using the Plex UI should be able to be recreated using `smart_filter`. This is the normal approach used when your Builder criteria is held solely within Plex, and no third-party service involvement is required.

    Smart Label Builders attaches a label to every item that meets the criteria, and then creates a Smart Filter to search for that label. This is the normal approach used when you want to use a third-party list (such as Trakt or TMDb) with a Smart Builder.

    ???+ important
        
        Smart Builders do not work with Playlists

    === "Smart Filter Builder"
    
        Like Plex's [Advanced Filters](https://support.plex.tv/articles/201273953-collections/), you have to start each filter with either `any` or `all` as a base. You can only 
        have one base attribute and all filter attributes must be under the base.
        
        Inside the base attribute you can use any filter below or nest more `any` or `all`. You can have as many nested `any` 
        or `all` next to each other as you want. If using multiple `any` or `all` you will have to do so in the form of a list.  
        
        **Note: To search by `season`, `episode`, `album`, or `track` you must use the `builder_level` [Setting](../settings.md) 
        to change the type of items the collection holds.**

        ## Smart Filter Examples
        
        A few examples are listed below:
        
        ```yaml
        collections:
          Documentaries:
            smart_filter:
              all:
                genre: Documentary
        ```
        ```yaml
        collections:
          Dave Chappelle Comedy:
            smart_filter:
              all:
                actor: Dave Chappelle
                genre: Comedy
        ```
        ```yaml
        collections:
          Top Action Movies:
            smart_filter:
              all:
                genre: Action
              sort_by: audience_rating.desc
              limit: 20
        ```
        ```yaml
        collections:
          90s Movies:
            smart_filter:
              any:
                year:
                  - 1990
                  - 1991
                  - 1992
                  - 1993
                  - 1994
                  - 1995
                  - 1996
                  - 1997
                  - 1998
                  - 1999
        ```
        ```yaml
        collections:
          90s Movies:
            smart_filter:
              any:
                decade: 1990
        ```

        If you specify TMDb Person ID's using the Setting `tmdb_person` and then tell either `actor`, `director`, `producer`, or 
        `writer` to add `tmdb`, the script will translate the TMDb Person IDs into their names and run the filter on those names.
        
        ```yaml
        collections:
          Robin Williams:
            smart_filter:
              all:
                actor: tmdb
            tmdb_person: 2157
        ```
        ```yaml
        collections:
          Steven Spielberg:
            smart_filter:
              all:
                director: tmdb
            tmdb_person: https://www.themoviedb.org/person/488-steven-spielberg
        ```
        ```yaml
        collections:
          Quentin Tarantino:
            smart_filter:
              any:
                actor: tmdb
                director: tmdb
                producer: tmdb
                writer: tmdb
            tmdb_person: 138
        ```

    === "Smart Label Builder"

        A Smart Label Collection is a smart collection that grabs every item with a specific label generated by the program. 
        That label is added to all the items the Collection Builders find instead of being added to a normal collection. 
        
        To make a collection a Smart Label Collection, the `smart_label` attribute must be added to the collection definition. 
        It functions in two different ways:

        1. Define the sort using the Movies/Shows column of the [Sorts Table](#sort-options) below along with any other Builder 
        to make that collection a Smart Label Collection.
            ```yaml
            collections:
              Marvel Cinematic Universe:
                trakt_list: https://trakt.tv/users/jawann2002/lists/marvel-cinematic-universe-movies?sort=rank,asc
                smart_label: release.desc
            ```
        
        2. Provide a whole `smart_filter` to determine exactly how the smart collection should be built, ensuring to include `label: <<smart_label>>`, which will link it to the collection labels.
            ```yaml
            collections:
              Unplayed Marvel Cinematic Universe:
                trakt_list: https://trakt.tv/users/jawann2002/lists/marvel-cinematic-universe-movies?sort=rank,asc
                smart_label:
                  sort_by: release.desc
                  all:
                    label: <<smart_label>>
                    unplayed: true
            ```
        
        This is extremely useful because smart collections don't follow normal show/hide rules and can eliminate the need to 
        have [Plex Collectionless](#plex-collectionless) when used correctly. To fix the issue described in 
        [Plex Collectionless](#plex-collectionless) you would make `Marvel Cinematic Universe` a Smart Label Collection 
        and all other Marvel collection just normal collections, and they will show/hide all the movie properly.
        
        To have the Smart Label Collections to eliminate Plex Collectionless you have to go all in on using them. A good rule of 
        thumb to make sure this works correctly is that every item in your library should have a max of one non-smart collection.
        
        Reach out on the [Kometa Discord](https://kometa.wiki/en/latest/discord/) or in the [GitHub Discussions](https://github.com/Kometa-Team/Kometa/discussions) for help if you're having any issues getting 
        this to work properly.

=== "Dumb Builders"

    This Builder finds items by using data held solely within Plex.
     
    The results of these builders are static and require Kometa to re-run in order to update.
    
    | Attribute                                     | Description                                                                 |             Works with Movies              |              Works with Shows              |    Works with Playlists and Custom Sort    |
    |:----------------------------------------------|:----------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
    | [`plex_all`](#plex-all)                       | Gets every movie/show in your library. Useful with [Filters](../filters.md) | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
    | [`plex_search`](#plex-search)                 | Gets every movie/show based on the search parameters provided               | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | [`plex_watchlist`](#plex-watlist)           | Gets every movie/show in your Watchlist.                                    | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | [`plex_pilots`](#plex-pilots)                 | Gets the first episode of every show in your library                        |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | [`plex_collectionless`](#plex-collectionless) | Gets every movie/show that is not in a collection                           | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
    
    === "Plex All"
    
        Finds every item in your library. Useful with [Filters](../filters.md).
        
        The expected input is either true or false.
        
        ```yaml
        collections:
          9.0 Movies:
            plex_all: true
            filters:
              user_rating.gte: 9
        ```
    
    === "Plex Search"
        
        Uses Plex's [Advanced Filters](https://support.plex.tv/articles/201273953-collections/) to find all items based on the search parameters provided.
        
        Any Advanced Filter made using the Plex UI should be able to be recreated using `plex_search`. If you're having trouble 
        getting `plex_search` to work correctly, build the collection you want inside of Plex's Advanced Filters and take a 
        screenshot of the parameters in the Plex UI and post it in either the 
        [Discussions](https://github.com/Kometa-Team/Kometa/discussions) or on [Discord](https://kometa.wiki/en/latest/discord/), 
        and I'll do my best to help you. 
        
        like Plex's [Advanced Filters](https://support.plex.tv/articles/201273953-collections/) you have to start each search with either `any` or `all` as a base. You can only 
        have one base attribute and all search attributes must be under the base.
        
        Inside the base attribute you can use any search below or nest more `any` or `all`. You can have as many nested `any` 
        or `all` next to each other as you want. If using multiple `any` or `all` you will have to do so in the form of a list.  
        
        **Note: To search by `season`, `episode`, `album`, or `track` you must use the `builder_level` [Setting](../settings.md) to change 
        the type of items the collection holds.**
        
        There are a couple other attributes you can have at the top level only along with the base attribute are:
    
        ## Plex Search Examples
        
        A few examples are listed below:
        
        ```yaml
        collections:
          Documentaries:
            plex_search:
              all:
                genre: Documentary
        ```
        ```yaml
        collections:
          Dave Chappelle Comedy:
            plex_search:
              all:
                actor: Dave Chappelle
                genre: Comedy
        ```
        ```yaml
        collections:
          Top Action Movies:
            collection_order: custom
            plex_search:
              all:
                genre: Action
              sort_by: audience_rating.desc
              limit: 20
        ```
        ```yaml
        collections:
          90s Movies:
            plex_search:
              any:
                year:
                  - 1990
                  - 1991
                  - 1992
                  - 1993
                  - 1994
                  - 1995
                  - 1996
                  - 1997
                  - 1998
                  - 1999
        ```
        ```yaml
        collections:
          90s Movies:
            plex_search:
              any:
                decade: 1990
        ```
        ```yaml
        collections:
          Best 2010+ Movies:
            collection_order: custom
            plex_search:
              all:
                year.gte: 2010
              sort_by:
                - year.desc
                - audience_rating.desc
              limit: 20
        ```
        
        Here's an example of an episode collection using `plex_search`.
        
        ```yaml
         collections:
           Top 100 Simpsons Episodes:
             collection_order: custom
             builder_level: episode
             plex_search:
               type: episode
               sort_by: audience_rating.desc
               limit: 100
               all:
                 title.ends: "Simpsons"
             summary: A collection of the highest rated simpsons episodes.
        ```
        
        If you specify TMDb Person ID's using the Setting `tmdb_person` and then tell either `actor`, `director`, `producer`, or 
        `writer` to add `tmdb`, the script will translate the TMDb Person IDs into their names and run the search on those names.
        
        ```yaml
        collections:
          Robin Williams:
            plex_search:
              all:
                actor: tmdb
            tmdb_person: 2157
        ```
        ```yaml
        collections:
          Steven Spielberg:
            plex_search:
              all:
                director: tmdb
            tmdb_person: https://www.themoviedb.org/person/488-steven-spielberg
        ```
        ```yaml
        collections:
          Quentin Tarantino:
            plex_search:
              any:
                actor: tmdb
                director: tmdb
                producer: tmdb
                writer: tmdb
            tmdb_person: 138
        ```

    === "Plex Watchlist"
        
        Finds every item in your Watchlist.
        
        The expected input is the sort you want returned. It defaults to `added.asc`.
        
        ### Watchlist Sort Options
        
        | Sort Option                                 | Description                                 |
        |:--------------------------------------------|:--------------------------------------------|
        | `title.asc`<br>`title.desc`                 | Sort by Title                               |
        | `release.asc`<br>`release.desc`             | Sort by Release Date (Originally Available) |
        | `critic_rating.asc`<br>`critic_rating.desc` | Sort by Critic Rating                       |
        | `added.asc`<br>`added.desc`                 | Sort by Date Added to your Watchlist        |
        
        The `sync_mode: sync` and `collection_order: custom` Setting are recommended.
        
        ```yaml
        collections:
          My Watchlist:
            plex_watchlist: critic_rating.desc
            collection_order: custom
            sync_mode: sync
        ```
        
    === "Plex Pilots"
    
        Gets the first episode of every show in your library. This only works with `builder_level: episode`
        
        ```yaml
        collections:
          Pilots:
            builder_level: episode
            plex_pilots: true
        ```
        
    === "Plex Collectionless"
    
        **This is not needed if you're using [Smart Label Collections](#smart-label).**
        
        Finds every item that is not in a collection unless the collection is in the exclusion list. This is a special 
        collection type to help keep your library looking correct. When items in your library are in multiple collections it 
        can mess up how they're displayed in your library.
        
        For Example, if you have a `Marvel Cinematic Universe` Collection set to `Show this collection and its items` and an 
        `Iron Man` Collection set to `Hide items in this collection` what happens is the show overrides the hide, and you end 
        up with both the collections and the 3 Iron Man movies all displaying.
        
        Alternatively, if you set the `Marvel Cinematic Universe` Collection to `Hide items in this collection` then movies 
        without a collection like `The Incredible Hulk` will be hidden from the library view.
        
        To combat the problem above you set all collections to `Hide items in this collection` then create a collection set to 
        `Hide collection` and put every movie that you still want to display in that collection. 
        
        With the variability of collections generated by the Kometa maintaining a collection like this becomes very difficult, 
        so in order to automate it, you can use `plex_collectionless`. You just have to tell it what collections to exclude or 
        what collection prefixes to exclude.
        
        There are two attributes for `plex_collectionless`:
        
        * `exclude`: Exclude these Collections from being considered for collectionless. 
        * `exclude_prefix` Exclude Collections whose title or sort title starts with a prefix from being considered for 
        collectionless. 
         
        **At least one exclusion is required.**
        
        ```yaml
        collections:
          Collectionless:
            plex_collectionless:
              exclude_prefix:
                - "!"
                - "+"
                - "~"
              exclude: 
                - Marvel Cinematic Universe
            sort_title: ~_Collectionless
            collection_order: alpha
            collection_mode: hide
        ```
        
        * Both `exclude` and `exclude_prefix` can take multiple values as a List.
        * This is a known issue with Plex Collection and there is a [Feature Suggestion](https://forums.plex.tv/t/collection-display-issue/305406) detailing the issue more on their 
        forms.

=== "Search Options"

    When using a Plex Builder, there are three elements that correlate to Plex's Advanced Filters in the Web UI.
    
    -  **Attribute:** What attribute you wish to filter.
    -  **Modifier:** Which modifier to use.
    -  **Value:** Actual value to filter.
    
    These three elements combined would look like `attribute.modifier: value`, in a Builder this may be something like `title.not: Harry Potter` or `episode_added: 7`.

    Attribute and Value elements are mandatory, whilst modifiers are optional. Typically speaking, Plex will have a default modifier of "is" or "contains" if you do not specify a modifier.

    The majority of Smart and Dumb Builders utilize the same Search Options, meaning that the criteria for the builders is largely interchangeable between the two. Any deviation from this will be highlighted against the specific Builder.

    === "Boolean Filters"
        
        Boolean Filters take no modifier and can only be either `true` or `false`.
        
        #### Boolean Filter Attributes
        
        | Boolean Search      | Description            |             Movie<br>Libraries             |             Show<br>Libraries              |             Music<br>Libraries             |
        |:--------------------|:-----------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
        | `hdr`               | Is HDR                 | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `unmatched`         | Is Unmatched           | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `duplicate`         | Is Duplicate           | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `unplayed`          | Is Unplayed            | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `progress`          | Is In Progress         | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `trash`             | Is Trashed             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `unplayed_episodes` | Has Unplayed Episodes  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_unplayed`  | Has Episodes Unplayed  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_duplicate` | Has Duplicate Episodes |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_progress`  | Has Episode Progress   |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_unmatched` | Has Episodes Unmatched |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `show_unmatched`    | Has Shows Unmatched    |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `artist_unmatched`  | Is Artist's Unmatched  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_unmatched`   | Is Album's Unmatched   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_trash`       | Is Track Trashed       |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        
    === "Date Filters"
        
        Date filters can be used with either no modifier or with `.not`, `.before`, or `.after`.
        
        No date filter can take multiple values.
        

        #### Date Filter Attributes
        
        | Date Search           | Description                                                                        |             Movie<br>Libraries             |             Show<br>Libraries              |             Music<br>Libraries             |
        |:----------------------|:-----------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
        | `added`               | Uses the date added attribute to match                                             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_added`       | Uses the date added attribute of the show's episodes to match                      |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `release`             | Uses the release date attribute (originally available) to match                    | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_air_date`    | Uses the air date attribute (originally available) of the show's episodes to match |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `last_played`         | Uses the date last played attribute to match                                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_last_played` | Uses the date last played attribute of the show's episodes to match                |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `artist_added`        | Uses the Artist's date added attribute to match                                    |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `artist_last_played`  | Uses the Artist's last played attribute to match                                   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_last_played`   | Uses the Album's last played attribute to match                                    |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_added`         | Uses the Album's date added attribute to match                                     |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_released`      | Uses the Album's release date attribute to match                                   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_last_played`   | Uses the Track's date last played attribute to match                               |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_last_skipped`  | Uses the Track's date last skipped attribute to match                              |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_last_rated`    | Uses the Track's date last rated attribute to match                                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_added`         | Uses the Track's date added attribute to match                                     |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        
        ???+ tip "Date Filter Modifiers"
            
            | Date Modifier | Description                                                                                                                                                | Plex Web UI Display  |
            |:--------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------:|
            | No Modifier   | Matches every item where the date attribute is in the last X days<br>**Format:** number of days<br>**Example:** `30`                                       |   `is in the last`   |
            | `.not`        | Matches every item where the date attribute is not in the last X days<br>**Format:** number of days<br>**Example:** `30`                                   | `is not in the last` |
            | `.before`     | Matches every item where the date attribute is before the given date<br>**Format:** MM/DD/YYYY or `today` for the current day<br>**Example:** `01/01/2000` |     `is before`      |
            | `.after`      | Matches every item where the date attribute is after the given date<br>**Format:** MM/DD/YYYY or `today` for the current day<br>**Example:** `01/01/2000`  |      `is after`      |
            
    === "Number Filters"
    
        Number filters must use `.gt`, `.gte`, `.lt`, or `.lte` as a modifier only the rating filters can use `.rated`.
        
        No number filter can take multiple values.
        
        #### Number Filter Attributes
        
        | Number Search              | Description                                                                                 |             Movie<br>Libraries             |             Show<br>Libraries              |             Music<br>Libraries             |
        |:---------------------------|:--------------------------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
        | `duration`                 | Uses the duration attribute to match using minutes<br>**Minimum:** `0`                      | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `plays`                    | Uses the plays attribute to match<br>**Minimum:** `0`                                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_plays`            | Uses the Episode's plays attribute to match<br>**Minimum:** `0`                             |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `critic_rating`            | Uses the critic rating attribute to match<br>**Range:** `0.0` - `10.0`                      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `audience_rating`          | Uses the audience rating attribute to match<br>**Range:** `0.0` - `10.0`                    | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `user_rating`              | Uses the user rating attribute to match<br>**Range:** `0.0` - `10.0`                        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_user_rating`      | Uses the user rating attribute of the show's episodes to match<br>**Range:** `0.0` - `10.0` |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `year`<sup>1</sup>         | Uses the year attribute to match<br>**Minimum:** `0`                                        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_year`<sup>1</sup> | Uses the Episode's year attribute to match<br> **Minimum:** `0`                             |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `album_year`<sup>1</sup>   | Uses the Album's year attribute to match<br>**Minimum:** `0`                                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_decade`<sup>1</sup> | Uses the Album's decade attribute to match<br>**Minimum:** `0`                              |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_plays`              | Uses the Album's plays attribute to match<br>**Minimum:** `0`                               |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_plays`              | Uses the Track's plays attribute to match<br>**Minimum:** `0`                               |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_skips`              | Uses the Track's skips attribute to match<br>**Minimum:** `0`                               |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `artist_user_rating`       | Uses the Artist's user rating attribute to match<br>**Range:** `0.0` - `10.0`               |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_user_rating`        | Uses the Album's user rating attribute to match<br>**Range:** `0.0` - `10.0`                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_critic_rating`      | Uses the Album's critic rating attribute to match<br>**Range:** `0.0` - `10.0`              |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_user_rating`        | Uses the Track's user rating attribute to match<br>**Range:** `0.0` - `10.0`                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        
        <sup>1</sup> You can use `current_year` to have Kometa use the current years value. This can be combined with a 
        `-#` at the end to subtract that number of years. i.e. `current_year-2`

        ???+ tip "Number Filter Modifiers"
        
            | Number Modifier | Description                                                                                                                                             | Plex Web UI Display |
            |:----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------:|
            | `.gt`           | Matches every item where the number attribute is greater than the given number<br>**Format:** number<br>**Example:** `30`, `1995`, or `7.5`             |  `is greater than`  |
            | `.gte`          | Matches every item where the number attribute is greater than or equal to the given number<br>**Format:** number<br>**Example:** `30`, `1995`, or `7.5` |         N/A         |
            | `.lt`           | Matches every item where the number attribute is less than the given number<br>**Format:** number<br>**Example:** `30`, `1995`, or `7.5`                |   `is less than`    |
            | `.lte`          | Matches every item where the number attribute is less than or equal to the given number<br>**Format:** number<br>**Example:** `30`, `1995`, or `7.5`    |         N/A         |
            | `.rated`        | Matches every item either rated or not rated<br>**Format:** `true` or `false`                                                                           |         N/A         |
            
            * `.rated` only works for rating filters

    === "String Filters"
    
        String filters can be used with either no modifier or with `.not`, `.is`, `.isnot`, `.begins`, or `.ends`.
        
        String filter can take multiple values **only as a list**.
        
        #### String Filter Attributes
        
        | String Search        | Description                                              |             Movie<br>Libraries             |             Show<br>Libraries              |             Music<br>Libraries             |
        |:---------------------|:---------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
        | `title`              | Uses the title attribute to match                        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_title`      | Uses the title attribute of the show's episodes to match |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `studio`             | Uses the studio attribute to match                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `edition`            | Uses the edition attribute to match                      | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `artist_title`       | Uses the Artist's Title attribute to match               |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_title`        | Uses the Album's Title attribute to match                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_title`        | Uses the Track's Title attribute to match                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_record_label` | Uses the Album's Record Label attribute to match         |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |

        ???+ tip "String Filter Modifiers"
        
            | String Modifier | Description                                                                    | Plex Web UI Display |
            |:----------------|:-------------------------------------------------------------------------------|:-------------------:|
            | No Modifier     | Matches every item where the attribute contains the given string               |     `contains`      |
            | `.not`          | Matches every item where the attribute does not contain the given string       | `does not contain`  |
            | `.is`           | Matches every item where the attribute exactly matches the given string        |        `is`         |
            | `.isnot`        | Matches every item where the attribute does not exactly match the given string |      `is not`       |
            | `.begins`       | Matches every item where the attribute begins with the given string            |    `begins with`    |
            | `.ends`         | Matches every item where the attribute ends with the given string              |     `ends with`     |

    === "Tag Filters"
        
        Tag filters can be used with either no modifier or with `.not` except for `decade` and `resolution` which can only be 
        used with no modifier.
        
        Tag filter can take multiple values as a **list or a comma-separated string**.
         
        #### Tag Filter Attributes
        
        | Tag Search                 | Description                                                                 |             Movie<br>Libraries             |             Show<br>Libraries              |             Music<br>Libraries             |
        |:---------------------------|:----------------------------------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
        | `actor`                    | Uses the actor tags to match                                                | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_actor`            | Uses the episode actor tags to match                                        |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `audio_language`           | Uses the audio language tags to match                                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `collection`               | Uses the collection tags to match for top level collections                 | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `season_collection`        | Uses the collection tags to match for season collections                    |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_collection`       | Uses the collection tags to match for episode collections                   |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `content_rating`           | Uses the content rating tags to match                                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `country`                  | Uses the country tags to match                                              | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `decade`<sup>1</sup>       | Uses the year tag to match the decade                                       | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `director`                 | Uses the director tags to match                                             | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `genre`                    | Uses the genre tags to match                                                | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `label`                    | Uses the label tags to match for top level collections                      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `season_label`             | Uses the label tags to match for season collections                         |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_label`            | Uses the label tags to match for episode collections                        |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `network`                  | Uses the network tags to match<br>**Only works with the New Plex TV Agent** |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `producer`                 | Uses the actor tags to match                                                | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `resolution`               | Uses the resolution tags to match                                           | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `subtitle_language`        | Uses the subtitle language tags to match                                    | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `writer`                   | Uses the writer tags to match                                               | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `year`<sup>1</sup>         | Uses the year tag to match                                                  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `episode_year`<sup>1</sup> | Uses the year tag to match                                                  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
        | `artist_genre`             | Uses the Artist's Genre attribute to match                                  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `artist_collection`        | Uses the Artist's Collection attribute to match                             |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `artist_country`           | Uses the Artist's Country attribute to match                                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `artist_mood`              | Uses the Artist's Mood attribute to match                                   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `artist_style`             | Uses the Artist's Style attribute to match                                  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `artist_label`             | Uses the Artist's Label attribute to match                                  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_genre`              | Uses the Album's Genre attribute to match                                   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_mood`               | Uses the Album's Mood attribute to match                                    |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_style`              | Uses the Album's Style attribute to match                                   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_format`             | Uses the Album's Format attribute to match                                  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_type`               | Uses the Album's Type attribute to match                                    |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_collection`         | Uses the Album's Collection attribute to match                              |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_source`             | Uses the Album's Source attribute to match                                  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `album_label`              | Uses the Album's Label attribute to match                                   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_mood`               | Uses the Track's Mood attribute to match                                    |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_source`             | Uses the Track's Source attribute to match                                  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        | `track_label`              | Uses the Track's Label attribute to match                                   |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
        
        <sup>1</sup> You can use `current_year` to have Kometa use the current years value. This can be combined with a 
        `-#` at the end to subtract that number of years. i.e. `current_year-2`

        ???+ tip "Tag Filter Modifiers" 

            | Tag Modifier | Description                                                            | Plex Web UI Display |
            |:-------------|:-----------------------------------------------------------------------|:-------------------:|
            | No Modifier  | Matches every item where the attribute matches the given string        |        `is`         |
            | `.not`       | Matches every item where the attribute does not match the given string |      `is not`       |


=== "Sort Options"

    The majority of Smart and Dumb Builders utilize the same Sort Options. Any deviation from this will be highlighted against the specific Builder.
 
    | Sort Option                                     | Description                                         |                   Movies                   |                   Shows                    |                  Seasons                   |                  Episodes                  |                  Artists                   |                   Albums                   |                   Tracks                   |
    |:------------------------------------------------|:----------------------------------------------------|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|:------------------------------------------:|
    | `title.asc`<br>`title.desc`                     | Sort by Title                                       | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | `season.asc`<br>`season.desc`                   | Sort by Season                                      |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `show.asc`<br>`show.desc`                       | Sort by Show                                        |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `album_artist.asc`<br>`album_artist.desc`       | Sort by Album Artist                                |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | `artist.asc`<br>`artist.desc`                   | Sort by Artist                                      |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
    | `album.asc`<br>`album.desc`                     | Sort by Album                                       |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
    | `year.asc`<br>`year.desc`                       | Sort by Year                                        | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `release.asc`<br>`release.desc`                 | Sort by Release Date (Originally Available)         | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `episode_release.asc`<br>`episode_release.desc` | Sort by Episode Release Date (Originally Available) |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `critic_rating.asc`<br>`critic_rating.desc`     | Sort by Critic Rating                               | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `audience_rating.asc`<br>`audience_rating.desc` | Sort by Audience Rating                             | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `user_rating.asc`<br>`user_rating.desc`         | Sort by User Rating                                 | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | `content_rating.asc`<br>`content_rating.desc`   | Sort by Content Rating                              | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `duration.asc`<br>`duration.desc`               | Sort by Duration                                    | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
    | `progress.asc`<br>`progress.desc`               | Sort by Progress                                    |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `played.asc`<br>`played.desc`                   | Sort by Date Last Played                            |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | `plays.asc`<br>`plays.desc`                     | Sort by Number of Plays                             | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | `unplayed.asc`<br>`unplayed.desc`               | Sort by Unplayed                                    |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `episode_added.asc`<br>`episode_added.desc`     | Sort by Last Episode Date Added                     |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `added.asc`<br>`added.desc`                     | Sort by Date Added                                  | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |
    | `viewed.asc`<br>`viewed.desc`                   | Sort by Date Last Viewed                            | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `rated.asc`<br>`rated.desc`                     | Sort by Date Last Rated                             |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
    | `popularity.asc`<br>`popularity.desc`           | Sort by Popularity                                  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
    | `resolution.asc`<br>`resolution.desc`           | Sort by Resolution                                  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  |
    | `bitrate.asc`<br>`bitrate.desc`                 | Sort by Bitrate                                     | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |  :fontawesome-solid-circle-xmark:{ .red }  |  :fontawesome-solid-circle-xmark:{ .red }  | :fontawesome-solid-circle-check:{ .green } |
    | `random`                                        | Sort by Random                                      | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } | :fontawesome-solid-circle-check:{ .green } |

    ## Sort Option Examples

    ```yaml
    collections:
      Best 2024 Movies:
        smart_filter:
          limit: 100
          all:
            year: 2024
          sort_by: audience_rating.desc
    ```

    ```yaml
    collections:
      Newly Released Movies:
        smart_filter:
          limit: 100
          all:
            release: 30
          sort_by: release.desc
    ```

=== "Builder Attributes"

    The majority of Smart and Dumb Builders utilize the same Builder Attributes. Any deviation from this will be highlighted against the specific Builder.

    | Attribute  | Description & Values                                                                                                                                                                                                                               |
    |:-----------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    | `limit`    | **Description:** The max number of item for the filter.<br>**Default:** `all`<br>**Values:** `all` or a number greater than 0                                                                                                                      |
    | `sort_by`  | **Description:** This will control how the filter is sorted in your library. You can do a multi-level sort using a list.<br>**Default:** `random`<br>**Values:** Any sort options for your filter type in the [Sorts Options Table](#sort-options) |
    | `validate` | **Description:** Determines if a collection will fail on a validation error<br>**Default:** `true`<br>**Values**: `true` or `false`                                                                                                                |
