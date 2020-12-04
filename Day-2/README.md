# Week-11 -- Day-2

## Express Endpoints

There are two main kind of endpoints, API and VIEW kind. Obviously there are other kinds and there are many other ways to categorize them besides calling them API and VIEW but for the sake of simplicity and to help you understand endpoints a little bit better let's start with these two.

### API Endpoint

API endpoint deal with resources in the database. They will create, read, update, or delete a resource or resources in the database. The resource can be anything from a user to a facebook post.

Below is an example of a CREATE (Post) and a READ (Get) all posts. In this case we are NOT dealing with a database but instead 'save' each show resource in an array.

    // show --> {id: 0, title: "title", platform: "platform", releaseYear: year, image: "image"}
    let shows = [];

    // ********************************************* SHOWS API (CRUD) ********************************************* //

    // CREATE
    router.post('/', function(req, res, next) {
      // Extract new show info from body
      let newShow = req.body;
      // Generate id for this new show
      newShow.id = uniqid();
      // Add new show to shows
      shows.push(newShow);
      // Send back new show
      res.send({message: "Success"});
    });

    // READ
    router.get('/', function(req, res, next) {
      console.log(shows);
      // Return all shows
      res.send(shows);
    });


Don't worry if you have questions regarding router or what next is. Some of these concepts will make more sense later.

### VIEW Endpoint

The view endpoints deal with serving a particular view  (HTML or ejs file).
So if somebody goes to the root path of our site '/' we will serve the homepage. Simple right?

    /* GET home page. */
    router.get('/', function(req, res, next) {
      res.render('index', { title: 'TV Shows Home Page', header: 'Welcome' });
    });


In the case above the root file we will be serving is 'index'.

### req and res

req stands for request. It is what is coming in. So if you have a post endpoint the incoming post data is inside `req.body`. There is also `req.params` but more on that on a different day.

res stands for response. It is what you will be using to respond back to whoever or whatever made the request. In the simplest for you can send back and empty json object like so: `res.send({})`
