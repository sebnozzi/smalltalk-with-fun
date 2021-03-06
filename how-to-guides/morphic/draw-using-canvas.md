# Draw using a Canvas

Create a subclass of a `Morph`:

```smalltalk
Morph subclass: #MyCustomDrawnMorph
        instanceVariableNames: ''
        classVariableNames: ''
        package: 'SmalltalkWithFun'
```

Override the method `drawOn:` like this:

```smalltalk
drawOn: aCanvas
    super drawOn: aCanvas.
```

This will call the default implementation, which is to fill the contents of the Morph with the color blue.

![](/assets/blue-default-morph.png)

In a Playground window, open your custom Morph and reference it with a variable:

```smalltalk
m := MyCustomDrawnMorph new openInHand.
```

Drop the Morph somewhere.

Now, modify your implementation of "drawOn:" to read like this:

```smalltalk
drawOn: aCanvas
	super drawOn: aCanvas.
	aCanvas fillOval: self bounds color: Color red.
```

After you accept the changes, you will notice that the Morph does not change right-away. You can force this programmatically from the Playground window with this:

```smalltalk
m changed.
```

After that, it should look like this:

![](/assets/morph-custom-drawn-red-oval.png)

Notice that within the `drawOn:` the coordinates you pass to the canvas are **absolute**. Nevertheless, anything drawn outside of the Morph's "bounds" (boundaries) will be cropped.

You can query the current "bounds" of your custom-morph with the `bounds` method.
