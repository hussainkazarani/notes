## Basics
> \- Normal Flow goes as follows: <br>
> `Client Requests` &rarr; `Server Responds` &rarr; `Cycle Closes` <br>
> 
> \- to keep a open cycle so that a server can send a response anytime it want we use websockets.
>
> \- it does this by turning a clients HTTP Protocol connection into a Websocket Protocol connection using the `upgrade` header and this connection stays open until we close it

## Websockets in Node.js (socket.io)
install the package on backend
```js
npm install socket.io
```

on frontend, we have to add script from documentation as follows:
> 1\. go to Socket.io &rarr; Docs &rarr; Client &rarr; Installation or [click here](https://socket.io/docs/v4/client-installation/)<br>
> 2\. in JS, add at the top: `const socket=io()`

```js
// example in node.js
import {Server} from 'socket.io';
const server = http.createServer((req,res)=>{
    res.write("Hi");
    res.end();
})

const io = new Server(server);
io.on("connection", (socket)=>{
    console.log("Connected", socket.id);

    // send to all connected clients
    io.emit("chat", {
      from: socket.id,
      text: msg
    });

    socket.on("disconnect", () => {
    console.log("Disconnected:", socket.id);
  });
})

server.listen(3000);
```

### Commands
#### Frontend
`socket.on("msg", ()=>{})` &rarr; listens from server

`socket.emit("msg", ()=>{})` &rarr; sends to server

#### Backend
`io.on("connection", (socket)=>{})` &rarr; when someone connects. all connections route inside this. it is \***required**\*

`io.emit("msg", "Hello")` &rarr; sends to everyone listening

`socket.on("msg", ()=>{})` &rarr; listens for message from socket/client

`socket.emit("msg", ()=>{})` &rarr; sends the message to that particular socket back

#### Other
`socket.broadcast.emit()` &rarr; send to everyone except sender

`socket.join(roomID)` &rarr; join a room. only on the server-side

`socket.to(roomID).emit()` &rarr; send to everyone in room except sender

`io.to(roomID).emit()` &rarr; send to everyone in room including sender