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

Once the `get` succeeds, the value should be persisted as long as at least one server is not killed and at least two servers are running (to achieve a quorum).
