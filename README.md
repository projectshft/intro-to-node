# Intro to Node

## Introduction
The following is based on an in-person event, but has also been written in such a way that anyone could pick it up and code along! In this short lesson, we'll be build a simple API based on the "official" (unofficial) Star Wars API called [SWAPI](https://swapi.co/)! In the past we built a front-end application that uses this API and you can find that lesson [here](https://github.com/projectshft/swapi).

## Prerequisites
We're going to assume that you're a bit familiar JavaScript and how the internet works. If not, you may be a little lost, but we challenge you to give it a shot either way. At the very least, this code-along should give you an idea of things to learn next!

## Setup
For simplicity sake, we're going to be using [repl.it](repl.it). Navigate to [this link](https://repl.it/@AaronHayslip/Star-Wars-API) to get started. The first thing you'll want to do is click "fork" at the top, middle of the page:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-3.50.29-PM.png)

This will allow you to have your own copy of our project. Okay, before we move on, we have a ton to talk about.

## What is Node and Why is it Useful?
Wikipedia says, "Node.js is an open-source, cross-platform JavaScript run-time environment that executes JavaScript code outside of a browser."

What does that mean?

JavaScript is almost always thought of as being run in the browser, but with Node, we can execute JavaScript outside of the browser. Why is this awesome? Well, it allows us to run Node in new environments to do awesome things like, create web servers.

And what exactly does that mean?

With Node, we don't have to learn Java, Ruby, Python, etc to write code for the "back end" - we can use JavaScript to do that too, just like we do with the front-end! We're not only _able_ to use JavaScript on the back-end with Node, but thanks to Node, writing JavaScript on the back-end is super fast and performant. Node enables JavaScript to be a first-class server-side langauge.

## Running JavaScript
Like we said, the usual place to run JavaScript is in the browser. Assuming you have Google Chrome installed, open in it up and navigate to `view` --> `Developer` --> `JavaScript Console`. It will open a window that looks something like this:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-7.54.08-PM.png)

And now we can write JavaScript!

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-8.01.15-PM.png)

But this isn't Node. Inside the Chrome browser, there's a JavaScript enginge called the [V8 JavaScript Engine](https://v8.dev/). But, thanks to Node, you can now get this engine locally on your machine by downloading node.

## Downloading Node
For the sake of this lesson, we're going to be using repl.it, but in case you were wondering about how to up and running with Node, it's pretty simple. Just download it from [nodejs.org](https://nodejs.org/en/), install it and open your command-line, then type in `node`, like this:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-8.05.28-PM.png)

Now, just like with the Chrome Developer Console, we can type in JavaScript and have it executed right from our machine:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-8.06.43-PM.png)

But let's get on with building out our API.

## What is an API?
First, let's talk about what an API even is.

**API** stands for **A**pplication **P**rogramming **I**nterface. Though the way we usually use the term is in the context we're using it now (which is to refer to a public API that will give us back data) it can also be used to reference the way that we might interact with any programming interface, such as jQuery.

But as we just said, at the moment when we refer to the "API" we'll be building, we're thinking about creating a mechanism that would allow anyone to get access to our Star Wars data via HTTP requests. Sheesh, another vocab word that we have to define.

## What is HTTP?
HTTP stands for **H**ypertext **T**ransfer **P**rotocol. It is essentially the way different computers can communicate with one another across the internet. Just as our home have address that we can identify with some unique identfiers, server (special computers that communicate on the web) have IP (internet protocol) addresses that we can unique identify and communicate with as well.

We call the dispatching of data that we do with **HTTP**, "requests". For example, when you type "google.com" into your browser, you're making a _request_ to google to get their website sent to you. Specifically (and briefly), these are the steps that happen in the background:

1. You type "google.com" in and hit "enter"
2. DNS (Domain Name System), translates "google.com" into it's formal "IP address" (will look something like: `64.68.90.1`)
3. Your browser then finds the google server somewhere and asks for all that it needs to display "google.com"
4. Google then responds with some HTML, CSS and JavaScript files
5. Your browser reads those files and parses together what looks like Google.com, until you're ready to do something else (like a search) and kick off another request to Google's servers for more data.

There are 4 main types of **HTTP** requests:

**GET**: You can make this request when you want to ask for more data. For example, let's say you want to get all the data from the Star Wars API on Luke Skywalker. You can make a request for that.
**POST**: This is for creating and save new data. For example, every time you Tweet or Instagram, you're making a request to either Twitter or Instagram's servers to save your new Tweet or Instagram.
**PUT**: This is for updating existing data. For example, let's say that you post something controversial on Facebook (which everyone does?) and then you want to change it. A POST request would be use to make this edit.
**DELETE**: For the really bad Facebook post that your regret. Self explanatory.

## HTTP and Public Facing API's
Most web applications these days are set up in a such way that the data for the application can be accessed over the internet through HTTP. For example, Twitter, Facebook, Instagram and just about everything else you can think of have public facing API's that allow the average Joe developer to build applications using their data, accessible through their API's.

For example, let's look at the Google Books API. Copy and paste the following URL into your browser:

`https://www.googleapis.com/books/v1/volumes?q=javascript`

You should see something like this:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-8.26.29-PM.png)

