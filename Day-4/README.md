# Week-11 -- Day-4

## MongoDB Database  

Let's add mongo database to our express app.

### Installing & Running MongoDB (Mac)

Tree House has a good article on how to get started with MongoDB:

https://treehouse.github.io/installation-guides/mac/mongo-mac.html

Make sure you have brew installed before running the commands below. Sorry :(
Here is an excerpt of their instructions:

-   **Open the Terminal app**  and type  `brew update`.
-   **After updating Homebrew**  `brew install mongodb`
-   **After downloading Mongo,**  create the “db” directory. This is where the Mongo data files will live. You can create the directory in the default location by running  `mkdir -p /data/db`
-   **Make sure that the  `/data/db`  directory has the right permissions**  by running

    ```
    > sudo chown -R `id -un` /data/db
    > # Enter your password

    ```

-   **Run the Mongo daemon**, in one of your terminal windows run  `mongod`. This should start the Mongo server.

Reach out to me if you don't have a Mac machine or the instructions don't work for you. I don't mind helping you out. You can also google "How to install and run MongoDB on Windows"

Just remember you need to run mongo db just like you would run an express app. It's a service that needs to be running in the background. It even has a dedicated port!

### Connecting to MongoDB from Express

Run

    npm install mongoose --save

Then in your server.js file add the following code somewhere towards the top:

    // ******************************************** DATABASE ********************************************
    //Import the mongoose module
    var mongoose = require('mongoose');

    //Set up default mongoose connection
    var mongoDB = 'mongodb://127.0.0.1/my_database';
    mongoose.connect(mongoDB, {useNewUrlParser: true, useUnifiedTopology: true})
      .then(() => {
            console.log('Connection to MongoDB Successful');
         });

    //Get the default connection
    var db = mongoose.connection;

    //Bind connection to error event (to get notification of connection errors)
    db.on('error', console.error.bind(console, 'MongoDB connection error:'));
    // ******************************************** END DATABASE ********************************************

Note: The name of the Database you are using with the code above is called

> my_database

Feel free to change it.

If you start your server and see

> Connection to MongoDB Successful

you have successfully connected to MongoDB!

Congrats. Now celebrate

![enter image description here](https://media.giphy.com/media/KYElw07kzDspaBOwf9/giphy.gif)
