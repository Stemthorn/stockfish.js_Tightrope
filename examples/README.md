### Web Examples

To try out the web examples, download this repository and then start the included web server by running

```bash
node server.js
```

Then you can go to `http://localhost:9091/demo.html` to see a simple but working example of how to integrate stockfish.js into the frontend with a board. See `loadEngine.js` and `enginegame.js` to learn more.

You can also view `http://localhost:9091/` for a rudimentary example of how to send commands directly to the engine.

### Node.js Examples

If you want to use stockfish.js from the command line, you may want to simply install it globally: `npm install -g stockfish`. Then you can simply run `stockfish`.

In Node.js, the engines themselves can either be executed directly from the command line (i.e., `node stockfish.js` or `child_process.spawn("stockfish.js")`) or `require()`'d as a CommonJS module (i.e., `var stockfish = require("stockfish.js");`).

You can also require this repository directly for a simple engine interface.

First run:

```bash
npm init -y
npm install stockfish
```

Then create a script, like `run-stockfish.js`:
```js
var stockfish = require("stockfish")("lite-single", function onReady() {
    stockfish.sendCommand("uci");
    stockfish.sendCommand("go depth 5");
});
stockfish.listener = function (line) {
    console.log("STDOUT:", line);
    if (/bestmove \S+/.test(line)) {
        console.log("The best move is " + line.match(/bestmove (\S+)/)[1] + ".");
    }
};
```

For more detailed examples on how to use stockfish.js from the command line, see `node_abstraction.js`, `node_direct.js`, `node_module.js`, and `node_spawn.js`.

### License

Example code: MIT
