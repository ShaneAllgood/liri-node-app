# LIRI Bot

### Overview

This project is a command line interface application that takes in a type of search and items to look up and returns the results in both the console and log.txt file.

LIRI asks the user to enter their name in a prompt. LIRI then asks to make a selection from a list to determine the kind of search to perform. Finally, in another prompt, LIRI asks for the term to be search (e.g. the title of a song). The results are displayed in the console and also logged to the log.txt file.

### Before You Begin

1. LIRI will search Spotify for songs, Bands in Town for concerts, and OMDB for movies.

2. To retrieve the data that will power this app, you'll need to send requests using the `axios` package to the Bands in Town, Spotify      and OMDB APIs. You'll find these Node packages crucial for your assignment.

   * [Node-Spotify-API](https://www.npmjs.com/package/node-spotify-api)

   * [Axios](https://www.npmjs.com/package/axios)

   * [OMDB API](http://www.omdbapi.com)
   
   * [Bands In Town API](http://www.artists.bandsintown.com/bandsintown-api)

   * [Inquirer](https://www.npmjs.com/package/inquirer)

   * [Moment](https://www.npmjs.com/package/moment)

   * [DotEnv](https://www.npmjs.com/package/dotenv)
   
### Instructions

1. Navigate to the root of your project and run `npm init -y` &mdash; this will initialize a `package.json` file for your project. The      `package.json` file is required for installing third party npm packages and saving their version numbers. If you fail to initialize a    `package.json` file, it will be troublesome, and at times almost impossible for anyone else to run your code after cloning your           project.

2. Make a `.gitignore` file and add the following lines to it. This will tell git not to track these files, and thus they won't be          committed to Github.

    ```
    node_modules
    .DS_Store
    .env
    ```

3. Make a JavaScript file named `keys.js`.

  * Inside keys.js your file will look like this:

    ```js
    console.log('this is loaded');

    exports.spotify = {
      id: process.env.SPOTIFY_ID,
      secret: process.env.SPOTIFY_SECRET
    };
    ```

4. Next, create a file named `.env`, add the following to it, replacing the values with your API keys (no quotes) once you have them:

    ```js
    # Spotify API keys

    SPOTIFY_ID=your-spotify-id
    SPOTIFY_SECRET=your-spotify-secret

    ```

  * This file will be used by the `dotenv` package to set what are known as environment variables to the global `process.env` object in    node. These are values that are meant to be specific to the computer that node is running on, and since we are gitignoring this        file, they won't be pushed to github &mdash; keeping our API key information private.

  * If someone wanted to clone your app from github and run it themselves, they would need to supply their own `.env` file for it to       work.

5. Make a file called `random.txt`.

   * Inside of `random.txt` put the following in with no extra characters or white space:

   * spotify-this-song,"I Want it That Way"

6. Make a JavaScript file named `liri.js`.

7. At the top of the `liri.js` file, add code to read and set any environment variables with the dotenv package:

    ```js
    require("dotenv").config();
    ```

8. Add the code required to import the `keys.js` file and store it in a variable.

    ```js
      var keys = require("./keys.js");
    ```
  
* You should then be able to access your keys information like so

    ```js
    var spotify = new Spotify(keys.spotify);
    ```

9. Make it so liri.js can take in one of the following commands:

   * `concert-this`

   * `spotify-this-song`

   * `movie-this`

   * `do-what-it-says`

### What Each Command Should Do

1. `node liri.js concert-this <artist/band name here>`

   * This will search the Bands in Town Artist Events API (`"https://rest.bandsintown.com/artists/" + artist + "/events?app_id=codingbootcamp"`) for an artist and render the following information about each event to the terminal:

     * Name of the venue

     * Venue location

     * Date of the Event (use moment to format this as "MM/DD/YYYY")

        ![image](./assets/images/Sample_Concert_Search.JPG)

2. `node liri.js spotify-this-song '<song name here>'`

   * This will show the following information about the song in your terminal/bash window

     * Artist(s)

     * The song's name

     * A preview link of the song from Spotify


   * If no song is provided then your program will default to "The Sign" by Ace of Base.

        ![image](./assets/images/Sample_Song_Search.JPG)


   * You will utilize the [node-spotify-api](https://www.npmjs.com/package/node-spotify-api) package in order to retrieve song information from the Spotify API.

   * The Spotify API requires you sign up as a developer to generate the necessary credentials. You can follow these steps in order to generate a **client id** and **client secret**:

   * Step One: Visit <https://developer.spotify.com/my-applications/#!/>

   * Step Two: Either login to your existing Spotify account or create a new one (a free account is fine) and log in.

   * Step Three: Once logged in, navigate to <https://developer.spotify.com/my-applications/#!/applications/create> to register a new application to be used with the Spotify API. You can fill in whatever you'd like for these fields. When finished, click the "complete" button.

   * Step Four: On the next screen, scroll down to where you see your client id and client secret. Copy these values down somewhere, you'll need them to use the Spotify API and the [node-spotify-api package](https://www.npmjs.com/package/node-spotify-api).

3. `node liri.js movie-this '<movie name here>'`

   * This will output the following information to your terminal/bash window:

     ```
       * Title of the movie.
       * Year the movie came out.
       * IMDB Rating of the movie.
       * Rotten Tomatoes Rating of the movie.
       * Country where the movie was produced.
       * Language of the movie.
       * Plot of the movie.
       * Actors in the movie.
     ```

   * If the user doesn't type a movie in, the program will output data for the movie 'Mr. Nobody.'

   * You'll use the `axios` package to retrieve data from the OMDB API. Like all of the in-class activities, the OMDB API requires an API key. You may use `trilogy`.

      ![image](./assets/images/Sample_Movie_Search.JPG)

4. `node liri.js do-what-it-says`

   * Using the `fs` Node package, LIRI will take the text inside of random.txt and then use it to call one of LIRI's commands.

     * It should run `spotify-this-song` for "I Want it That Way," as follows the text in `random.txt`.

     * Edit the text in random.txt to test out the feature for movie-this and concert-this.

     ![image](./assets/images/Sample_Random_Search.JPG)

5. In addition to logging the data to your terminal/bash window, output the data to a .txt file called `log.txt`.

* Make sure you append each command you run to the `log.txt` file. 


[Video Demo](https://drive.google.com/file/d/1oOL2OoAM0BqHe-k-vx3HSSoGl4zSCf59/view)

Hello 