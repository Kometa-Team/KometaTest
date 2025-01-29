{%
    include-markdown "./award_1.md"
    replace='[["FULL_NAME", "People\\'s Choice"], ["CODE_NAME", "pca"], ["LIBRARY_TYPE", "Movie, Show"]]'
%}
| `People's Choice Award Winners` | `pca` | Collection of People's Choice Award Winners. |
{%
    include-markdown "./award_2.md"
    replace='[["FULL_NAME", "People\\'s Choice"], ["SHORT_NAME", "People\\'s Choice"]]'
%}
{%
    include-markdown "./award_3_movie.md"
    replace='["CODE_NAME", "pca"]'
%}
{%
    include-markdown "./award_3_show.md"
    replace='["CODE_NAME", "pca"]'
%}
{%
    include-markdown "./award_4.md"
    replace='[["SHORT_NAME", "People\\'s Choice"], ["CODE_NAME", "pca"]]'
%}