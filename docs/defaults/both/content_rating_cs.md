---
hide:
  - toc
---
# Common Sense Media Content Rating Collections

The `content_rating_cs` Default Collection File is used to dynamically create collections based on the content ratings 
available in your library.

If you do not use the Common Sense-based rating system within Plex, this file will attempt to match the ratings in your 
library to the respective rating system.

![](../images/content_rating_cs.png)

## Requirements & Recommendations

Supported Library Types: Movie, Show

Recommendations: Use the 
[Mass Content Rating Update Library Operation](../../config/operations.md#mass-content-rating-update) with either 
`mdb_commonsense` or `mdb_commonsense0` to update Plex to the Common Sense Rating.

## <a id="collection_section"></a>Collections Section 110

| Collection                                                        | Key                              | Description                                                                           |
| :---------------------------------------------------------------- | :------------------------------- | :------------------------------------------------------------------------------------ |
| `<<Content Rating>> Movies/Shows`<br>**Example:** `Age 5+ Movies` | `<<Number>>`<br>**Example:** `5` | Collection of Movies/Shows that have this Content Rating.                             |
| `Not Rated Movies/Shows`                                          | `other`                          | Collection of Movies/Shows that are Unrated, Not Rated or any other uncommon Ratings. |
| `Ratings Collections`                                             | `separator`                      | [Separator Collection](../separators.md) to denote the Section of Collections.        |

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  Movies:
    collection_files:
      - default: content_rating_cs
  TV Shows:
    collection_files:
      - default: content_rating_cs
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

        | Variable                      | Description & Values                                                                                                                                                                                                                                                    |
        | :---------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | `addons`                      | **Description:** Overrides the [default addons dictionary](#default-values). Defines how multiple keys can be combined under a parent key. The parent key doesn't have to already exist in Plex<br>**Values:** Dictionary List of Content Ratings found in your library |
        | `append_addons`               | **Description:** Appends to the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of Content Ratings found in your library                                                                                                                   |
        | `append_include`              | **Description:** Appends to the [default include list](#default-values).<br>**Values:** List of Content Ratings found in your library                                                                                                                                   |
        | `exclude`                     | **Description:** Exclude these Content Ratings from creating a Dynamic Collection.<br>**Values:** List of Content Ratings found in your library                                                                                                                         |
        | `include`                     | **Description:** Overrides the [default include list](#default-values).<br>**Values:** List of Content Ratings found in your library                                                                                                                                    |
        | `limit_<<key>>`<sup>1</sup>   | **Description:** Changes the Builder Limit of the [key's](#collection_section) collection.<br>**Default:** `limit`<br>**Values:** Number Greater than 0                                                                                                                 |
        | `limit`                       | **Description:** Changes the Builder Limit for all collections in a Defaults File.<br>**Values:** Number Greater than 0                                                                                                                                                 |
        | `name_format`                 | **Description:** Changes the title format of the Dynamic Collections.<br>**Default:** `Age <<key_name>>+ <<library_translationU>>s`<br>**Values:** Any string with `<<key_name>>` in it.                                                                                |
        | `remove_addons`               | **Description:** Removes from the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of Content Ratings found in your library                                                                                                                 |
        | `remove_include`              | **Description:** Removes from the [default include list](#default-values).<br>**Values:** List of Content Ratings found in your library                                                                                                                                 |
        | `sort_by_<<key>>`<sup>1</sup> | **Description:** Changes the Smart Filter Sort of the [key's](#collection_section) collection.<br>**Default:** `sort_by`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                                     |
        | `sort_by`                     | **Description:** Changes the Smart Filter Sort for all collections in a Defaults File.<br>**Default:** `release.desc`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                                        |
        | `summary_format`              | **Description:** Changes the summary format of the Dynamic Collections.<br>**Default:** `<<library_translationU>>s that are rated <<key_name>> accorfing to the Common Sense Rating System.`<br>**Values:** Any string.                                                 |

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
          - default: content_rating_cs
            template_variables:
              sep_style: blue #(1)!
              use_other: false #(2)!
              append_addons:
                German 18: #(3)!
                  - "de/18" #(4)!
              sort_by: title.asc
    ```

    1.  Use the blue [Separator Style](../separators.md#separator-styles)
    2.  Do not create a "Not Rated Movies/Shows" collection
    3.  Defines a collection which will be called "German 18", this does not need to already exist in your library
    4.  Adds the "de/18" content rating to the "German 18" addon list, "de/18" must exist in your library if the "German
    18" content rating does not

## Default Values

Unless you customize them as described above, these collections use default lists and searches to create the collections.

If you are interested in customizing the default values, you can find that information [here](#template-variables).

If you are interested in seeing what those default builders are, you can find that information [here](../sources.md).
