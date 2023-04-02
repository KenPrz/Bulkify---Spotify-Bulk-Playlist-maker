# Automatic Spotify Playlist Generator
The Automatic Spotify Playlist Generator is a Python script that enables users to create a new playlist on their Spotify account by providing a list of track titles as input. The script uses the Spotify Web API to search for each track on Spotify and add them to the newly created playlist.

## Getting Started
To use the Automatic Spotify Playlist Generator, you will need to have a Spotify account and have created an app on the Spotify Developer Dashboard. You will also need to have Python 3 and the spotipy library installed on your computer.

+ Clone the repository or download the script file onto your computer.
+ Install the required dependencies by running `pip install -r requirements.txt` in your terminal or command prompt.
+ Open the script file in your preferred Python editor or IDE.
+ Replace the placeholders for the Spotify API credentials in the code with your own credentials.
+ Input your desired track titles into the titles list.
+ Run the script.

## Usage
The script takes a list of track titles as input and creates a new playlist on your Spotify account with those tracks.

```
import os
import sys
import spotipy
import spotipy.util as util

# Spotify API credentials
username = 'YOUR_SPOTIFY_USERNAME'
client_id = 'YOUR_CLIENT_ID'
client_secret = 'YOUR_CLIENT_SECRET'
redirect_uri = 'YOUR_REDIRECT_URI'

# Authentication scope
scope = 'playlist-modify-public'

# Get Spotify API token
token = util.prompt_for_user_token(username, scope, client_id, client_secret, redirect_uri)
if not token:
    print("Could not authenticate token")
    sys.exit()

# Create Spotify object
sp = spotipy.Spotify(auth=token)

# List of track titles
titles = ['Title 1', 'Title 2', 'Title 3']

# Create new playlist
playlist_name = 'My Playlist'
playlist = sp.user_playlist_create(username, playlist_name)

# Search for each track on Spotify and add to playlist
for title in titles:
    results = sp.search(q=title, type='track')
    items = results['tracks']['items']
    if len(items) > 0:
        track_uri = items[0]['uri']
        sp.user_playlist_add_tracks(username, playlist['id'], [track_uri])
        print(f"Added {title} to {playlist_name}")
    else:
        print(f"Could not find {title} on Spotify")
```
## Customization
You can customize the script to suit your needs by modifying the scope variable to change the permission level of the Spotify API token, and by modifying the search query to include more information such as the artist or album name to retrieve more accurate results.

## Troubleshooting
If you encounter any errors while running the script, make sure that your Spotify API credentials are correct and that your app has the appropriate permissions. You can also check the Spotify Developer Dashboard for any error messages related to your app.

## Contributing
Contributions to the Automatic Spotify Playlist Generator are welcome. To contribute, please fork the repository, make your changes, and submit a pull request.
