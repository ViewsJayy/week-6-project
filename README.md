# Let's Build an Application!

We are going to put together everything that we learned into one application. This will be an interactive step-by-step guide for building our first application. That application will be a Node.js server that will host HTML pages with React. We will also utilize Node.JS packages to build API endpoints!

From the terminal we can open VS Code by using the command:

```bash
code .
```

At this point you should have an empty folder that is opened in VS Code. Now let's create our first Node.JS package by running the initialization command.

```bash
npm init
```

_You can hit enter for all the questions that it asks for now_.

Inside of VS Code you should see a Package file (package.json) that was created form the `npm init` command. This will be our application Package file. Let's now install a third-party package that will help us create the API we are wanting. The Node.js package we will be installing is called _Express_ ([https://expressjs.com/](https://expressjs.com/)). We will be utilizing some of the helpful functions it ask for creating an application. Let's install it with `npm`.

```bash
# install the express Node.js package and save it to the package.json file
npm install express --save
```

If you look at the package.josn file now you should see a new section called dependencies. It will now have express as one of the dependencies of our application.

Thinking back remember that original node script we ran to create a HTTP server?

```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain’);
  res.end('Hello, World!\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

Let's see how to implement this with _Express_. Create a new file in the "our-first-app" folder called _app.js_. In the file copy the following JavaScript.

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
    res.send('Hello World!')
});

app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`)
});
```

If you compare the script chunks of JavaScript you can see that express handles "some" of the work for us. We will see more of these benefits very soon as we build more of this out. Let's run this application and see what we get!

```bash
node app.js
```

After running that you will be able to go to [http://localhost:3000/](http://localhost:3000/) and you should see the words "Hello World!" printing in the browser.

# Amazing Right!

Now we will make this a little more useful to us. Complete the following changes:

1. Create a new folder called _public_.
2. Create a file called _index.html_ and put it in the newly created _public_ folder. 
3. Add an import to to a new Node.js package called _path_ and assign it to a variable called _path_. 
4. Delete the code `app.get(...)`
5. Add the following code in place of it `app.use(express.static(path.join(__dirname, 'public')));`
6. Add the following code to the _index.html_ file:

```html
<!DOCTYPE html>
<html>

<head>
    <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>

<body>
    <h1>This will be a React app!</h1>
    <main id="app-root"></main>
    <script type="text/babel">
      // const root = ReactDOM.createRoot(...);
      // root.render(...)
    </script>
</body>

