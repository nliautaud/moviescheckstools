# moviescheckstools

Import/export movie lists between movies database services without API or simple binding.

| service | import | export | API | tooled import | tooled export |
|---------|:------:|:------:|:---:|:-------------:|:-------------:|
| [IMDb](http://imdb.com)  | no | IMDb CSV | partial | ? | (not needed) |
| [trakt.tv](http://trakt.tv) | no | no | yes | [TraktRater][traktrater] | [trakt.tv backup][ttvbackup] |
| [SensCritique](http://senscritique.com) | no | no | no | [imdb2senscritique][imdb2sc] | ? |
| [ICheckMovies](http://icheckmovies.com) | [IMDb CSV][icmexp] | paid | no | (not needed) | (see below) |
| [criticker](http://criticker.com) | [IMDb CSV](crtexp) | no | no | (not needed) | ? |
| [Letterboxed](http://letterboxed.com) | paid | yes | no | ? | (not needed) |

[imdbify]: https://github.com/nliautaud/imdbify
[imdb2sc]: https://github.com/mukurokudo/imdb2senscritique
[ttvbackup]: https://darekkay.com/blog/trakt-tv-backup/
[traktrater]: https://github.com/damienhaynes/TraktRater

[icmexp]: http://www.icheckmovies.com/import/imdbvotes
[crtexp]: http://www.criticker.com/?im


[imdbify][imdbify] convert a movie list to an IMDb CSV file, thus may be used between the site/tool export and site/tool import, to fill the gap between the majority of them.

Examples :

- **To export from IMDb to SensCritique**, export a CSV file by using "*Export this List*" on IMDb, then import the data in SensCritique with [imdb2senscritique][imdb2sc].
- **To export from trakt.tv to SensCritique**, export trakt.tv data with [trakt.tv backup][ttvbackup], convert a file (ex. ``ratings_movies.txt``) to IMDb CSV format with [imdbify][imdbify], then import the data in SensCritique with [imdb2senscritique][imdb2sc].
- **To export from ICheckMovies to trakt.tv, criticker or SensCritique**, export ICheckMovies data (see below), convert to IMDb CSV format with [imdbify][imdbify], then import to trakt.tv with [TraktRater][traktrater] or to criticker (www.criticker.com/?im) or SensCritique with [imdb2senscritique][imdb2sc].

## other tools

- [compare](https://rawgit.com/nliautaud/moviescheckstools/master/compare.html) : Drop several export files from IMDb, trakt.tv backup, or any file containing IMDb ID's surrounded by double quotes to compare their IMDb IDs. 

## icheckmovies scrapping export

Create a CSV export of the checked movies in icheckmovies, as a list of IMDB urls.

1. Install the [Web Scraper Extension](webscraper.io) for chrome
1. Import the following sitemap (replace ``44`` by the number of pages in icheckmovies), scrape (it may take more than a minute) & export the resulting CSV file  
``{"startUrl":"https://www.icheckmovies.com/movies/checked/?page=[1-44]","selectors":[{"parentSelectors":["_root"],"type":"SelectorElementAttribute","multiple":true,"id":"imdb_link","selector":"a.optionIMDB","extractAttribute":"href","delay":""}],"_id":"icheckmovies_checked_imdbids"}``
3. delete the url prefixes in the file with a text editor to keep only the IMDb ID surrounded by double quotes
4. drop the file onto [compare](#imdbify) and save the result
5. give the resulting data to [TraktRater][traktrater].

Done !
