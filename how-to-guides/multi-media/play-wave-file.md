# Play a Wave file

First, load the sound like this:

```smalltalk
mySound := SampledSound fromWaveFileNamed: 'c:\windows\media\chimes.wav'.
```

Then play it:

```smalltalk
mySound play.
```

Of course, replace the full file-path with whatever sound file in your system you want to play.

Playing a sound seems to be a non-clocking operation.

