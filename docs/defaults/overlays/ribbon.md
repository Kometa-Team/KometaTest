---
hide:
  - toc
---
# Ribbon Overlays

The `ribbon` Default Overlay File is used to create a ribbon overlay based on the Top Lists of various sites on each 
item within your library.

![](images/ribbon.png)

## Requirements & Recommendations

Supported Overlay Level: Movie, Show

## Supported Ribbon

| Ribbon                          | Key               | Weight |
| :------------------------------ | :---------------- | :----- |
| BAFTA Winner                    | `bafta`           | `150`  |
| Berlinale Winner                | `berlinale`       | `130`  |
| Cannes Winner                   | `cannes`          | `140`  |
| César Winner                    | `cesar`           | `70`   |
| Common Sense Selection          | `common`          | `20`   |
| Critic's Choice Winner          | `choice`          | `90`   |
| Emmys Winner                    | `emmys`           | `100`  |
| Golden Globe Director           | `golden_director` | `160`  |
| Golden Globe Winner             | `golden`          | `170`  |
| IMDb Top 250                    | `imdb`            | `60`   |
| Independent Spirit Award Winner | `spirit`          | `80`   |
| Letterboxd Top 250              | `letterboxd`      | `50`   |
| Metacritic Must See             | `metacritic`      | `30`   |
| Oscars Best Director            | `oscars_director` | `180`  |
| Oscars Best Picture             | `oscars`          | `190`  |
| Razzies Winner                  | `razzie`          | `10`   |
| Rotten Tomatoes Certified Fresh | `rotten`          | `40`   |
| Rotten Tomatoes Verified Hot    | `rottenverified`  | `45`   |
| Sundance Winner                 | `sundance`        | `110`  |
| Venice Winner                   | `venice`          | `120`  |

## Config

The below YAML in your config.yml will create the overlays:

```yaml
libraries:
  Movies:
    overlay_files:
      - default: ribbon
  TV Shows:
    overlay_files:
      - default: ribbon
```

## Template Variables

Template Variables can be used to manipulate the file in various ways to slightly change how it works without having to 
make your own local copy.

Note that the `template_variables:` section only needs to be used if you do want to actually change how the defaults 
work. Any value not specified will use its default value if it has one if not it's just ignored.

??? abstract "Variable Lists (click to expand)"

    * **File-Specific Template Variables** are variables available specifically for this Kometa Defaults File.

    * **Overlay Template Variables** are additional variables shared across the Kometa Overlay Defaults.

    ??? example "Default Template Variable Values (click to expand)"

        | Variable            | Default  |
        |:--------------------|:---------|
        | `horizontal_offset` | `0`      |
        | `horizontal_align`  | `right`  |
        | `vertical_offset`   | `0`      |
        | `vertical_align`    | `bottom` |
        
    === "File-Specific Template Variables"

        | Variable                     | Description & Values                                                                                                    |
        | :--------------------------- | :---------------------------------------------------------------------------------------------------------------------- |
        | `style`                      | **Description:** Controls the color of the ribbon. <br>**Default:** `yellow` <br>**Values:** `yellow, gray, black, red` |
        | `use_all`                    | **Description:** Used to turn on/off all keys. <br>**Default:** `true` <br>**Values:** `true` or `false`                |
        | `weight_<<key>>`<sup>1</sup> | **Description:** Controls the weight of the Overlay. Higher numbers have priority.<br>**Values:** Any Number            |

        1. Each default overlay has a `key` that when calling to effect a specific overlay you must replace `<<key>>` 
        with when calling.

    === "Overlay Template Variables"

        {%
           include-markdown "../overlay_variables.md"
        %}
    
???+ example "Example Template Variable Amendments"

    The below is an example config.yml extract with some Template Variables added in to change how the file works.
    
    ```yaml
    libraries:
      Movies:
        overlay_files:
          - default: ribbon
            template_variables:
              style: black
              weight_metacritic: 35
              use_common: false
    ```