What just happened? Let's walk through it step-by-step:

1. When you typed that URL into the browser, your browser made a request to the Google Books API
2. The Google Books API responded with data that was specific to your request. Reading the documentation on the [Google Books API](https://developers.google.com/books/docs/v1/using) would tell you that you can search for books by passing in an optional "query string". Without going into it too much, we added `q=javascript` (`q` is for query) which told the Google Books server to search it's database for books with "JavaScript" in the title.
3. The Google Books API fufilled our request and responded with some JSON data.

## What is JSON?
Well, I'm glad you asked. JSON stands for "JavaScript Object Notation". We could spend a ton of time on it, but it's essentially the most widely adopted way to format data on the web. Most of the API's you would use would return it's data in this format. Additionally, most programming languages have functions that allow them to convert data in JSON - so whether your Web Server is built with Ruby, Python, JavaScript or whatever, it will be able to return JSON when used to build out an API.

## What does JSON look like?
JSON looks like JavaScript Arrays and Objects, because they are. You should be able to translate any data you can think of into this format. For example, a basic grocery list might look like this:

```js
{
  "items": ["beer", "cheese", "milk", "bread"]
}
```

The above is an object with one property, `items`, which is an array of strings to describe our list. We could add more data to the JSON above to make it more useful:

```js
{
  "items": [
    {"name": "beer", "price": 11},
    {"name": "cheese", "price": 8},
    {"name": "milk", "price": 5},
    {"name": "bread", "price": 4}
  ],
  "grocery_store": "Harris Teeter",
  "shopping_date": "2018-11-29T18:12:09+00:00"
}
```

Now we know how much our items cost, the location of the shopping trip and the time of the shopping trip.

## Building our API
Now we're ready to get started! Go to this link: [https://repl.it/@AaronHayslip/Star-Wars-API](https://repl.it/@AaronHayslip/Star-Wars-API). In a moment we'll start building our API, but let's first tour our workspace.

For simplicity sake, we're using [repl.it](repl.it), but normally we'd write this code on files local to our computer and not with "repl.it".

On "repl.it", you'll see 4 different "windows". We'll give them numbers below to make them easy to reference.

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Asset-1@200x-1.png)

1. This panel shows us all the files in this project. We can select which files we want to work on from here.
2. This panel is where we'll actually write our code
3. This panel represents our actual browser. We'll make our requests using this window in the URL bar.
4. This panel represents our terminal. We won't have to do much from here thanks to Repl.it, but this is our "console" and where our code will log.

As you can see, we're doing a console log inside of `index.js`. We can actually run this file if we press the big green "start" button at the top. You will see the code log inside the terminal (panel 4).

## JSON for our API
Our API is going to be brief and simple. We'll build a few different URLs to enable developers to get Star Wars data for their applications. Only our will be give them data on some of the "people" in Star Wars - just 10 of the people in fact.

Since we don't have a database, we'll just store all the data that we have inside of a JSON file and send different parts of that data back as requests are made to our API. In Panel 1, create a new file called `people.js` and add the following to it:

