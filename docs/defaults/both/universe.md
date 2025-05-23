---
hide:
  - toc
---
# Universe Collections

The `universe` Default Collection File is used to create collections based on popular Movie universes (such as the 
Marvel Cinematic Universe or Wizarding World).

![](../images/universe.png)

## Requirements & Recommendations

Supported Library Types: Movie & Show

## <a id="collection_section"></a>Collections Section 040

| Collection                   | Key         | Description                                                                    |
| :--------------------------- | :---------- | :----------------------------------------------------------------------------- |
| `Alien / Predator`           | `avp`       | Collection of Movies in the Alien / Predator Universe                          |
| `Arrowverse`                 | `arrow`     | Collection of Movies in the The Arrow Universe                                 |
| `DC Animated Universe`       | `dca`       | Collection of Movies in the DC Animated Universe                               |
| `DC Extended Universe`       | `dcu`       | Collection of Movies in the DC Extended Universe                               |
| `Fast & Furious`             | `fast`      | Collection of Movies in the Fast & Furious Universe                            |
| `In Association with Marvel` | `marvel`    | Collection of Movies in the Marvel Universe (but not part of MCU)              |
| `Marvel Cinematic Universe`  | `mcu`       | Collection of Movies in the Marvel Cinematic Universe                          |
| `Middle Earth`               | `middle`    | Collection of Movies in the Middle Earth Universe                              |
| `Rocky / Creed`              | `rocky`     | Collection of Movies in the Rocky / Creed Universe                             |
| `Star Trek`                  | `trek`      | Collection of Movies in the Star Trek Universe                                 |
| `Star Wars Universe`         | `star`      | Collection of Movies in the Star Wars Universe                                 |
| `The Mummy Universe`         | `mummy`     | Collection of Movies in the The Mummy Universe                                 |
| `Universe Collections`       | `separator` | [Separator Collection](../separators.md) to denote the Section of Collections. |
| `View Askewverse`            | `askew`     | Collection of Movies in the The View Askew Universe                            |
| `Wizarding World`            | `wizard`    | Collection of Movies in the Wizarding World Universe                           |
| `X-Men Universe`             | `xmen`      | Collection of Movies in the X-Men Universe                                     |

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  Movies:
    collection_files:
      - default: universe
  TV Shows:
    collection_files:
      - default: universe
