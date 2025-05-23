---
hide:
  - toc
---
# Producer Collections

The `producer` Default Collection File is used to dynamically create collections based on the most popular producers in 
your library.

## Requirements & Recommendations

Supported Library Types: Movie

## <a id="collection_section"></a>Collections Section 160

| Collection                                         | Key                                                | Description                                                                    |
| :------------------------------------------------- | :------------------------------------------------- | :----------------------------------------------------------------------------- |
| `<<producer_name>>`<br>**Example:** `Frank Welker` | `<<producer_name>>`<br>**Example:** `Frank Welker` | Collection of Movies by th Producer.                                           |
| `Producer Collections`                             | `separator`                                        | [Separator Collection](../separators.md) to denote the Section of Collections. |

{%
  include-markdown "../people.md"
%}

## Config

The below YAML in your config.yml will create the collections:

```yaml
libraries:
  Movies:
    collection_files:
      - default: producer
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

        | Variable                                 | Description & Values                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
        |:-----------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
        | `style` | **Description:** Controls the visual theme of the collections created.<br>**Default:** `bw`<br>**Values:** `bw`, `rainier`, `signature`, `diiivoy`, or `diiivoycolor` |
        | `data` | **Description:** Replaces the `data` dynamic collection value.<table class="clearTable"><tr><th>Attribute</th><th>Description & Values</th></tr><tr><td><code>depth</code></td><td>Controls the depth within the casting credits to search for common actors<br><strong>Default:</strong> 5<br><strong>Values:</strong> Number greater than 0</td></tr><tr><td><code>limit</code></td><td>Controls the maximum number of collections to create<br><strong>Default:</strong> 25<br><strong>Values:</strong> Number greater than 0</td></tr></table> |
        | `exclude` | **Description:** Exclude these Producers from creating a Dynamic Collection.<br>**Values:** List of Producer Names |
        | `include` | **Description:** Force these Actors to be included to create a Dynamic Collection.<br>**Values:** List of Actor Names |
        | `limit_<<key>>`<sup>1</sup> | **Description:** Changes the Builder Limit of the [key's](#collection_section) collection.<br>**Default:** `limit`<br>**Values:** Number Greater than 0 |
        | `limit` | **Description:** Changes the Builder Limit for all collections in a Defaults File.<br>**Values:** Number Greater than 0 |
        | `name_format` | **Description:** Changes the title format of the Dynamic Collections.<br>**Default:** `<<key_name>> (Producer)`<br>**Values:** Any string with `<<key_name>>` in it. |
        | `sort_by_<<key>>`<sup>1</sup> | **Description:** Changes the Smart Filter Sort of the [key's](#collection_section) collection.<br>**Default:** `sort_by`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options) |
        | `sort_by` | **Description:** Changes the Smart Filter Sort for all collections in a Defaults File.<br>**Default:** `release.desc`<br>**Values:** [Any `smart_filter` Sort Option](../../files/builders/plex.md#sort-options) |
        | `summary_format` | **Description:** Changes the summary format of the Dynamic Collections.<br>**Default:** `<<library_translationU>>s produced by <<key_name>>.`<br>**Values:** Any string with `<<key_name>>` in it. |
        | `tmdb_birthday` | **Description:** Controls if the Definition is run based on `tmdb_person`'s Birthday. Has 3 possible attributes `this_month`, `before` and `after`.<br>**Values:**<table class="clearTable"><tr><td>`this_month`</td><td>Run's if Birthday is in current Month</td><td>`true`/`false`</td></tr><tr><td>`before`</td><td>Run if X Number of Days before the Birthday</td><td>Number 0 or greater</td></tr><tr><td>`after`</td><td>Run if X Number of Days after the Birthday</td><td>Number 0 or greater</td></tr></table> |
        | `tmdb_person_offset_<<key>>`<sup>1</sup> | **Description:** Changes the summary tmdb_person_offset for the specific key.<br>**Default:** `0`<br>**Values:** Dictionary of Actor Name as the keys and the tmdb_person_offset as the value. |

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
          - default: producer
            template_variables:
              data:
                depth: 15 #(1)!
                limit: 5 #(2)!
              style: signature #(3)!
              sort_by: title.asc
              use_separator: false #(4)!
              tmdb_person_offset_Richard Brooks: 1 #(5)!
    ```

    1.  Check the first 15 casting credits in each movie
    2.  Create 5 collections maximum
    3.  use the [rainier Style](#poster-styles)
    4.  Do not create a "Producers Collections" separator
    5.  There are two Richard Brooks, so use the 2nd 
    [Richard Brooks](https://www.themoviedb.org/search?query=Richard%20Brooks) found on TMDb
