---
layout: post
title:      "Playlister Sinatra"
date:       2018-04-14 17:51:46 +0000
permalink:  playlister_sinatra
---


**Learning Objective**

1. Solidify your ActiveRecord understanding
2. Build out basic views for all your models
2. Create forms for editing and creating a new song that returns a well-structured params hash

**Setup**

1.	Create a migration
•	Run rake db:migration to create  a migration directory within the db directory
2.	Run rake db:create_migration NAME=( Songs, Artists, Genres, Song_Genres) to create the files for creating the tables for the database 
3.	Create the tables for Songs, Artists, Genres and Song_Genres

```
class CreateArtists < ActiveRecord::Migration
  def change
    create_table :artists do |t|
      t.string :name
    end
  end
end

class CreateSongs < ActiveRecord::Migration
  def change
    create_table :songs do |t|
      t.string :name
      t.integer :artist_id
    end
  end
end

class CreateGenres < ActiveRecord::Migration
  def change
    create_table :genres do |t|
      t.string :name
    end
  end
end

class CreateSongGenres < ActiveRecord::Migration
  def change
    create_table :song_genres do |t|
      t.integer :song_id
      t.integer :genre_id
    end
  end
end
```

4.	In the app/models folder you have the Artist, Song and Genre files that need to be setup with associations.
•	The associations are created by ActiveRecord migrations. An Artist has many Songs, and it has many Genres, through Songs. 

class Artist < ActiveRecord::Base
  has_many :songs
  has_many :genres, through: :songs

  include Slugifiable::Instance
  extend Slugifiable::Class
end

•	A Genre has many Songs, and it has many Artists, through Songs. All of the genres association comes from the song_genres table, which is a join table for songs and genres.

class Genre < ActiveRecord::Base
  has_many :song_genres
  has_many :songs, through: :song_genres
  has_many :artists, through: :songs

  include Slugifiable::Instance
  extend Slugifiable::Class
end
•	Because of the relationship between Artist/Song and Genre/Song, a Song belongs to an Artist and belongs to a Genre.

class Song < ActiveRecord::Base
  belongs_to :artist
  has_many :song_genres
  has_many :genres, through: :song_genres

  include Slugifiable::Instance
  extend Slugifiable::Class
end

•	The last association is for the song_genres since this is a joint table for songs and genres it will belong to both songs and genres.

class SongGenre < ActiveRecord::Base
  belongs_to :genre
  belongs_to :song
end

5.	Run rake db:migrate again this time to create the tables and columns for the table and their associations. If the table is created correctly you should see the table in the file schema.rb. This will pass the tests for all the models spec. 

6.	Setup the model and controllers.