```js
  {
"results": [
    {
      "id": 1,
      "name": "Luke Skywalker",
      "height": "172",
      "mass": "77",
      "hair_color": "blond",
      "skin_color": "fair",
      "eye_color": "blue",
      "birth_year": "19BBY",
      "gender": "male",
      "homeworld": "https://swapi.co/api/planets/1/",
      "films": [
          "https://swapi.co/api/films/2/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/3/",
          "https://swapi.co/api/films/1/",
          "https://swapi.co/api/films/7/"
      ],
      "species": [
          "https://swapi.co/api/species/1/"
      ],
      "vehicles": [
          "https://swapi.co/api/vehicles/14/",
          "https://swapi.co/api/vehicles/30/"
      ],
      "starships": [
          "https://swapi.co/api/starships/12/",
          "https://swapi.co/api/starships/22/"
      ],
      "created": "2014-12-09T13:50:51.644000Z",
      "edited": "2014-12-20T21:17:56.891000Z",
      "url": "https://swapi.co/api/people/1/"
    },
    {
      "id": 2,
      "name": "C-3PO",
      "height": "167",
      "mass": "75",
      "hair_color": "n/a",
      "skin_color": "gold",
      "eye_color": "yellow",
      "birth_year": "112BBY",
      "gender": "n/a",
      "homeworld": "https://swapi.co/api/planets/1/",
      "films": [
          "https://swapi.co/api/films/2/",
          "https://swapi.co/api/films/5/",
          "https://swapi.co/api/films/4/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/3/",
          "https://swapi.co/api/films/1/"
      ],
      "species": [
          "https://swapi.co/api/species/2/"
      ],
      "vehicles": [],
      "starships": [],
      "created": "2014-12-10T15:10:51.357000Z",
      "edited": "2014-12-20T21:17:50.309000Z",
      "url": "https://swapi.co/api/people/2/"
    },
    {
      "id": 3,
      "name": "R2-D2",
      "height": "96",
      "mass": "32",
      "hair_color": "n/a",
      "skin_color": "white, blue",
      "eye_color": "red",
      "birth_year": "33BBY",
      "gender": "n/a",
      "homeworld": "https://swapi.co/api/planets/8/",
      "films": [
          "https://swapi.co/api/films/2/",
          "https://swapi.co/api/films/5/",
          "https://swapi.co/api/films/4/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/3/",
          "https://swapi.co/api/films/1/",
          "https://swapi.co/api/films/7/"
      ],
      "species": [
          "https://swapi.co/api/species/2/"
      ],
      "vehicles": [],
      "starships": [],
      "created": "2014-12-10T15:11:50.376000Z",
      "edited": "2014-12-20T21:17:50.311000Z",
      "url": "https://swapi.co/api/people/3/"
    },
    {
      "id": 4,
      "name": "Darth Vader",
      "height": "202",
      "mass": "136",
      "hair_color": "none",
      "skin_color": "white",
      "eye_color": "yellow",
      "birth_year": "41.9BBY",
      "gender": "male",
      "homeworld": "https://swapi.co/api/planets/1/",
      "films": [
          "https://swapi.co/api/films/2/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/3/",
          "https://swapi.co/api/films/1/"
      ],
      "species": [
          "https://swapi.co/api/species/1/"
      ],
      "vehicles": [],
      "starships": [
          "https://swapi.co/api/starships/13/"
      ],
      "created": "2014-12-10T15:18:20.704000Z",
      "edited": "2014-12-20T21:17:50.313000Z",
      "url": "https://swapi.co/api/people/4/"
    },
    {
      "id": 5,
      "name": "Leia Organa",
      "height": "150",
      "mass": "49",
      "hair_color": "brown",
      "skin_color": "light",
      "eye_color": "brown",
      "birth_year": "19BBY",
      "gender": "female",
      "homeworld": "https://swapi.co/api/planets/2/",
      "films": [
          "https://swapi.co/api/films/2/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/3/",
          "https://swapi.co/api/films/1/",
          "https://swapi.co/api/films/7/"
      ],
      "species": [
          "https://swapi.co/api/species/1/"
      ],
      "vehicles": [
          "https://swapi.co/api/vehicles/30/"
      ],
      "starships": [],
      "created": "2014-12-10T15:20:09.791000Z",
      "edited": "2014-12-20T21:17:50.315000Z",
      "url": "https://swapi.co/api/people/5/"
    },
    {
      "id": 6,
      "name": "Owen Lars",
      "height": "178",
      "mass": "120",
      "hair_color": "brown, grey",
      "skin_color": "light",
      "eye_color": "blue",
      "birth_year": "52BBY",
      "gender": "male",
      "homeworld": "https://swapi.co/api/planets/1/",
      "films": [
          "https://swapi.co/api/films/5/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/1/"
      ],
      "species": [
          "https://swapi.co/api/species/1/"
      ],
      "vehicles": [],
      "starships": [],
      "created": "2014-12-10T15:52:14.024000Z",
      "edited": "2014-12-20T21:17:50.317000Z",
      "url": "https://swapi.co/api/people/6/"
    },
    {
      "id": 7,
      "name": "Beru Whitesun lars",
      "height": "165",
      "mass": "75",
      "hair_color": "brown",
      "skin_color": "light",
      "eye_color": "blue",
      "birth_year": "47BBY",
      "gender": "female",
      "homeworld": "https://swapi.co/api/planets/1/",
      "films": [
          "https://swapi.co/api/films/5/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/1/"
      ],
      "species": [
          "https://swapi.co/api/species/1/"
      ],
      "vehicles": [],
      "starships": [],
      "created": "2014-12-10T15:53:41.121000Z",
      "edited": "2014-12-20T21:17:50.319000Z",
      "url": "https://swapi.co/api/people/7/"
    },
    {
      "id": 8,
      "name": "R5-D4",
      "height": "97",
      "mass": "32",
      "hair_color": "n/a",
      "skin_color": "white, red",
      "eye_color": "red",
      "birth_year": "unknown",
      "gender": "n/a",
      "homeworld": "https://swapi.co/api/planets/1/",
      "films": [
          "https://swapi.co/api/films/1/"
      ],
      "species": [
          "https://swapi.co/api/species/2/"
      ],
      "vehicles": [],
      "starships": [],
      "created": "2014-12-10T15:57:50.959000Z",
      "edited": "2014-12-20T21:17:50.321000Z",
      "url": "https://swapi.co/api/people/8/"
    },
    {
      "id": 9,
      "name": "Biggs Darklighter",
      "height": "183",
      "mass": "84",
      "hair_color": "black",
      "skin_color": "light",
      "eye_color": "brown",
      "birth_year": "24BBY",
      "gender": "male",
      "homeworld": "https://swapi.co/api/planets/1/",
      "films": [
          "https://swapi.co/api/films/1/"
      ],
      "species": [
          "https://swapi.co/api/species/1/"
      ],
      "vehicles": [],
      "starships": [
          "https://swapi.co/api/starships/12/"
      ],
      "created": "2014-12-10T15:59:50.509000Z",
      "edited": "2014-12-20T21:17:50.323000Z",
      "url": "https://swapi.co/api/people/9/"
    },
    {
      "id": 10,
      "name": "Obi-Wan Kenobi",
      "height": "182",
      "mass": "77",
      "hair_color": "auburn, white",
      "skin_color": "fair",
      "eye_color": "blue-gray",
      "birth_year": "57BBY",
      "gender": "male",
      "homeworld": "https://swapi.co/api/planets/20/",
      "films": [
          "https://swapi.co/api/films/2/",
          "https://swapi.co/api/films/5/",
          "https://swapi.co/api/films/4/",
          "https://swapi.co/api/films/6/",
          "https://swapi.co/api/films/3/",
          "https://swapi.co/api/films/1/"
      ],
      "species": [
          "https://swapi.co/api/species/1/"
      ],
      "vehicles": [
          "https://swapi.co/api/vehicles/38/"
      ],
      "starships": [
          "https://swapi.co/api/starships/48/",
          "https://swapi.co/api/starships/59/",
          "https://swapi.co/api/starships/64/",
          "https://swapi.co/api/starships/65/",
          "https://swapi.co/api/starships/74/"
      ],
      "created": "2014-12-10T16:16:29.192000Z",
      "edited": "2014-12-20T21:17:50.325000Z",
      "url": "https://swapi.co/api/people/10/"
    }
  ]
}
  ```

