# Load and play sound \(from a Wave file\)

First, load a Wave file like this:

```smalltalk
mySound := SampledSound fromWaveFileNamed: 'c:\windows\media\chimes.wav'.
```

Then play it:

```smalltalk
mySound play.
```

You can combine both in one line:

```smalltalk
(SampledSound fromWaveFileNamed: 'c:\windows\media\chimes.wav') play.
```

Replace the full file-path with whatever sound file in your system you want to play.

Playing a sound seems to be a non-clocking operation.

