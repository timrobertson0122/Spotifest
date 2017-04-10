Planning

- Find Songkick event page for chosen festival e.g. https://www.songkick.com/festivals/57-reading/id/28673189-reading-festival-2017#lineup
- Parse artist links in 'Line-up' section into an array of artist names
- Use Spotify API to create new empty playlist e.g.
      curl -X POST "https://api.spotify.com/v1/users/timrobertson0122/playlists" -H "Authorization: Bearer {your access token}" -H "Content-Type: application/json" --data "{\"name\":\"{Festival Name}\", \"public\":false}"
- For each artist in array search Spotify by artist name to get back Spotify Artist ID e.g.
      curl -X GET "https://api.spotify.com/v1/search?q=foo+fighters&type=artist"
  This returns a JSON object with an ID field e.g.
      "id" : "7jy3rLJdDQY21OgRLCZ9sD"
- Query Spotify using the ID and return, for example, the top tracks for that artist e.g.
      curl -X GET "https://api.spotify.com/v1/artists/7jy3rLJdDQY21OgRLCZ9sD/top-tracks?country=US"
- Extract each track URI from the resulting JSON object e.g.
        "name" : "Everlong",
        "popularity" : 74,
        "preview_url" : "https://p.scdn.co/mp3-preview/4a2dc307a71393a695d69b16407cd73e1e234941?cid=8897482848704f2a8f8d7c79726a70d4",
        "track_number" : 11,
        "type" : "track",
        "uri" : "spotify:track:5UWwZ5lm5PKu6eKsHAGxOk"
        }
- Pass all URI's in a POST request to the playlist endpoint http://api.spotify.com/v1/users/{user_id}/playlists/{playlist_id}/tracks

e.g.
      curl -X POST "https://api.spotify.com/v1/users/timrobertson0122/playlists/3cEYpjA9oz9GiPac4AsH4n/tracks?position=0&uris=spotify%3Atrack%3A5UWwZ5lm5PKu6eKsHAGxOk,{next track uri}"
- Repeat for each artist in original array
