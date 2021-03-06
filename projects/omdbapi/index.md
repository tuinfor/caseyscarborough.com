---
layout: project
title: Projects &middot; OMDBAPI Gem
---

# omdbapi

<i class="icon-cloud-download"></i> <a href="https://github.com/caseyscarborough/omdbapi/zipball/master">Download .zip</a> &nbsp; 
<i class="icon-cloud-download"></i> <a href="https://github.com/caseyscarborough/omdbapi/tarball/master">Download .tar.gz</a> &nbsp; 
<i class="icon-github"></i> <a href="https://github.com/caseyscarborough/omdbapi">View on GitHub</a>

[![Gem Version](https://badge.fury.io/rb/omdbapi.png)](http://badge.fury.io/rb/omdbapi)

This gem is a simple and easy to use wrapper for the [omdbapi.com](http://omdbapi.com/) API. This API allows you to pull almost any type of information about a show or movie, and uses information from IMDb. 

## Documentation

The complete documentation for the gem can be viewed at [rdoc.info/gems/omdbapi/frames](http://rdoc.info/gems/omdbapi/frames).

## Installation

### Requirements

* Ruby v1.9.3 or later

### Installing

You can install the gem by adding it your application's Gemfile:

```ruby
gem 'omdbapi'
```

And then execute:

```bash
$ bundle
```

Or you can install it manually by issuing the following command:

```bash
$ gem install omdbapi
```

## Usage

```ruby
require 'omdbapi'
```
### Title

You can get a movie or TV show's information in a Hash by using the title method, shown below:

<pre class="highlight"><code class="ruby">game_of_thrones = OMDB.title('Game of Thrones')
# => {:title=>"Game of Thrones", :year=>"2011", :rated=>"TV-MA", :released=>"17 Apr 2011", :runtime=>"1 h", :genre=>"Adventure, Drama, Fantasy", :director=>"N/A", :writer=>"David Benioff, D.B. Weiss", :actors=>"Peter Dinklage, Lena Headey, Maisie Williams, Emilia Clarke", :plot=>"Seven noble families fight for control of the mythical land of Westeros.", :poster=>"http://ia.media-imdb.com/images/M/MV5BNTY2MzAxNzM0Ml5BMl5BanBnXkFtZTcwNDA0MDkxOQ@@._V1_SX300.jpg", :imdb_rating=>"9.4", :imdb_votes=>"382,638", :imdb_id=>"tt0944947", :type=>"series", :response=>"True"} 
game_of_thrones.title # => "Game of Thrones"
game_of_thrones.year  # => "2011"
game_of_thrones.rated # => "TV-MA"
# etc...
</code></pre>

This function will return a Hash with the following information about the title:

<pre class="highlight"><code class="ruby">:title, :year, :rated, :released, :runtime, :genre, :director, :writer, 
:actors, :plot, :poster, :imdb_rating, :imdb_votes, :imdb_id, :type
</code></pre>

You can also pass in the optional parameters for year or plot. Plot defaults to 'short', so the only other option is 'full'.

<pre class="highlight"><code class="ruby">OMDB.title('True Grit')
# => {:title=>"True Grit", :year=>"2010", :rated=>"PG-13"...
OMDB.title('True Grit', year: '1969')
# => {:title=>"True Grit", :year=>"1969", :rated=>"G"...

# Get the title with the full plot
OMDB.title('Breaking Bad', plot: 'full')

# Get the original Italian Job with the full plot
OMDB.title('The Italian Job', year: '1969', plot: 'full')
</code></pre>

### IMDb ID

You can find a title by it's IMDb ID using the id method:

<pre class="highlight"><code class="ruby">lost = OMDB.id('tt0411008')
# => {:title=>"Lost", :year=>"2004", :rated=>"TV-14", :released=>"22 Sep 2004", :runtime=>"42 min", :genre=>"Adventure, Drama, Fantasy, Mystery, Sci-Fi, Thriller", :director=>"N/A", :writer=>"J.J. Abrams, Jeffrey Lieber", :actors=>"Matthew Fox, Jorge Garcia, Evangeline Lilly, Naveen Andrews", :plot=>"The survivors of a plane crash are forced to live with each other on a remote island, a dangerous new world that poses unique threats of its own.", :poster=>"http://ia.media-imdb.com/images/M/MV5BMjA3NzMyMzU1MV5BMl5BanBnXkFtZTcwNjc1ODUwMg@@._V1_SX300.jpg", :imdb_rating=>"8.3", :imdb_votes=>"160,182", :imdb_id=>"tt0411008", :type=>"series", :response=>"True"} 
lost.released    # => "22 Sep 2004"
lost.imdb_rating # => "8.3"
# etc...
</code></pre>

### Search

You can find a title by using the search method:

<pre class="highlight"><code class="ruby">results = OMDB.search('Star Wars')
# => [{:title=>"Star Wars", :year=>"1977", :imdb_id=>"tt0076759", :type=>"movie"}, {:title=>"Star Wars: Episode V - The Empire Strikes Back", :year=>"1980", :imdb_id=>"tt0080684", :type=>"movie"}, {:title=>"Star Wars: Episode VI - Return of the Jedi", :year=>"1983", :imdb_id=>"tt0086190", :type=>"movie"}, {:title=>"Star Wars: Episode I - The Phantom Menace", :year=>"1999", :imdb_id=>"tt0120915", :type=>"movie"}, {:title=>"Star Wars: Episode III - Revenge of the Sith", :year=>"2005", :imdb_id=>"tt0121766", :type=>"movie"}, {:title=>"Star Wars: Episode II - Attack of the Clones", :year=>"2002", :imdb_id=>"tt0121765", :type=>"movie"}, {:title=>"Star Wars: The Clone Wars", :year=>"2008", :imdb_id=>"tt1185834", :type=>"movie"}, {:title=>"Star Wars: Clone Wars", :year=>"2003", :imdb_id=>"tt0361243", :type=>"series"}, {:title=>"Star Wars: The Clone Wars", :year=>"2008", :imdb_id=>"tt0458290", :type=>"series"}, {:title=>"The Star Wars Holiday Special", :year=>"1978", :imdb_id=>"tt0193524", :type=>"movie"}]
results.each { |r| puts r.title }
# etc...
</code></pre>

This method returns an Array of search results. Each search result is a Hash with the following information about the result:

<pre class="highlight"><code class="ruby">:title, :year, :imdb_id, :type</code></pre>

If there is only a single search result, the title will be returned as a Hash with the full information, instead of the Array of shortened search results.


This method will return a Hash of the title's properties, exactly as the title method.

## Running the Tests

The test suite is written using RSpec, and can be run by issuing the following command from the root of the repository:

<pre class="no-highlight"><code><span class="dollar">$</span> rspec spec</code></pre>

## Contributing

Please feel free to contribute to the project by following the options below.

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request