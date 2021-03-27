# Raft

This is an implementation of the Raft algorithm from David Beazley's course on the topic.
Not production code, etc...

Note that persistence has not been implemented, so the key/value store is in-memory.

## How To Run
Written on python 3.8.1. May run on other python versions.
```
pip install flask requests blessings
```

Then run the following in separate processes (preferrably split terminal/tmux panes):
```
./server.py 0
./server.py 1
./server.py 2
```

You should then be able to get/set values:
```
$ ./client.py set foo bar
$ ./client.py get foo
bar
```

Once the `get` succeeds, the value should be persisted as long as you preconditions of raft are met, even if you kill some servers: something like "only kill < half the servers and allow the election (if any) to finish before killing more". 

You can alter config.json to run more servers. Note that raft works best with an odd number of servers. You can also run the servers with `--verbosity=1` or `--versbosity=2` to see more details about what's going on under the hood. If you increase verbosity, it's a good idea to also run with a slower clocktick interval, e.g. `--clocktick-ms=100` (or slower).