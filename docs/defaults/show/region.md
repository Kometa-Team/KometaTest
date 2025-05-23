---
hide:
  - toc
---
# Region Collections

The `region` Default Collection File is used to dynamically create collections based on the countries within your 
library. The collection aims to be inclusive, with all 230 countries incorporated into 39 countries or collections of 
countries. Some care has been taken to ensure all countries are included, and the groupings won't fit well with 
everyone's collections.  Western and Southern Europe, Oceania, and North America could be useful groupings for those 
libraries with more of an Asian focus, for instance. Please see the comments in the yml below where a decision point 
might be seen as controversial. You are welcome to edit this to fit your own audience's needs.

**[This file has a Movie Library Counterpart.](../movie/region.md)**

![](../images/region1.png)

## Requirements & Recommendations

Supported Library Types: Show

## <a id="collection_section"></a>Collections Section 081

| Collection                            | Key                                                    | Description                                                                    |
| :------------------------------------ | :----------------------------------------------------- | :----------------------------------------------------------------------------- |
| `<<Region>>`<br>**Example:** `German` | `<<2 digit ISO 3166-1 code>>`<br>**Example:** `German` | Collection of TV Shows that have this Region.                                  |
| `Other Regions`                       | `other`                                                | Collection of TV Shows that are in other uncommon Regions.                     |
| `Region Collections`                  | `separator`                                            | [Separator Collection](../separators.md) to denote the Section of Collections. |

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  TV Shows:
    collection_files:
      - default: region
```

## Color Style

Below is a screenshot of the alternative Color (`color`) style which can be set via the `style` Template Variable.

![](../images/region2.png)

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

        | Variable                        | Description & Values                                                                                                                                                                                                                                                                                          |
        | :------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
        | `addons`                        | **Description:** Defines how multiple keys can be combined under a parent key. The parent key doesn't have to already exist in Plex<br>**Values:** Dictionary List of [2 digit ISO 3166-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)                                                |
        | `append_addons`                 | **Description:** Appends to the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of [2 digit ISO 3166-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)                                                                                                      |
        | `append_include`                | **Description:** Appends to the [default include list](#default-values).<br>**Values:** List of [2 digit ISO 3166-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)                                                                                                                      |
        | `exclude`                       | **Description:** Exclude these Countries from creating a Dynamic Collection.<br>**Values:** List of [2 digit ISO 3166-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)                                                                                                                  |
        | `include`                       | **Description:** Overrides the [default include list](#default-values).<br>**Values:** List of [2 digit ISO 3166-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)                                                                                                                       |
        | `key_name_override`             | **Description:** Overrides the [default key_name_override dictionary](#default-values).<br>**Values:** Dictionary with `key: new_key_name` entries                                                                                                                                                            |
        | `limit_<<key>>`<sup>1</sup>     | **Description:** Changes the Builder Limit of the [key's](#collection_section) collection.<br>**Default:** `limit`<br>**Values:** Number Greater than 0                                                                                                                                                       |
        | `limit`                         | **Description:** Changes the Builder Limit for all collections in a Defaults File.<br>**Values:** Number Greater than 0                                                                                                                                                                                       |
        | `name_format`                   | **Description:** Changes the title format of the Dynamic Collections.<br>**Default:** `<<key_name>>`<br>**Values:** Any string with `<<key_name>>` in it.                                                                                                                                                     |
        | `remove_addons`                 | **Description:** Removes from the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of [2 digit ISO 3166-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)                                                                                                    |
        | `remove_include`                | **Description:** Removes from the [default include list](#default-values).<br>**Values:** List of [2 digit ISO 3166-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_3166_country_codes)                                                                                                                    |
        | `sort_by_<<key>>`<sup>1</sup>   | **Description:** Changes the Smart Filter Sort of the [key's](#collection_section) collection.<br>**Default:** `sort_by`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                                                                           |
        | `sort_by`                       | **Description:** Changes the Smart Filter Sort for all collections in a Defaults File.<br>**Default:** `release.desc`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                                                                              |
        | `style`                         | **Description:** Controls the visual theme of the collections created<table class="clearTable"><tr><th>Values:</th></tr><tr><td><code>white</code></td><td>White Theme</td></tr><tr><td><code>color</code></td><td>Color Theme</td></tr></table>                                                              |
        | `summary_format`                | **Description:** Changes the summary format of the Dynamic Collections.<br>**Default:** `<<library_translationU>>s filmed in <<key_name>>.`<br>**Values:** Any string.                                                                                                                                        |
        | `sync_mode_<<key>>`<sup>1</sup> | **Description:** Changes the Sync Mode of the [key's](#collection_section) collection.<br>**Default:** `sync_mode`<br>**Values:**<table class="clearTable"><tr><td>`sync`</td><td>Add and Remove Items based on Builders</td></tr><tr><td>`append`</td><td>Only Add Items based on Builders</td></tr></table> |
        | `sync_mode`                     | **Description:** Changes the Sync Mode for all collections in a Defaults File.<br>**Default:** `sync`<br>**Values:**<table class="clearTable"><tr><td>`sync`</td><td>Add and Remove Items based on Builders</td></tr><tr><td>`append`</td><td>Only Add Items based on Builders</td></tr></table>              |

        1. Each default collection has a `key` that when calling to effect a specific collection you must replace `<<key>>` with when calling.

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
          - default: region
            template_variables:
              use_other: false #(1)!
              use_separator: false #(2)!
              style: color #(3)!
              exclude:
                - fr #(4)!
              sort_by: title.asc
    ```

    1.  Do not create the "Other Regions" collection
    2.  Do not create a "Region Collections" separator
    3.  Set the [Color Style](#color-style)
    4.  Exclude "French" from the list of collections that are created

## Default Values

Unless you customize them as described above, these collections use default lists and searches to create the collections.

If you are interested in customizing the default values, you can find that information [here](#template-variables).

If you are interested in seeing what those default builders are, you can find that information [here](../sources.md).
