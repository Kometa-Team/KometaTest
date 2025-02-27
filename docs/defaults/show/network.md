---
hide:
  - toc
---
# Network Collections

The `network` Default Collection File is used to dynamically create collections based on the networks available in your library.

???+ danger "Important"

    This default requires that the library be set to use the "Plex TV Series" scanner and the "Plex Series" agent.

    The error in this case will be `Plex Error: plex_search attribute: network not supported`.

## Requirements & Recommendations

Supported Library Types: Show

## <a id="collection_section"></a>Collections Section 050

| Collection                          | Key                                 | Description                                                                    |
| :---------------------------------- | :---------------------------------- | :----------------------------------------------------------------------------- |
| `<<network>>`<br>**Example:** `NBC` | `<<network>>`<br>**Example:** `NBC` | Collection of Shows the aired on the network.                                  |
| `Network Collections`               | `separator`                         | [Separator Collection](../separators.md) to denote the Section of Collections. |


## Poster Styles

This Default can use the `style` Template Variable to easily change the posters styles.

### Color Style (Default)

![](../images/Network_color.png)

### White Style

![](../images/Network_white.png)

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  TV Shows:
    collection_files:
      - default: network
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

        | Variable                      | Description & Values                                                                                                                                                                                                                                             |
        | :---------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
        | `addons`                      | **Description:** Overrides the [default addons dictionary](#default-values). Defines how multiple keys can be combined under a parent key. The parent key doesn't have to already exist in Plex<br>**Values:** Dictionary List of Networks found in your library |
        | `append_addons`               | **Description:** Appends to the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of Networks found in your library                                                                                                                   |
        | `append_include`              | **Description:** Appends to the [default include list](#default-values).<br>**Values:** List of Networks found in your library                                                                                                                                   |
        | `exclude`                     | **Description:** Exclude these Networks from creating a Dynamic Collection.<br>**Values:** List of Networks found in your library                                                                                                                                |
        | `include`                     | **Description:** Overrides the [default include list](#default-values).<br>**Values:** List of Networks found in your library                                                                                                                                    |
        | `limit_<<key>>`<sup>1</sup>   | **Description:** Changes the Builder Limit of the [key's](#collection_section) collection.<br>**Default:** `limit`<br>**Values:** Number Greater than 0                                                                                                          |
        | `limit`                       | **Description:** Changes the Builder Limit for all collections in a Defaults File.<br>**Values:** Number Greater than 0                                                                                                                                          |
        | `name_format`                 | **Description:** Changes the title format of the Dynamic Collections.<br>**Default:** `<<key_name>>`<br>**Values:** Any string with `<<key_name>>` in it.                                                                                                        |
        | `remove_addons`               | **Description:** Removes from the [default addons dictionary](#default-values).<br>**Values:** Dictionary List of Networks found in your library                                                                                                                 |
        | `remove_include`              | **Description:** Removes from the [default include list](#default-values).<br>**Values:** List of Networks found in your library                                                                                                                                 |
        | `sort_by_<<key>>`<sup>1</sup> | **Description:** Changes the Smart Filter Sort of the [key's](#collection_section) collection.<br>**Default:** `sort_by`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                              |
        | `sort_by`                     | **Description:** Changes the Smart Filter Sort for all collections in a Defaults File.<br>**Default:** `release.desc`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options)                                                 |
        | `style`                       | **Description:** Choose between the default color version or the **white** one.<br>**Values:** `color` or `white`                                                                                                                                                |
        | `summary_format`              | **Description:** Changes the summary format of the Dynamic Collections.<br>**Default:** `<<library_translationU>>s broadcast on <<key_name>>.`<br>**Values:** Any string.                                                                                        |

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
          - default: network
            template_variables:
              style: white
              append_exclude:
                - BBC #(1)!
              sort_by: title.asc
              collection_mode: show_items #(2)!
              sep_style: gray #(3)!
    ```

    1.  exclude "BBC" from the list of items that should be included in the Collection list
    2.  Show these collections and their items within the "Library" tab
    3.  Use the gray [Separator Style](../separators.md#separator-styles)

## Default Values

Unless you customize them as described above, these collections use default lists and searches to create the collections.

If you are interested in customizing the default values, you can find that information [here](#template-variables).

If you are interested in seeing what those default builders are, you can find that information [here](../sources.md).
