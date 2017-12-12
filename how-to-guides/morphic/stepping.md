# Stepping

What is "stepping" anyway? In a broader sense just what the name suggests. More specifically, the method `step` will be invoked at regular intervals.

The "stepping" mechanism can be activated an de-activated with the methods `startStepping` and `stopStepping` respectively.

When a Morph "starts stepping" its `step` method will be called at the intervals specified by `stepTime`. The latter specifies how many milliseconds should pass between one `step` invocation and the `next. The Morphic system will do its best to honor this, but it might not always be possible. That number should be taken as the "minimum amount of time that will pass between step invocations".

Something changing at regular intervals is a good opportunity to implement something like an animation, but it does not need be the case. You could as well modify some internal state, or do something else, instead of changing the visible aspect of your Morph.