## Our API Routes
For our API, we'll want developer to be able to make GET requests to following routes for data. The root url will be `https://Star-Wars-API--aaronhayslip.repl.co` (because that's what repl.it gives us), but the following url's will be the routes we'll define for our API:

- `/people`: This route will return _all_ the people in our `people.json` file. We'll also want to enable developers to pass this route an optional query to search for people by name. For example, if we make a GET reqeust to `https://Star-Wars-API--aaronhayslip.repl.co/people?name=skywalker`, it should return both Luke and Leia (I know - her real last name is Organa, but we're imagining that it remained Skywalker after birth).
- `/person/:id`: This route will return a single person from our `people.json` file, based on the id. The syntax that looks like, `:id`, is a parameter. In other words, we'll replace the `:id` part with an actual id when we do the request. For example, `https://Star-Wars-API--aaronhayslip.repl.co/person/2` should return all the data for `C-3PO`.

That's it for this little API! Let's get coding!

## ExpressJS
We're going to be using a framework called [Express JS](https://expressjs.com/) to make our API. We could built it without Express, but no one really would or should because it would be a pain. If you look at line 10 of `package.json`, you'll see that we're including `express`. You don't have to know how that works, just know that we're pulling the code in.

Next add the following started code to `index.js`:

```js
const express = require('express');
const fs = require('fs');

const app = express();
```

For the sake of time, we're going to breeze through this. The above code is importing `express` in and also `fs`. `fs` is the "file system" module which is built into Node. We'll use it to read our JSON file.

Next, `const app = express();` is kickstarting our Express code.

