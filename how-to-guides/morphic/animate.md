# Animate a Morph

Start by subclassing Morph to create a custom implementation:

```smalltalk
Morph subclass: #MyCustomDrawnMorph
    instanceVariableNames: 'frameNr'
    classVariableNames: ''
    package: 'SmalltalkWithFun'
```

Notice the "frameNr" instance variable.

Implement the initialize method like this:

```
initialize
	super initialize.
	self extent: 100@100.
	frameNr := 0.
	self startStepping.
```

We are doing many things here:

1. With `super initialize` we call the superclass version of this method. This is often very important and **vital** when subclassing Morphs
2. By calling `extent:` we set the width and height at once to 100x100.
3. We initialize our instance variable to 0 (it will alternate between 0 and 1 in our example).
4. We tell the Morphic engine to start "stepping" our Morph.

The last point needs further consideration. What does it mean? For performance reasons, not all Morphs in the Morphic system are "animated". Animation is "turned on" for a specific Morph when it receives the message `startStepping`. As you can imagine, you can stop animation by passing `stopStepping`.

When a Morph "starts stepping" its `step` method will be called at the intervals specified by `stepTime`. The latter specifies how many milliseconds should pass between one `step` invocation and the `next. The Morphic system will do its best to honor this, but it might not always be possible. That number should be taken as the "minimum amount of time that will pass between step invocations".

For our example we will adjust our `stepTime` like this:

```smalltalk
stepTime
    "Call step twice per second (or: every 500 milliseconds)"
    ^ 500.
```

In our `step` method, we will just change our `frameNr` like this:

```smalltalk
step
    frameNr := frameNr + 1.
    frameNr := frameNr % 2.
    self changed.
```

Some explanation:

1. First we increase the `frameNr` by one.
2. But we want it to remain within the maximum amount of frames, in this case 2. So we re-assign the `frameNr` to its "modulo 2" so that anything greater or equal than 2 will go back to 0 or 1.
3. We notify the Morph that some important property of itself has `changed`. This will result in the Morph being redrawn.

The last point is very important. If we didn't call `self changed` we would see no changes happening, even if the `frameNr` had different values.

It's time to implement the custom-drawing. It will do different things depending on the `frameNr`:

```smalltalk
drawOn: aCanvas
    | ovalColor |
    ovalColor := (frameNr = 0)
        ifTrue: [ Color red ]
        ifFalse: [ Color green ].
        aCanvas fillOval: self bounds color: ovalColor.
```

