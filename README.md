# Jump Start React

In this workshop, we are going to learn how to build apps with React while ignoring all the overwhelming distractions on the web. No build tools for now. We are all going to code together, right in the browser using [JS Bin](http://jsbin.com/). Of course, you need to build tools in real life apps so I am going to show you how to use them at the end of this workshop.


## Who This Workshop is For


- Beginners - will learn how to get started with React.
- Experienced - will get a refresher of the fundamentals of React and how some features work under the hood. You will also learn how best to teach beginners React


## Task 1: Setup Environment

1. Open [JS Bin](http://jsbin.com) and paste the following in the HTML tab

    ```html
        <!DOCTYPE html>
        <html>
        <head>
          <meta charset="utf-8">
          <meta name="viewport" content="width=device-width">
          <link href="https://fonts.googleapis.com/css?family=Lato" rel="stylesheet">
          <title>JS Bin</title>
        </head>
        <body>

        <!--   Coming soon... -->

        </body>
        </html>
    ```


    **Note**
    For sake, we are adding a different font called `Lato`.

2. Open the CSS tab and add the following to it:

    ```css
        body {
          font-family: 'Lato', sans-serif;
        }
    ```

    **Note**
    This adds the font to the body tag of your project.

    DEMO: https://jsbin.com/damayit/1/edit?html,js,output

## Task 2: Hello World in React


1. Update the HTML tab by adding the following inside the `<body>` tag:

    ```html
        <div id="root"></div>
        <script>
          const rootElement = document.getElementById('root')
          const element = document.createElement('h2')
          element.textContent = 'Hello World from React'
          element.className = 'container'
          rootElement.appendChild(element)
        </script>
    ```


    **What is going on?**

      1. First, we create a `div` with an id `root`
      2. Next, we add a `script` tag to contain our JavaScript code. In the JS code, we grab the reference to that div element and pass the reference to a `rootElement` variable.
      3. We also create a new `h2` DOM element using `createElement` and pass the element to an `element` variable.
      4. We then set  text to the new element and a class of container
      5. Finally, we append the `h2` element we to our root `div` element.

    DEMO: https://jsbin.com/pebojug/2/edit?html,js,output


2. You can move the JavaScript code to the JavaScript tab

    DEMO: https://jsbin.com/pebojug/11/edit?html,js,output


3. Next, let’s rebuild this same greeting app with React. Import the following libraries (React and React DOM) below the `root`  element in the HTML:

    ```html
    <script src="https://unpkg.com/react@16.0.0/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16.0.0/umd/react-dom.development.js"></script>
    ```

4. Update the JavaScript code to the following:

    ```javascript
    const rootElement = document.getElementById('root');

        const element = React.createElement(
          'h2', // element.createElement('h2)
          {className: 'container'}, // element.className
          'Hello World from React' // element,textContent
        );

        ReactDOM.render(element, rootElement);
    ```

    **What’s going on?**

      - We are still grabbing the `root` element.
      - We then use the React’s `createElement` method to create a new element. It takes 3 arguments:
        1. The element (eg. `h2`).
        2. Attributes as properties in an object (eg: `className`).
        3. The text content of the element.
      - Then the render method in `ReactDOM` is used to render the element inside `root`.

    **Note**
    This shows we can do the same thing we do with the DOM API using React but with more features and flexibilities which we will see in the rest of this workshop.

    DEMO: https://jsbin.com/pebojug/14/edit?html,js,output


5. Log the value of `element` to the console, let’s inspect it and see what looks like. Paste this below the `element` variable declaration.

    ```html
    console.log(element);
    ```


6. Now open the developer console and expand the object logged. You should see that the `props` property contains the `className` as well as the text content as `children`:
    ![](https://d2mxuefqeaa7sj.cloudfront.net/s_B91C6BDEF00BBA98B3B67441C70824DBBF025433CFEA86FB099C458E2D11F379_1519206268758_Screen+Shot+2018-02-20+at+3.50.46+PM.png)


    **Note**
    For the content of `h2` to be stored in a `children` property in `props` alongside, that means we can have `children` in the object you saw in the second argument of `React.createElement`.


7. Update the JS tab as follows:

    ```javascript
        const rootElement = document.getElementById('root');

        const element = React.createElement(
          'h2',
          {
            className: 'container',
            children: 'Hello World from React'
          }
        );

        ReactDOM.render(element, rootElement);
    ```

    You should see it produces the same output. Now convert the `children` property’s value to an array of strings:

    ```javascript
        const element = React.createElement(
          'h2',
          {
            className: 'container',
            children: [
              'Hello World from React',
              '. Thank you!'
            ]
          }
        );
    ```

    React would append each of the items in the array to the DOM.

    DEMO: https://jsbin.com/pebojug/15/edit?html,js,output

    **Note**
    A React element can also be a one off the items in `children` array. This way you can start building nested DOM trees.


## Task 3: Meet JSX

Though it’s 100% possible to write a React app using `createElement`, you can imagine how difficult it would be when you have a deep DOM tree. JSX allows you to write HTML-like content right inside your JavaScript code.


1. For JSX to work, you need to enable Babel. Babel is a transpiler which basically converts code written in on format or representation to another. Refer to the image below to enable Babel:
    ![](https://d2mxuefqeaa7sj.cloudfront.net/s_B91C6BDEF00BBA98B3B67441C70824DBBF025433CFEA86FB099C458E2D11F379_1519208337357_Screen+Shot+2018-02-21+at+1.16.24+PM.png)


    If you are working with another editor, you can just include this in your HTML:

    ```html
    <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
    ```


2. Update the JS code as follows:

    ```javascript
        const rootElement = document.getElementById('root');

        const props = {
          className: 'container',
          children: [
            'Hello World from React',
            '. Thank you!'
          ]
        }

        const element = <h2 {...props} />

        ReactDOM.render(element, rootElement);
    ```

    What’s happening?

      1. We are writing a JSX and rendering this JSX.
      2. The `props` object is also passed to the JSX using **spread operators**.


3. You can nest elements just the way you write HTML:

    ```html
        const element = <div className="wrapper">
                <h2 {...props} />
              </div>
    ```

    DEMO: https://jsbin.com/yazunus/3/edit?html,js,output


## TASK 4: Composing Components

React is a component-based library, therefore, it encourages the component architectural pattern. Components allows you to build small reusable UI elements and UI widgets then **compose** them to make a full fleshed app. Components are not exclusive to React. It’s a trending pattern for building engineering projects.


1. Assuming you had the following JSX that has a repeating pattern:

    ```html
        <div>
          <h2 className="greeting">Hello World from React</h2>
          <h2 className="greeting">Goodbye from React</h2>
        </div>
    ```

    We are repeating the `h2` tag along with all of its properties. Why don’t we create a `greating` component that we can reuse?


2. Create a function to to return this elements as JSX:

    ```javascript
       const rootElement = document.getElementById('root');

        const greeting = (props) => <h2 className="greeting">{props.children}</h2>

        const element = <div className="wrapper">
                {greeting({children: 'Hello World from React'})}
                {greeting({children: 'Goodbye from React'})}
              </div>

        ReactDOM.render(element, rootElement);
    ```

    DEMO: https://jsbin.com/dugema/2/edit?html,js,output

    As you can see, a component can be a simple function that returns a chunk of HTML elements as JSX.


3. A more intuitive way to write this is to update the `greeting` variable so that it’s in title case. Then you can use it like a normal tag in the JSX. You can’t use the lower case version because JSX would mistake it as an inbuilt HTML tag. Update the code to look like the following:

    ```javascript
        const rootElement = document.getElementById('root');

        const Greeting = (props) => <h2 className="greeting">{props.children}</h2>

        const element = <div className="wrapper">
                <Greeting>Hello World from React</Greeting>
                <Greeting>Goodbye from React</Greeting>
              </div>

        ReactDOM.render(element, rootElement);
    ```


    DEMO: https://jsbin.com/dugema/3/edit?html,js,output


## Task 5: Props and State

To compose components, you need a way to move shared data from one component to another. We have fairly see properties which is only perfect for data that a component must not mutate. Props can only be rendered without changing its value.

States on the other hand gives you the flexibility to store data that can change and probably render this data directly or pass them down to child components as props. States control the behavior of a component.


1. To use state, we need to make use of a class component. Replace the content of your JS with the following:

    ```javascript
        const rootElement = document.getElementById('root');

        const Usernames = (props) => (
          <ul>
            <li>Codebeast</li>
            <li>Eugene</li>
            <li>Jacky</li>
          </ul>
        )

        class App extends React.Component {
           render() {
             return (<div>
                     <Usernames />
                    </div>)
           }
        }

        const element = <App />

        ReactDOM.render(element, rootElement);
    ```


2. Take a close look at the two components and figure out what data might change in the future.
3. The list of usernames. Update the code to store this list in a state:

    ```javascript
        const rootElement = document.getElementById('root');

        const Usernames = (props) => (
          <ul>
          {props.users.map(user => <li>{user.username}</li>)}
          </ul>
        )

        class App extends React.Component {

           constructor(props) {
             super(props)
             this.state = {
               users: [
                 {username: 'Codebeast'},
                 {username: 'Eugene'},
                 {username: 'Jacky'}
               ]
             }
           }
           render() {
             return (<div>
                     <Usernames users={this.state.users} />
                    </div>)
           }
        }

        const element = <App />

        ReactDOM.render(element, rootElement);
    ```

    **What’s going on?**

      1. Each class makes the `props` and `state` available via `this.props` and `this.state`. As for `props`, you need to let tell the base component from React about them by calling `super(props)` in the constructor.
      2. The state is created as an object with a `users` property that stores an array of usernames
      3. We render the `Usernames` child component while passing the `users` state to it via the `users` props.


    DEMO: https://jsbin.com/jilezeq/2/edit?html,js,output


## Task 6: Events

The most common (if not only) way of collecting inputs and actions from the user of our apps is through events. Let’s see how we can collect actions in React apps.


1. Update the render method in the previous task to look like the following:

    ```javascript
        render() {
             return (<div>
                     <Usernames users={this.state.users} />
                     <button onClick={this.addRandomUser.bind(this)}>Add Random User</button>
                    </div>)
           }
    ```

    We now have a button that we attached an `onClick` event to. This event takes a function to call when the button is clicked. In our case, we care calling an instance method named `addRandomUser`.


2. Add this method to your class:

    ```javascript
        addRandomUser() {
             const newUsers = ['Ganga', 'Joy', 'Karis', 'William'];
             const randomNumber = Math.floor(Math.random() * newUsers.length)
             const randomUser = newUsers[randomNumber];
             this.setState({users: [...this.state.users, {username: randomUser}]})
           }
    ```

    **What’s going on?**

      1. We have list of possible new users.
      2. We create a random number by
        1. Generating a random number between 0 and 1
        2. Multiplying it with the length of the array to create a boundary between 0 and the length of the array (4)
        3. Then we floor the number
      3. We use this random number to get a random user from the array
      4. Finally we set the new state of the `users` array by adding the new user to it.

    DEMO: https://jsbin.com/waferog/2/edit?html,js,output

## Task 7: Networking in React

Having a state with static data doesn’t showcase real life situations. Let’s see how we can make a request to a server hosted somewhere else for some data and then render the data in our page.


1. Import the axios library to your HTML:

    ```html
    <script src="https://cdnjs.cloudflare.com/ajax/libs/axios/0.18.0/axios.js"></script>
    ```


2. Add a the following method to the class:

    ```javascript
        componentDidMount() {
            axios.get('https://api.github.com/users/christiannwamba/followers')
              .then(res => {
                const usernames = res.data.map(user => ({username: user.login}));
                this.setState({users: [...this.state.users, ...usernames]});
              })
          }
    ```

    **What's going on?**
      1. We declare a method called `componentDidMount`. This method is one of React’s inbuilt methods that are known as **lifecycle methods**. These methods allow you to hook into a React’s component lifecycle from creation to destruction. In our case we need the to make a request once the component s ready (mounted). No need to call this component, React will after this component is mounted
      2. We then make a request to the Github server to get a user’s followers. The request is made using Ajax.
      3. The payload returned has a lot of data but we just need to get the usernames.
      4. We update the state. **When ever state is updated, the affected components are re-rendered to update the UI**.

    DEMO: https://jsbin.com/hebipux/2/edit?html,js,output


## Task 8: Working with React’s CLI tool (CRA)

Building an app is a process. A process much more complex than writing the code itself. Bundling, performance, offline capabilities, deploying, local development, etc are tasks you might need to consider when building a real app.

The Create React App (CRA) CLI tool simplifies this process.


1. Install [Node.js](https://nodejs.org)
2. Install the CLI tool

    ```bash    
        npm install -g create-react-app
    ```


3. Create a new app:

    ```bash
        create-react-app jump-start
    ```


4. Install axios via npm:

    ```bash
        npm install axios --save
    ```


5. Open the file in a code editor, head to the `src` folder, and add a new file named `Usernames.js` with the following content:

    ```javascript
        import React from 'react';
        export default props => (
          <ul>{props.users.map(user => <li>{user.username}</li>)}</ul>
        );
    ```

6. Update `App.js` to look like the following:

    ```javascript
        import React from 'react';
        import axios from 'axios';
        import Usernames from './Usernames';
        class App extends React.Component {

          constructor(props) {
            super(props)
            this.state = {
              users: [
                {username: 'Codebeast'},
                {username: 'Eugene'},
                {username: 'Jacky'}
              ]
            }
          }

         componentDidMount() {
           axios.get('https://api.github.com/users/christiannwamba/followers')
             .then(res => {
               const usernames = res.data.map(user => ({username: user.login}));
               console.log(usernames)
               this.setState({users: [...this.state.users, ...usernames]});
             })
         }

          addRandomUser() {
            const newUsers = ['Ganga', 'Joy', 'Karis', 'William'];
            const randomNumber = Math.floor(Math.random() * newUsers.length)
            const randomUser = newUsers[randomNumber];
            this.setState({users: [...this.state.users, {username: randomUser}]})
          }

          render() {
            return (<div>
                    <Usernames users={this.state.users} />
                    <button onClick={this.addRandomUser.bind(this)}>Add Random User</button>
                   </div>)
          }
        }
        export default App;
    ```

The major difference is:


  1. We have split the two components into 2 files.
  2. Then import the child component `Usernames` to the parent component `App` for render.
  3. Also, instead of using script tags, we are importing React and axios using `import`.


7. Run `npm start` to see the app in your browser.
