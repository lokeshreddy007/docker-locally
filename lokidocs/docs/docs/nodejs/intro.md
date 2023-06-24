## Node JS
Node.js is an open-source, cross-platform JavaScript runtime environment that executes JavaScript code outside of a web browser

`One-man army` - runs in a single process. While this certainly has its pros and cons, the asynchronous nature of Node.js allows it to handle multiple requests to a server without the hassle of managing threads.

`So many packages` - has over 1,000,000 open-source packages hosted on npm. 

`Under the hood` - uses Google’s open-source, high-performance JavaScript and WebAssembly engine called V8. This gives Node.js a stronger performance compared to other frameworks.

While we have praised Node.js for running applications on a single thread, there is more to it. When we ask the OS to read a file for us, we use the file system API. Node.js provides us with several APIs that allow us to make asynchronous calls. For Node.js, these underlying APIs are written in C++ and threads are hidden from us. If you have ever worked with threads before, you will realize that things can get messy when dealing with multiple threads. Deadlocks and race conditions are the worst, so having Node.js manage that for us is, undoubtedly, a praiseworthy feature

### How does it work?

`Event loop` - The event loop is initialized when Node.js runs. It can perform otherwise blocking operations in a non-blocking manner. The event loop can be further broken down into phases.

`Event queue` - The event queue stores incoming events in an orderly fashion. It then passes those events one-by-one to the event loop.

`API pool` - The API pool consists of all the APIs that Node.js provides to execute blocking events asynchronously.

 Node.js is still limited by the amount of processing power it can harness. Complex programs that require a lot of processing significantly can slow things down. While Node.js can handle asynchronous I/O functions with ease, it is not suitable for compute-intensive applications like machine learning. Hence, it is essential to weigh the pros and cons before choosing a framework or a runtime environment.

### The beauty of Node.js

Node.js applications run on a single thread and are still able to keep up with multi-threaded applications. This is because Node.js takes full advantage of asynchronous computing. It allows a single server to handle multiple clients at once. Processes, such as fetching data from storage or making new connections, can all be performed asynchronously, ensuring that the application does not get blocked. Furthermore, Node.js processes code sequentially. Without asynchronous operations, the entire program would halt until a file is read or a `setTimeout()` is called.

#### Reference
[Nodejs Eventloop](https://www.freecodecamp.org/news/nodejs-eventloop-tutorial/)

[Node Js What When Where Why How](https://www.freecodecamp.org/news/node-js-what-when-where-why-how-ab8424886e2/)

## Fundamentals

### Input
Passing input to a program using the terminal. `node app.js Hello`
```js
console.log('Hey there,' , process.argv[2]); 
//  process.argv.forEach((val, index) => {
//   console.log(`${index}: ${val}`);
// });

```
 The process module. You might be wondering why we have a 2 in square brackets after argv. This is because all of our command-line arguments are passed to the argv property.

The first argument, 0, is the process.execPath, which is the path of the node executable.
The second argument, 1, is the path of the JavaScript file that is being run.
The next argument(s) are the command-line arguments, if any have been passed. In our case, this will be a simple Hello.
#### Coding challenge

We want to create a random number guessing game. The way it works is that the game generates a random number from 1 to 10, and the player must try to guess it in 3 tries or less.
```js
const readline = require("readline");
let rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

function getRandomIntInclusive(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  //The maximum and minimum is inclusive
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
// We want the player to have 3 tries
let tries = 3;
// We want to player to guess numbers from 1 to 10
let randomNumber = getRandomIntInclusive(1, 10);
rl.setPrompt("Guess the number! (1-10): ");
rl.prompt();
rl.on("line", function (answer) {
  tries--;
  game(tries, randomNumber, answer);
  rl.prompt();
});

function game(tries, randomNumber, guess) {
  if (tries > 0) {
    if (guess == randomNumber) {
      console.log("WINNER");
      process.exit();
    } else if (guess < randomNumber) {
      console.log("TOO LOW");
    } else if (guess > randomNumber) {
      console.log("TOO HIGH");
    } else {
      console.log("NOT A NUMBER");
    }
  } else {
    if (guess == randomNumber) {
      console.log("WINNER");
    } else {
      console.log("YOU LOSE! THE NUMBER WAS:", randomNumber);
    }
    process.exit();
  }
}
```

### Buffer in Node.js

Node.js has a `Buffer` class that provides us with the functionality we discussed above. This `Buffer` class is an array of bytes that is used to represent binary data. Streams, and other file system operations, are usually carried out with binary data, making buffers the ideal candidates for them.

The `Buffer` class is based on JavaScript’s Uint8Array. To put it simply, we can think of `Buffer` objects as arrays that only contain integers from 0 to 255. One distinction is that `Buffer` objects correspond to fixed-sized blocks of memory, which cannot be changed after they are created. There is no explicit way of deleting a buffer, but setting it to `null` will do the job. The memory will be handled by the garbage collector.

### Event-driven architecture

Most of Node.js is built around an asynchronous, event-driven architecture. Core APIs, such as the `fs` module or the `net`, module use events to communicate with the program. Once the `fs` module is ready to provide data to be read, it emits an event. Whenever a new connection is established, the `net.Server` object emits an event.

To handle events, Node.js uses the `events` module. It has a class named `EventEmitter`, and all objects that emit events belong to this class. What should the program do once an event is emitted? For this, the `eventEmitter.on()` function is used. This allows for one or more functions to be _attached_ to a specific event. These _attached_ functions are also called **listeners**, as they _listen_ for events to be emitted. Furthermore, listener functions are called synchronously once the object emits a specific event. This makes sure that the sequence of events is preserved and no race conditions or logic errors arise

```js
const EventEmitter = require('events');
const myEmitter = new EventEmitter();
someFunction = function (){
  console.log('Something has happened!');
}
myEmitter.on('Some event', someFunction);
myEmitter.emit('Some event');
```
-   We import the `events` module in **line 1**.
-   Using the `new` keyword, we create an object and name it `myEmitter` in **line 2**.
-   Since the `on` method needs a function to attach with an event, we define a function named `someFunction` on **line 3**.
-   We define the `on` method on **line 6** and pass it the name of the event, `Some event`, and the function to call when this event is emitted, `someFunction`.
-   Finally, we `emit` our event, `Some event`, on **line 7**.