## Defining a Route
Let's start by defining a very simple route. Make `index.js` look like this:

```js
const express = require('express');
const fs = require('fs');

const app = express();

app.get('/people', (req, res) => {
  res.send('hello world!');
});

app.listen(3000, () => {
  console.log('server started');
});
```

We can use `get` to define a GET route. This function (`get`) takes two arguments. The first is the path of the URL (in this case, `/people`), and the second argument is a callback function which takes two parameters itself. These two paramaters are the "request" object (`req`) and "response" object `req`. Each of these items are objects that represent data about the request and about the response. Note that from our routes, we _have_ to send a response back (`res.send`).

The final piece of code is the code that allows our app to being listening for connections on port 3000. Again, we won't go into too much depth in explaining that piece at the moment.

To try all of this out, click "Start". Then, in panel 3, click this little button:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-29-at-2.36.35-PM-1.png)

That will open the repl.it browser in a new tab:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-29-at-2.37.53-PM.png)

The first thing you will see is an error, `Cannot GET /` which is because we don't have a route defined for `/`. But we do have one for `/people`! So change that URL to look like `https://star-wars-api--aaronhayslip.repl.co/people` and you should see a response!

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-29-at-2.39.28-PM.png)

## Returning All the People
Now instead of just returning `hello world`, we want to return all the `people` from the JSON file. First, we'll have to read our file using the `fs` module. Change `index.js` to look like this:

```js
const express = require('express');
const fs = require('fs');

const app = express();

app.get('/people', (req, res) => {
  const people = JSON.parse(fs.readFileSync('people.json'));
  
  res.send(people);
});

app.listen(3000, () => {
  console.log('server started');
});
```

Now if you click "restart" and refresh the browser tab, you should see all the JSON data in the browser!

## Querying a Search for People
This is awesome, but what is someone wants to do a search for "Skywalker"? For example, what if instead of just making a request to `/people`, someone wants to make a request to `/people?name=skywalker`? Let's change our code to look like this:

```js
const express = require('express');
const fs = require('fs');

const app = express();

app.get('/people', (req, res) => {
  const people = JSON.parse(fs.readFileSync('people.json'));

  if (req.query.name) {
    const queryName = req.query.name.toLowerCase();

    res.send(people.results.filter(p => p.name.toLowerCase().includes(queryName)))
  } else {
    res.send(people);
  }
});

app.listen(3000, () => {
  console.log('server started');
});
```

Depending on your familiarity with JavaScript, this may look like jibberish. That's okay. What we're essentially doing is checking to see if there is a query called `name` on the URL. If there is, we're filtering out any of the "people" objects inside of `people.json` based on the query that came in with the request. Otherwise (`else`), we're just sending back all the people.

## A Route for 1 Person
Almost done! Now we want to define our next route which will enable developers to make requests to our API for 1 specific person based on their id. The route will look like this (at first):

```js
const express = require('express');
const fs = require('fs');

const app = express();

app.get('/people', (req, res) => {
  const people = JSON.parse(fs.readFileSync('people.json'));

  if (req.query.name) {
    const queryName = req.query.name.toLowerCase();

    res.send(people.results.filter(p => p.name.toLowerCase().includes(queryName)))
  } else {
    res.send(people);
  }
});

app.get('/person/:id', (req, res) => {

});


app.listen(3000, () => {
  console.log('server started');
});
```

The first thing we'll want to do is grab the `:id` parameter from the URL. We can do that inside of Express with `req.params` sort of like how we grabbed the query with `req.query`. Here is the rest of the code:

```js
const express = require('express');
const fs = require('fs');

const app = express();

app.get('/people', (req, res) => {
  const people = JSON.parse(fs.readFileSync('people.json'));

  if (req.query.name) {
    const queryName = req.query.name.toLowerCase();

    res.send(people.results.filter(p => p.name.toLowerCase().includes(queryName)))
  } else {
    res.send(people);
  }
});

app.get('/person/:id', (req, res) => {
  const people = JSON.parse(fs.readFileSync('people.json')).results;
  const allPossibleIds = people.map(p => p.id);
  const id = parseInt(req.params.id);

  if (!allPossibleIds.includes(id)) {
    res.status(404)
    res.send('This id does not exist');
  } else {
    res.send(people.filter(p => p.id === id));
  }
});


app.listen(3000, () => {
  console.log('server started');
});
```

There are some complicated bits in there, but essentially we created an array called `allPossibleIds` which represented a list of all the ids we have in our `people.json` file. We did this just in case someone makes a request for an id that we don't have.

## Conclusion

