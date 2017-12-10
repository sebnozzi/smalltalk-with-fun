# Execute a deferred action

Sometimes you want to execute asynchronously, with an initial delay.

Open a Playground window and a Transcript window.

Paste this code into the Playground window:

```smalltalk
[ (Delay forSeconds: 2) wait.
Transcript show: 'Appears after two seconds'; cr 
] fork.
```

Execute that code. You should see the message appear in the Transcript window after two seconds.

