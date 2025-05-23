---
hide:
  - toc
---
# Franchise Collections

The `franchise` Default Collection File is used to create collections based on popular TV Show franchises, and can be 
used as a replacement to the TMDb Collections that Plex creates out-of-the-box.

Unlike most Default Collection Files, Franchise works by placing collections inline with the main library items if your 
library allows it. For example, the "Pretty Little Liars" franchise collection will appear next to the "Pretty Little 
Liars" show in your library so that you have easy access to the other shows in the franchise.

**[This file has a Movie Library Counterpart.](../movie/franchise.md)**

![](../images/showfranchise.png)

## Requirements & Recommendations

Supported Library Types: Show

## <a id="collection_section"></a>Collections

| Collection                                                  | Key                                                 | Description                                        |
| :---------------------------------------------------------- | :-------------------------------------------------- | :------------------------------------------------- |
| `<<Collection Name>>`<br>**Example:** `Pretty Little Liars` | `<<Starting TMDb Show ID>>`<br>**Example:** `31917` | Collection of Shows specified for this Collection. |

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  TV Shows:
    collection_files:
      - default: franchise
```

## Template Variables

Template Variables can be used to manipulate the file in various ways to slightly change how it works without having to 
make your own local copy.

Note that the `template_variables:` section only needs to be used if you do want to actually change how the defaults 
work. Any value not specified will use its default value if it has one if not it's just ignored.

??? abstract "Variable Lists (click to expand)"

    * **File-Specific Template Variables** are variables available specifically for this Kometa Defaults File.

    ???+ warning

        [Shared Collection Variables](../collection_variables.md) are NOT available to this Defaults File.

    === "File-Specific Template Variables"

        | Variable                                 | Description & Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
        | :--------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | `addons`                                 | **Description:** Overrides the [default addons dictionary](#default-values). Defines how multiple keys can be combined under a parent key. The parent key doesn't have to already exist in Plex<br>**Values:** Dictionary List of TMDb Show IDs                                                                                                                                                                                                                                                                                                        |
        | `append_addons`                          | **Description:** Appends to the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of TMDb Show IDs                                                                                                                                                                                                                                                                                                                                                                                                                          |
        | `append_data`                            | **Description:** Appends to the [default data dictionary](#default-values).<br>**Values:** Dictionary List of TMDb Main Show ID                                                                                                                                                                                                                                                                                                                                                                                                                        |
        | `build_collection`                       | **Description:** Controls if you want the collection to actually be built. i.e. you may just want these shows sent to Sonarr.<br>**Values:** `false` to not build the collection                                                                                                                                                                                                                                                                                                                                                                       |
        | `collection_mode`                        | **Description:** Controls the collection mode of all collections in this file.<br>**Values:**<table class="clearTable"><tr><td>`default`</td><td>Library default</td></tr><tr><td>`hide`</td><td>Hide Collection</td></tr><tr><td>`hide_items`</td><td>Hide Items in this Collection</td></tr><tr><td>`show_items`</td><td>Show this Collection and its Items</td></tr></table>                                                                                                                                                                        |
        | `collection_order_<<key>>`<sup>1</sup>   | **Description:** Changes the Collection Order of the [key's](#collection_section) collection.<br>**Default:** `collection_order`<br>**Values:**<table class="clearTable"><tr><td>`release`</td><td>Order Collection by Release Dates</td></tr><tr><td>`alpha`</td><td>Order Collection Alphabetically</td></tr><tr><td>`custom`</td><td>Order Collection Via the Builder Order</td></tr><tr><td>[Any `plex_search` Sort Option](../../files/builders/plex.md#sort-options)</td><td>Order Collection by any `plex_search` Sort Option</td></tr></table> |
        | `collection_order`                       | **Description:** Changes the Collection Order for all collections in this file.<br>**Values:**<table class="clearTable"><tr><td>`release`</td><td>Order Collection by Release Dates</td></tr><tr><td>`alpha`</td><td>Order Collection Alphabetically</td></tr><tr><td>`custom`</td><td>Order Collection Via the Builder Order</td></tr><tr><td>[Any `plex_search` Sort Option](../../files/builders/plex.md#sort-options)</td><td>Order Collection by any `plex_search` Sort Option</td></tr></table>                                                  |
        | `collection_section`                     | **Description:** Adds a sort title with this collection sections.<br>**Values:** Any number                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
        | `data`                                   | **Description:** Overrides the [default data dictionary](#default-values). Defines the data that the custom dynamic collection processes.<br>**Values:** Dictionary List of TMDb Main Show ID                                                                                                                                                                                                                                                                                                                                                          |
        | `exclude`                                | **Description:** Exclude these Collections from creating a Dynamic Collection.<br>**Values:** List of Collection IDs                                                                                                                                                                                                                                                                                                                                                                                                                                   |
        | `item_sonarr_tag_<<key>>`<sup>1</sup>    | **Description:** Used to append a tag in Sonarr for every show found by the builders that's in Sonarr of the [key's](#collection_section) collection.<br>**Default:** `item_sonarr_tag`<br>**Values:** List or comma-separated string of tags                                                                                                                                                                                                                                                                                                          |
        | `item_sonarr_tag`                        | **Description:** Used to append a tag in Sonarr for every show found by the builders that's in Sonarr for all collections in a Defaults File.<br>**Values:** List or comma-separated string of tags                                                                                                                                                                                                                                                                                                                                                    |
        | `minimum_items`                          | **Description:** Controls the minimum items that the collection must have to be created.<br>**Default:** `2`<br>**Values:** Any number                                                                                                                                                                                                                                                                                                                                                                                                                 |
        | `name_mapping_<<key>>`<sup>1</sup>       | **Description:** Sets the name mapping value for using assets of the [key's](#collection_section) collection.<br>**Values:** Any String                                                                                                                                                                                                                                                                                                                                                                                                                |
        | `order_<<key>>`<sup>1</sup>              | **Description:** Controls the sort order of the collections in their collection section.<br>**Values:** Any number                                                                                                                                                                                                                                                                                                                                                                                                                                     |
        | `remove_addons`                          | **Description:** Removes from the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of TMDb Show IDs                                                                                                                                                                                                                                                                                                                                                                                                                        |
        | `remove_data`                            | **Description:** Removes from the [default data dictionary](#default-values).<br>**Values:** List of TMDb Main Show IDs to remove                                                                                                                                                                                                                                                                                                                                                                                                                      |
        | `sonarr_add_missing_<<key>>`<sup>1</sup> | **Description:** Override Sonarr `add_missing` attribute of the [key's](#collection_section) collection.<br>**Default:** `sonarr_add_missing`<br>**Values:** `true` or `false`                                                                                                                                                                                                                                                                                                                                                                         |
        | `sonarr_add_missing`                     | **Description:** Override Sonarr `add_missing` attribute for all collections in a Defaults File.<br>**Values:** `true` or `false`                                                                                                                                                                                                                                                                                                                                                                                                                      |
        | `sonarr_folder_<<key>>`<sup>1</sup>      | **Description:** Override Sonarr `root_folder_path` attribute of the [key's](#collection_section) collection.<br>**Default:** `sonarr_folder`<br>**Values:** Folder Path                                                                                                                                                                                                                                                                                                                                                                               |
        | `sonarr_folder`                          | **Description:** Override Sonarr `root_folder_path` attribute for all collections in a Defaults File.<br>**Values:** Folder Path                                                                                                                                                                                                                                                                                                                                                                                                                       |
        | `sonarr_tag_<<key>>`<sup>1</sup>         | **Description:** Override Sonarr `tag` attribute of the [key's](#collection_section) collection.<br>**Default:** `sonarr_tag`<br>**Values:** List or comma-separated string of tags                                                                                                                                                                                                                                                                                                                                                                    |
        | `sonarr_tag`                             | **Description:** Override Sonarr `tag` attribute for all collections in a Defaults File.<br>**Values:** List or comma-separated string of tags                                                                                                                                                                                                                                                                                                                                                                                                         |
        | `sort_title_<<key>>`<sup>1</sup>         | **Description:** Sets the sort title of the [key's](#collection_section) collection.<br>**Default:** `sort_title`<br>**Values:** Any String                                                                                                                                                                                                                                                                                                                                                                                                            |
        | `sort_title`                             | **Description:** Sets the sort title for all collections. Use `<<collection_name>>` to use the collection name. **Example:** `"!02_<<collection_name>>"`<br>**Values:** Any String with `<<collection_name>>`                                                                                                                                                                                                                                                                                                                                          |
        | `summary_<<key>>`<sup>1</sup>            | **Description:** Changes the summary of the [key's](#collection_section) collection.<br>**Values:** New Collection Summary                                                                                                                                                                                                                                                                                                                                                                                                                             |
        | `sync_mode_<<key>>`<sup>1</sup>          | **Description:** Changes the Sync Mode of the [key's](#collection_section) collection.<br>**Default:** `sync_mode`<br>**Values:**<table class="clearTable"><tr><td>`sync`</td><td>Add and Remove Items based on Builders</td></tr><tr><td>`append`</td><td>Only Add Items based on Builders</td></tr></table>                                                                                                                                                                                                                                          |
        | `sync_mode`                              | **Description:** Changes the Sync Mode for all collections in a Defaults File.<br>**Default:** `sync`<br>**Values:**<table class="clearTable"><tr><td>`sync`</td><td>Add and Remove Items based on Builders</td></tr><tr><td>`append`</td><td>Only Add Items based on Builders</td></tr></table>                                                                                                                                                                                                                                                       |

        1. Each default collection has a [`key`](#collection_section) that you must replace `<<key>>` with when using 
        this Template Variable. These keys are found in the table at the top of this page.
    
    ???+ example "Example Template Variable Amendments"

        The below is an example config.yml extract with some Template Variables added in to change how the file works.
    
        Click the :fontawesome-solid-circle-plus: icon to learn more
        
        ```yaml
        libraries:
          TV Shows:
            collection_files:
              - default: franchise
                template_variables:
                  append_data:
                    "31917": Pretty Little Liars  #(1)!
                  append_addons:
                    31917: [46958, 79863, 110531]  #(2)!
                  sonarr_add_missing: true  #(3)!
        ```
    
        1.  Add [TMDb Show 31917](https://www.themoviedb.org/tv/31917-pretty-little-liars) to the data dictionary
        2.  Add [TMDb Shows 46958](https://www.themoviedb.org/tv/46958), [79863](https://www.themoviedb.org/tv/79863) 
        and [110531](https://www.themoviedb.org/tv/110531) as addons of [TMDb Show 
        31917](https://www.themoviedb.org/tv/31917-pretty-little-liars) so that they appear in the same collection
        3.  Add items missing from your library in Plex to Sonarr

## Default Values

Unless you customize them as described above, these collections use default lists and searches to create the collections.

If you are interested in customizing the default values, you can find that information [here](#template-variables).

If you are interested in seeing what those default builders are, you can find that information [here](../sources.md).
