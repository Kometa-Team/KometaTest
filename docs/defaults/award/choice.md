{%
    include-markdown "./award_1.md"
    replace='[["FULL_NAME", "Critics Choice"], ["CODE_NAME", "choice"], ["LIBRARY_TYPE", "Movie, Show"]]'
%}
| `Critics Choice Best Picture Winners` | `best` | Collection of Critics Choice Best Feature Award Winners |
{%
    include-markdown "./award_2.md"
    replace='[["FULL_NAME", "Critics Choice"], ["SHORT_NAME", "Critics Choice"]]'
%}
{%
    include-markdown "./award_3_movie.md"
    replace='["CODE_NAME", "choice"]'
%}
{%
    include-markdown "./award_3_show.md"
    replace='["CODE_NAME", "choice"]'
%}
{%
    include-markdown "./award_4.md"
    replace='[["SHORT_NAME", "Critics Choice"], ["CODE_NAME", "choice"]]'
%}