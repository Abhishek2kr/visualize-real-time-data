# visualize-real-time-data
## Requirement: 
Track the vehicles location.

## Pseudo Plan:
In case of maximum amount of vehicles we need to filter/split them into area wise(For minimize the server load).
Vehicles will be uploading there location per 10 sec, on interval of 10 seconds.
On certain time I will have location differences of all the vehicles which will be helpful indetifying moving and non-moving vehicles.
From front-end side I will be calling api so that I can get the real time data, I should call the api in case of data change only.

## Tools:
Nodejs- For creating runtime environment
Expressjs- Framework for nodejs creating.
Socket.io- Library for real time connection between client and server.
Reactjs- For client side.

## Dummy code:

```javascript
const express = require("express");
const http = require("http");
const socketIo = require("socket.io");
const port = process.env.PORT || 4001;

const app = express();

router.get("/", (req, res) => {
  res.send({ response: "I am alive" }).status(200);
});

const server = http.createServer(app);
const io = socketIo(server);
let interval;
io.on("connection", socket => {
  console.log("New client connected");
  if(interval) clearInterval(interval);
  interval = setInterval(() => getApiAndEmit(socket),10000);
  socket.on("disconnect", () => console.log("Client disconnected"));
});

const getApiAndEmit = async socket => {
  try {
    const processedData = readAndProcessVehiclesData(); // This function is not declared.
    socket.emit("eventName", processedData);
  } catch (error) {
    console.error(`Error: ${error.code}`);
  }
};
server.listen(port, () => console.log(`Listening on port ${port}`));
``` 
