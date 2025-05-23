---
hide:
  - toc
---
# Collectionless Collection

The `collectionless` Default Collection File is used to create a 
[Collectionless collection](../../files/builders/plex.md#plex-collectionless) to help Show/Hide Movies/Shows properly in 
your library.

![](../images/collectionless.png)

## Requirements & Recommendations

Supported Library Types: Movie, Show

Requirements: 

* This file needs to run last under `collection_files`.

* All other normal collections must use `collection_mode: hide_items`.

* Disable the `Minimum automatic collection size` option when using the `Plex Movie` Agent. (Use the 
[`franchise` Default](../movie/franchise.md) for automatic collections)

## Collection

| Collection       | Description                                                                                                                            |
| :--------------- | :------------------------------------------------------------------------------------------------------------------------------------- |
| `Collectionless` | [Collectionless collection](../../files/builders/plex.md#plex-collectionless) to help Show/Hide Movies/Shows properly in your library. |

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  Movies:
    template_variables:
      collection_mode: hide_items
    collection_files:
      - default: collectionless
  TV Shows:
    template_variables:
      collection_mode: hide_items
    collection_files:
      - default: collectionless
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

        | Variable                 | Description & Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
        | :----------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | `collection_order`       | **Description:** Changes the Collection Order for all collections in this file.<br>**Default:** `alpha`<br>**Values:**<table class="clearTable"><tr><td>`release`</td><td>Order Collection by Release Dates</td></tr><tr><td>`alpha`</td><td>Order Collection Alphabetically</td></tr><tr><td>`custom`</td><td>Order Collection Via the Builder Order</td></tr><tr><td>[Any `plex_search` Sort Option](../../files/builders/plex.md#sort-options)</td><td>Order Collection by any `plex_search` Sort Option</td></tr></table> |
        | `exclude_prefix`         | **Description:** Overrides the default exclude_prefix list. Exclude Collections with one of these prefixes from being considered for collectionless.<br>**Default:** default exclude_prefix list<br>**Values:** List of Prefixes                                                                                                                                                                                                                                                                                              |  |
        | `exclude`                | **Description:** Exclude these Collections from being considered for collectionless.<br>**Values:** List of Collections                                                                                                                                                                                                                                                                                                                                                                                                       |
        | `name_collectionless`    | **Description:** Changes the name of the collection.<br>**Values:** New Collection Name                                                                                                                                                                                                                                                                                                                                                                                                                                       |
        | `sort_title`             | **Description:** Sets the sort title for the collection.<br>**Default:** `~_Collectionless`<br>**Values:** Any String                                                                                                                                                                                                                                                                                                                                                                                                         |
        | `summary_collectionless` | **Description:** Changes the summary of the collection.<br>**Values:** New Collection Summary                                                                                                                                                                                                                                                                                                                                                                                                                                 |
        | `url_poster`             | **Description:** Changes the poster url of the collection.<br>**Values:** URL directly to the Image                                                                                                                                                                                                                                                                                                                                                                                                                           |

???+ example "Example Template Variable Amendments"

    The below is an example config.yml extract with some Template Variables added in to change how the file works.

    Click the :fontawesome-solid-circle-plus: icon to learn more

    ```yaml
    libraries:
      Movies:
        template_variables:
          collection_mode: hide_items
        collection_files:
          - default: collectionless
            template_variables:
              exclude:
                - Marvel Cinematic Universe
              collection_order: release
    ```

## Default Values

Unless you customize them as described above, these collections use default lists and searches to create the collections.

If you are interested in customizing the default values, you can find that information [here](#template-variables).

If you are interested in seeing what those default builders are, you can find that information [here](../sources.md).
