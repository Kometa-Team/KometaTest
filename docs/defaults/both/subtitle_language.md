---
hide:
  - toc
---
# Subtitle Language Collections

The `subtitle_language` Default Collection File is used to dynamically create collections based on the subtitle 
languages available in your library.

![](../images/subtitle_language.png)

## Requirements & Recommendations

Supported Library Types: Movie, Show

## <a id="collection_section"></a>Collections Section 095

| Collection                                               | Key                                                                                      | Description                                                                    |
| :------------------------------------------------------- | :--------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------- |
| `<<Subtitle Language>> Audio`<br>**Example:** `Japanese` | `<<ISO 639-1 Code>>`<br>**Example:** `ja` <br>`<<ISO 639-2 Code>>`<br>**Example:** `myn` | Collection of Movies/Shows that have this Subtitle Language.                   |
| `Other Subtitles`                                        | `other`                                                                                  | Collection of Movies/Shows that are less common Languages.                     |
| `Subtitle Language Collections`                          | `separator`                                                                              | [Separator Collection](../separators.md) to denote the Section of Collections. |

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  Movies:
    collection_files:
      - default: subtitle_language
  TV Shows:
    collection_files:
      - default: subtitle_language
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

        | Variable                      | Description & Values                                                                                                                                                                                                                                                               |
        | :---------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | `append_include`              | **Description:** Appends to the [default include list](#default-values)<br>**Values:** List of [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)<br>**Values:** List of [ISO 639-2 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-2_codes)            |
        | `exclude`                     | **Description:** Exclude these Audio Languages from creating a Dynamic Collection.<br>**Values:** List of [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)<br>**Values:** List of [ISO 639-2 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-2_codes) |
        | `include`                     | **Description:** Overrides the [default include list](#default-values)<br>**Values:** List of [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)<br>**Values:** List of [ISO 639-2 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-2_codes)             |
        | `key_name_override`           | **Description:** Overrides the [default key_name_override dictionary](#default-values).<br>**Values:** Dictionary with `key: new_key_name` entries                                                                                                                                 |
        | `limit_<<key>>`<sup>1</sup>   | **Description:** Changes the Builder Limit of the [key's](#collection_section) collection.<br>**Default:** `limit`<br>**Values:** Number Greater than 0                                                                                                                            |
        | `limit`                       | **Description:** Changes the Builder Limit for all collections in a Defaults File.<br>**Values:** Number Greater than 0                                                                                                                                                            |
        | `name_format`                 | **Description:** Changes the title format of the Dynamic Collections.<br>**Default:** `<<key_name>> Subtitles`<br>**Values:** Any string with `<<key_name>>` in it.                                                                                                                |
        | `remove_include`              | **Description:** Removes from the [default include list](#default-values)<br>**Values:** List of [ISO 639-1 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)<br>**Values:** List of [ISO 639-2 codes](https://en.wikipedia.org/wiki/List_of_ISO_639-2_codes)          |
        | `sort_by_<<key>>`<sup>1</sup> | **Description:** Changes the Smart Filter Sort of the [key's](#collection_section) collection.<br>**Default:** `sort_by`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                                                |
        | `sort_by`                     | **Description:** Changes the Smart Filter Sort for all collections in a Defaults File.<br>**Default:** `release.desc`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                                                   |
        | `summary_format`              | **Description:** Changes the summary format of the Dynamic Collections.<br>**Default:** `<<library_translationU>>s with <<key_name>> Subtitles.`<br>**Values:** Any string.                                                                                                        |

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
          - default: subtitle_language
            template_variables:
              use_other: false #(1)!
              use_separator: false #(2)!
              exclude:
                - fr  #(3)!
              sort_by: title.asc
    ```

    1.  Do not create an "Other Audio" collection
    2.  Do not create an "Audio Language Collections" separator
    3.  Exclude "French" from having an Audio Collection

## Default Values

Unless you customize them as described above, these collections use default lists and searches to create the collections.

If you are interested in customizing the default values, you can find that information [here](#template-variables).

If you are interested in seeing what those default builders are, you can find that information [here](../sources.md).
