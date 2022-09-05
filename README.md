# New Albums

A python script to update a Spotify playlist every day with all the songs from any significant new albums. It shouldn't include single-only releases. Anything older than a month should be deleted.

## Installation

Before you can run the New Albums script, there are some pre-requisites the script assumes.

### Spotify Developer Account

The script will need a Spotify **Client Id** and **Client Secret** to interact with Spotify's Web API.

Register for a [developer account](https://developer.spotify.com) on Spotify. After registering, create a new app. Once you create a new app, a Client Id and Client Secret will be generated. You will need these in later steps.

Additionally, the New Albums script uses an Authorization Code Flow. Due to this, you will need to set a redirect URL for your app. To add a redirect URL, open the app's settings. Note: The New Albums script is only intended to run locally, on your machine, so add a redirect link to `http://localhost:8080`.

### Spotify Playlist Id

The script will need the unique ID for one of your playlists. To get the ID for a playlist, in Spotify, right-click on the playlist > Share > Copy Share Link. The link will contain the playlist ID. It is the string between `playlist/` and `?si=`.

### Environment Variables

You can specify custom environment variables to include using a `.env` file.  Alternatively, you can set them manually using the information below.

#### Windows

FIRST SET UP ENVIRONMENT VARIABLES ON YOUR COMPUTER, [SEE HERE FOR INSTRUCTIONS](https://superuser.com/questions/949560/how-do-i-set-system-environment-variables-in-windows-10).

To set all 4 in a one-liner on Windows:

```cmd
set SPOTIFY_CLIENT_ID=xxx && set SPOTIFY_CLIENT_SECRET=xxx && set SPOTIFY_REDIRECT_URI=http://localhost:8080 && set NEW_ALBUMS_PLAYLIST_ID=xxx && set SPOTIFY_USER=xxx
```

To view all currently set environment variables, use the command `set`.

#### MacOS/Linux

To set all 4 in a one-liner on Linux: ([Instructions](https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-set-environment-variables-in-linux/))

```cmd
 export SPOTIFY_CLIENT_ID=xxx && export SPOTIFY_CLIENT_SECRET=xxx && export SPOTIFY_REDIRECT_URI='http://localhost:8080' && export NEW_ALBUMS_PLAYLIST_ID=xxx && export SPOTIFY_USER=xxx
```

Note that there is a space before the first export.  This is intentional and should not be removed: a leading space in most terminals instructs the terminal not to lodge the command in the history file, leaving fewer traces of your environment keys in side effecting channels.

To view all currently set environment variables, use the command `env`. You can filter down to just the above using `env | egrep '(SPOTIFY|PLAYLIST)'`

### Set which genres to Reject
By default, the genres specified in `new_albums._default_fiat` is used to filter genres.  You can add a custom fiat file in the `new_albums` folder and specify the name in your .env file usimg the `FIAT_FILE` variable.   

The script will reject any album on which the primary artist's first genre matches any of the genres in your reject list. For example, if you have `"dance pop"` in your reject list, then the script will reject Beyoncé's 'RENAISSANCE' album, because her first genre is dance pop. (Her genres are ['dance pop', 'pop', 'r&b']).

### Create a Virtual Environment (optional)

These steps is not necessary, but recommended for environment isolation. You could use [virtualenv](https://virtualenv.pypa.io/en/latest/installation.html) (and [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io/en/latest/index.html)) or just the built-in [venv](https://docs.python.org/3/library/venv.html).

### Install dependencies

Installing the package adds the dependencies specified in the setup.py file

```
pip install .
```

### Local development

The package can be installed in develop mode to allow you to make changes locally.

`pip install . develop`  

## Running

Once you have completed all the installation steps, run New Albums script by running `py -m new_albums`.

### Filter by country

By default, the script will filter by US. To filter by a specific country, you can pass the `--country` flag followed by the country ISO code, e.g. `py -m new_albums --country JP`

**Options**:
- `py -m new_albums`: filters by US
- `py -m new_albums --country GB`: filter by GB
- `py -m new_albums --country list`: list all available Spotify country codes. The script then prompts you to type an ISO code.
- `py -m new_albums --country all`: include -m new_albums codes (worldwide)

`-c` can also be used as an abbreviation for `--country`, e.g. `py -m new_albums -c all`

### Filter by top genres

By default, the script will not filter by top genres. To enable this filter, you can pass the `--top-genres` flag, e.g. `py -m new_albums --top-genres`

`-g` can also be used as an abbreviation for `--top-genres`, e.g. `py -m new_albums -g`
