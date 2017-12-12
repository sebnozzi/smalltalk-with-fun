# Animate a Morph

We will animate a Morph by making use of the stepping mechanism. The stepping mechanism is not specific to animations, but it suits the purpose pretty well.

Start by subclassing the Morph class:

```smalltalk
Morph subclass: #MyCustomDrawnMorph
    instanceVariableNames: 'frameNr'
    classVariableNames: ''
    package: 'SmalltalkWithFun'
```

Notice the "frameNr" instance variable.

Implement the initialize method like this:

```smalltalk
initialize
    super initialize.
    self extent: 175@45.
    frameNr := 0.
    self startStepping.
```

We are doing many things here:

1. With `super initialize` we call the superclass version of this method. This is often very important and **vital** when subclassing Morphs
2. By calling `extent:` we set the width and height in one single call.
3. We initialize our instance variable to 0 \(it will change over time during the animation cycle\).
4. We tell the Morphic engine to start "stepping" our Morph.

Implement the `step` method like this:

```
step
    frameNr := (frameNr + 1) % 200.
    self changed.
```

This increases the frame-number while forcing it to remain in the range 0 to 199. After that it marks the Morph as "changed" \(or "dirty"\) so that it is re-drawn at the next opportunity.

How often it will happen is determined by the value returned by the `stepTime` method.

Be sure to implement it like this:

```smalltalk
stepTime
    ^ 40.
```

It's time to implement the custom-drawing. It will do different things depending on the `frameNr`:

```smalltalk
drawOn: aCanvas
    | progressRect progress barColor |
    progress := frameNr min: 100.
    progressRect := self bounds withWidth: progress / 100 * self width.
    barColor := progress < 100
        ifTrue: [  "blueish" Color r: 0.35 g: 0.6 b: 1.0 ]
        ifFalse: [ "green"   Color h: 121 s: 0.4 v: 1.0 ].
    aCanvas fillRectangle: self bounds color: Color lightGray.
    aCanvas fillRectangle: progressRect color: barColor.	aCanvas drawString: progress asString at: (self center translateBy: -6 @ -7).
```

Once all this is in place, you are ready to open your new custom-drawn animated Morph. Do this in a Playground:

```smalltalk
MyCustomDrawnMorph new openInHand.
```

Drop it whenever you like.

Try adding this as the last line of `drawOn:`

```smalltalk
    aCanvas
        drawString: 'frameNr: ' , frameNr asString
        at: (self bottomLeft translateBy: 2 @ -15)
        font: nil
        color: Color darkGray.
```

Notice how between frames 100 and 199 nothing happens. After that a new animation cycle begins. Experiment by changing the methods `stepTime`, `step` and `drawOn:`