```

## Template Variables

Template Variables can be used to manipulate the file in various ways to slightly change how it works without having to 
make your own local copy.

Note that the `template_variables:` section only needs to be used if you do want to actually change how the defaults 
work. Any value not specified will use its default value if it has one if not it's just ignored.

??? abstract "Variable Lists (click to expand)"

    * **File-Specific Template Variables** are variables available specifically for this Kometa Defaults File.

    * **Shared Template Variables** are additional variables shared across the Kometa Defaults.

    * **Shared Separator Variables** are additional variables available since this Default contains a 
    [Separator](../separators.md).

    === "File-Specific Template Variables"

        | Variable                               | Description & Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
        | :------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | `append_data`                          | **Description:** Appends to the [default data dictionary](#default-values).<br>**Values:** Dictionary List of keys/names                                                                                                                                                                                                                                                                                                                                                                                                                               |
        | `collection_order_<<key>>`<sup>1</sup> | **Description:** Changes the Collection Order of the [key's](#collection_section) collection.<br>**Default:** `collection_order`<br>**Values:**<table class="clearTable"><tr><td>`release`</td><td>Order Collection by Release Dates</td></tr><tr><td>`alpha`</td><td>Order Collection Alphabetically</td></tr><tr><td>`custom`</td><td>Order Collection Via the Builder Order</td></tr><tr><td>[Any `plex_search` Sort Option](../../files/builders/plex.md#sort-options)</td><td>Order Collection by any `plex_search` Sort Option</td></tr></table> |
        | `collection_order`                     | **Description:** Changes the Collection Order for all collections in a Defaults File.<br>**Default:** `custom`<br>**Values:**<table class="clearTable"><tr><td>`release`</td><td>Order Collection by Release Dates</td></tr><tr><td>`alpha`</td><td>Order Collection Alphabetically</td></tr><tr><td>`custom`</td><td>Order Collection Via the Builder Order</td></tr><tr><td>[Any `plex_search` Sort Option](../../files/builders/plex.md#sort-options)</td><td>Order Collection by any `plex_search` Sort Option</td></tr></table>                   |
        | `data`                                 | **Description:** Overrides the [default data dictionary](#default-values). Defines the data that the custom dynamic collection processes.<br>**Values:** Dictionary List of keys/names                                                                                                                                                                                                                                                                                                                                                                 |
        | `exclude`                              | **Description:** Exclude these Universes from creating a Dynamic Collection.<br>**Values:** List of Universes                                                                                                                                                                                                                                                                                                                                                                                                                                          |
        | `imdb_list_<<key>>`<sup>1</sup>        | **Description:** Adds the Movies in the IMDb List to the [key's](#collection_section) collection.<br>**Values:** List of IMDb List URLs                                                                                                                                                                                                                                                                                                                                                                                                                |  |  |
        | `mdblist_list_<<key>>`<sup>1</sup>     | **Description:** Adds the Movies in the MDBList List to the [key's](#collection_section) collection. Overrides the [default mdblist_url](#default-values) for that collection if used.<br>**Values:** List of MDBList List URLs                                                                                                                                                                                                                                                                                                                        |  |  |  |
        | `minimum_items`                        | **Description:** Controls the minimum items that the collection must have to be created.<br>**Default:** `2`<br>**Values:** Any number                                                                                                                                                                                                                                                                                                                                                                                                                 |
        | `name_mapping_<<key>>`<sup>1</sup>     | **Description:** Sets the name mapping value for using assets of the [key's](#collection_section) collection. <br>**Values:** Any String                                                                                                                                                                                                                                                                                                                                                                                                               |
        | `remove_data`                          | **Description:** Removes from the [default data dictionary](#default-values).<br>**Values:** List of keys to remove                                                                                                                                                                                                                                                                                                                                                                                                                                    |
        | `sync_mode_<<key>>`<sup>1</sup>        | **Description:** Changes the Sync Mode of the [key's](#collection_section) collection.<br>**Default:** `sync_mode`<br>**Values:**<table class="clearTable"><tr><td>`sync`</td><td>Add and Remove Items based on Builders</td></tr><tr><td>`append`</td><td>Only Add Items based on Builders</td></tr></table>                                                                                                                                                                                                                                          |
        | `sync_mode`                            | **Description:** Changes the Sync Mode for all collections in a Defaults File.<br>**Default:** `sync`<br>**Values:**<table class="clearTable"><tr><td>`sync`</td><td>Add and Remove Items based on Builders</td></tr><tr><td>`append`</td><td>Only Add Items based on Builders</td></tr></table>                                                                                                                                                                                                                                                       |
        | `trakt_list_<<key>>`<sup>1</sup>       | **Description:** Adds the Movies in the Trakt List to the [key's](#collection_section) collection. Overrides the [default trakt_url](#default-values) for that collection if used.<br>**Values:** List of Trakt List URLs                                                                                                                                                                                                                                                                                                                              |  |  |  |

        1. Each default collection has a [`key`](#collection_section) that you must replace `<<key>>` with when using 
        this Template Variable. These keys are found in the table at the top of this page.

    === "Shared Template Variables"

        {%
          include-markdown "../collection_variables.md"
        %}

    === "Shared Separator Variables"

        {%
          include-markdown "../separator_variables.md"
        %}
    
???+ example "Example Template Variable Amendments"

    The below is an example config.yml extract with some Template Variables added in to change how the file works.

    Click the :fontawesome-solid-circle-plus: icon to learn more
    
    ```yaml
    libraries:
      Movies:
        collection_files:
          - default: universe
            template_variables:
              sep_style: salmon #(1)!
              collection_order: release #(2)!
              radarr_add_missing: true #(3)!
              append_data:
                monster: MonsterVerse #(4)!
              trakt_list_monster: https://trakt.tv/users/rzepkowski/lists/monsterverse-movies #(5)!
    ```

    1.  Use the salmon [Separator Style](../separators.md#separator-styles)
    2.  Sort the Universe collections by release date
    3.  Send missing items in your library from the source lists to Radarr
    4.  Create a new universe called "MonsterVerse", the key for this universe will be "monster"
    5.  Add a trakt list to the "monster" key

## Default Values

Unless you customize them as described above, these collections use default lists and searches to create the collections.

If you are interested in customizing the default values, you can find that information [here](#template-variables).

If you are interested in seeing what those default builders are, you can find that information [here](../sources.md).
