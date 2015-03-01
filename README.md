# Problem

We want to determine the best transitions between 2 songs if we ignore the tempo.

# Questions
1. What determines a good transition?
2. How can we ignore tempo in determining a transition?

# Resources
1. [Echonest API]
2. [Infinite Jukebox]

### 1. Mini-abstract and relevance of [Echonest API]

The Ehonest API is an API for song related information.  It has methods that allow the user to get song information.  Using the pyechonest.track module, you can find the relevant information of a segment to make a good transition.  The information needed is pitch, duration, timbre, and loudness.

```python
import pyechonest.track as track

t = track.track_from_filename('file.mp3')
t.get_analysis() #this MUST be called before getting segment information can occur
for i in range(0,len(t.segments)):
  print t.segments[i]
```

This will print the information of each segment.  In order to get the specific information requested, we would need to access the element in each segment

```python
import pyechonest.track as track

t = track.track_from_filename('file.mp3')
t.get_analysis()
for i in range(0,len(t.segments)):
  print t.segments[i]["timbre"]
  print t.segments[i]["pitches"]
  print t.segments[i]["duration"]
  print t.segments[i]["loudness_max"]
```

### 2. Mini-abstract and relevence of [Infinite Jukebox]

derp.


[Echonest API]: http://developer.echonest.com/docs/v4
[Infinite Jukebox]: http://infinitejuke.com
