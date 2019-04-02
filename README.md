# A research on facebook

## Running the application on a local web server
Clone the repository to your local machine.
```
cd your/desired/path/
git clone https://github.com/BastianA/fbres.git
```
To run the application locally we need to serve it through a simulated web server.
Make sure you have [node.js](https://nodejs.org/en/) installed.
Now run 
```
npm install -g http-server
```
to install your node web server.
Now cd into the project directory and type `http-server -c-1` to run it. The cache timeout flag is optional. 
The server will be served at `http://localhost:8080/`