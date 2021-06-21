# "Englisch-Bubble-Sort-C#"

this is for an uni project

script:   https://cdn.jsdelivr.net/npm/phoenix-js@1.0.3/dist/glob/main.js

@LIA.eval: @LIA.eval_(false,@uid,`@0`,@1,@2)
@LIA.evalWithDebug: @LIA.eval_(true,@uid,`@0`,@1,@2)

@LIA.eval_
<script>
var hash = Math.random().toString(36).replace(/[^a-z]+/g, '')
var ROOT_SOCKET = 'wss://liarunner.herokuapp.com/socket'; // default path is /socket

var socket = new Socket(ROOT_SOCKET,
  { timeout: 30000,
  logger: function(kind, msg, data) {
      window.console.log(`${kind}: ${msg}`, data)
  }
});

socket.connect(); // connect
var chan = socket.channel("lia:"+hash);

let current_retries = 0;

const timer = (() => {
  let counter = 105; // seconds (found by testing)

  send.lia("LIA: terminal")
  send.lia("LIA: stop")

  const timerHandle = setInterval(() => {
    console.clear();
    if(counter > 0) {
        counter--;
        if(counter < 95) console.log(`ETA until execution: ${counter}s, Retries: ${current_retries}`);
    }
    else if(counter <= 0) {
      console.log(`Couldn't reach server in the estimated time. Is your internet connection working?`)
    }
  }, 1000);

  const stop = () => {
    clearInterval(timerHandle);
    console.clear();
  };

  const timer = {
    stop: stop
  };

  return timer;
})();

chan.on("service", (e) => {
  if (e.message.stderr)
    console.error(e.message.stderr)
  else if (e.message.stdout) {
    if (!e.message.stdout.startsWith("Warning: cannot switch "))
      console.stream(e.message.stdout)
  }
  else if (e.message.exit) {
    if(@0) console.debug(e.message.exit)
    send.lia("LIA: stop")
  }
})

// error hook gets called, when a reconnect is attemted
socket.onError((e) => {
  current_retries++
})

var order = @2
var files = {}

if (order[0])
  files[order[0]] = `@input(0)`
if (order[1])
  files[order[1]] = `@input(1)`
if (order[2])
  files[order[2]] = `@input(2)`
if (order[3])
  files[order[3]] = `@input(3)`
if (order[4])
  files[order[4]] = `@input(4)`
if (order[5])
  files[order[5]] = `@input(5)`
if (order[6])
  files[order[6]] = `@input(6)`
if (order[7])
  files[order[7]] = `@input(7)`
if (order[8])
  files[order[8]] = `@input(8)`
if (order[9])
  files[order[9]] = `@input(9)`


chan.join()
.receive("ok", (e) => {
    chan.push("lia", {event_id: "@1", message: {start: "CodeRunner", settings: null}})
    .receive("ok", (e) => {
        chan.push("lia", {event_id: "@1", message: {files: files}})
        .receive("ok", (e) => {
            if(@0) console.debug(e.message)
            chan.push("lia", {event_id: "@1", message: {compile: @3, order: order}})
            .receive("ok", (e) => {
                if(@0) console.debug(e.message)
                chan.push("lia", {event_id: "@1", message: {execute: @4}})
                .receive("ok", (e) => {
                    timer.stop();
                    send.lia("LIA: terminal")
                })
                .receive("error", (e) => {
                    timer.stop();
                    console.err("could not start application => ", e)
                    chan.push("lia", {event_id: "@1", message: {stop: ""}})
                    send.lia("LIA: stop")
                })
            })
            .receive("error", (e) => {
                timer.stop();
                send.lia(e.message, e.details, false)
                chan.push("lia", {event_id: "@1", message: {stop: ""}})
                send.lia("LIA: stop")
            })
        })
        .receive("error", (e) => {
            timer.stop();
            lia.error("could not setup files => ", e)
            chan.push("lia", {event_id: "@1", message: {stop: ""}})
            send.lia("LIA: stop")
        })
    })
    .receive("error", (e) => {
        timer.stop();
        lia.error("could not start service => ", e)
        chan.push("lia", {event_id: "@1", message: {stop: ""}})
        send.lia("LIA: stop")
    })
})
.receive("error", (e) => {
  timer.stop();
  lia.error("channel join => ", e);
});


send.handle("input", (e) => {
    chan.push("lia", {event_id: "@1", message: {input: e}})
})
send.handle("stop",  (e) => {
    chan.push("lia", {event_id: "@1", message: {stop: ""}})
});


"LIA: wait"
</script>


@end
-->