</html>
```

That's it! 

In your terminal if you press CTRL-C to exit the application. Try running it again with `node app.js` what do you see when you go to [http://localhost:3000/](http://localhost:3000/)?

**Congratulations!** Now you can creating an HTTP Server that will host your React applications. Try adding more HTML file of React applications we have created so far to your server. 

----

## What is an API?

An _API_, or Application Programming Interface, is a set of rules and protocols that allows different software applications to communicate with each other. It defines the methods and data formats that applications can use to request and exchange information. APIs enable developers to integrate different services, systems, or platforms and leverage their functionalities in their own applications. The standard we will be talking about it _REST_ for building out an API. _REST_ standards up something called _CRUD_ operations to perform this communication. 

_CRUD_ operations refer to the basic operations that can be performed on data in a persistent storage system. These operations are _Create_, _Read_, _Update_, and _Delete_, and they are commonly associated with databases. In the context of web development, these operations can be performed using HTTP verbs (_GET_, _POST_, _PUT_, _DELETE_) to interact with an API or a web server.

Node.js, along with the _Express_ framework, is a popular choice for building web applications and APIs. Express provides a simple and intuitive way to handle HTTP requests and responses, making it easy to implement _CRUD_ operations.

Let's go through each CRUD operation and how it can be implemented using Node.js and Express:

1. _Create (POST)_:

    The POST method is used to create new resources. In Express, you can define a route that handles the HTTP POST requests to create a new resource.
    
    For example:

    ```javascript
    app.post('/users', (req, res) => {
        // Logic to create a new user
        // Access request data using req.body
        // Save the new user to the database
        // Return a response indicating success or failure
    });
    ```

    In this example, a POST request to /users would trigger the code to create a new user.

2. _Read (GET)_:
    The GET method is used to retrieve existing resources. In Express, you can define a route that handles the HTTP GET requests to retrieve a resource or a list of resources.
    
    For example:
    ```javascript
    app.get('/users', (req, res) => {
        // Logic to fetch a list of users from the database
        // Return the list of users as a response
    });

    app.get('/users/:id', (req, res) => {
        // Logic to fetch a specific user by ID from the database
        // Access the ID using req.params.id
        // Return the user as a response
    });
    ```

    In this example, a GET request to /users would retrieve a list of users, and a GET request to /users/:id (with a specific ID) would retrieve a single user.

3. _Update (PUT)_:
    The PUT method is used to update existing resources. In Express, you can define a route that handles the HTTP PUT requests to update a resource.
    
    For example:
    ```javascript
    app.put('/users/:id', (req, res) => {
        // Logic to update a specific user by ID in the database
        // Access the ID using req.params.id
        // Access the updated data using req.body
        // Update the user in the database
        // Return a response indicating success or failure
    });
    ```

    In this example, a PUT request to /users/:id (with a specific ID) would trigger the code to update the corresponding user.

4. _Delete (DELETE)_:
    The DELETE method is used to delete existing resources. In Express, you can define a route that handles the HTTP DELETE requests to delete a resource.
    
    For example:
    ```javascript
    app.delete('/users/:id', (req, res) => {
        // Logic to delete a specific user by ID from the database
        // Access the ID using req.params.id
        // Delete the user from the database
        // Return a response indicating success or failure
    });
    ```

    In this example, a DELETE request to /users/:id (with a specific ID) would trigger the code to delete the corresponding user.

By utilizing these HTTP verbs and corresponding routes in _Express_, you can easily implement the _CRUD_ operations for managing data in your web application or _API_.

If you open your browsers developer tools you can go to the network tab and see that when we _request_ the HTML pages we are using the HTTP verb _GET_. When we perform most _Read_ operations we will be using the _GET_ method.

Throughout the next exercise, we will build a new API endpoint that will allow us to call our server for quotes from our React application. 

### Adding an API endpoint to our application

Let's go back to _our-first-app_ and add a simple endpoint. To do this let's follow these simple steps. 

1. Create a new file called _quotes.json_ in the _our-first-app_ folder.
2. Add the following to the _quotes.json_ file:
    ```json
    [
        {
            "text": "Genius is one percent inspiration and ninety-nine percent perspiration.",
            "author": "Thomas Edison"
        },
        {
            "text": "You can observe a lot just by watching.",
            "author": "Yogi Berra"
        },
        {
            "text": "A house divided against itself cannot stand.",
            "author": "Abraham Lincoln"
        }
    ]
    ```
3. Open _app.js_ again. 
4. Right before the call to _app.listen_ let's add the following code.
    ```javascript
    app.get('/api/quotes', (req, res) => {
        res.json(quotes);
    });
    ```
5. At the top of _app.js_ import the _quotes.json_ file using _require_.

If you run `node app.js` again in your terminal and navigate to [http://localhost:3000/api/quotes](http://localhost:3000/api/quotes) you should see the quotes from the file. Spend some time adding your own quotes to the file and restarting the server again to see them!

### Want to see them rendered in React?

Add a new file called _quotes.html_ to the _public_ folder and add the following template to the new file:

```html
<!DOCTYPE html>
<html>

<head>
    <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>

<body>
    <main id="app-root"></main>
    <script type="text/babel">
        const Quotes = () => {
            const [quotes, setQuotes] = React.useState([]);

            // What does this do?
            // How would I find out?
            React.useEffect(() => {
                fetch('http://localhost:3000/api/quotes')
                    .then((response) => {
                        return response.json();
                    })
                    .then((newQuotes) => {
                        setQuotes(newQuotes);
                    });
            }, [])

            return (
                <div>
                    <h1>Inspirational Quotes of the Day!</h1>
                    Todo - Render the quotes below
                </div>
            )

        }
        const root = ReactDOM.createRoot(document.getElementById('app-root'));
        root.render(<Quotes />);
    </script>
</body>

</html>
```

Inside of the JSX implement the **TODO** that will render each quote and it's author.
