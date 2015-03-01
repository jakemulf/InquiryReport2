# Problem

We want to determine the best transitions between 2 songs if we ignore the tempo.

# Questions
1. What determines a good transition?
2. How can we ignore tempo in determining a transition?

# Resources
1. [Echonest API]
2. [Infinite Jukebox]

### 1. Mini-abstract and relevance of [Echonest API]

The Echonest API is an API for song related information.  It has methods that allow the user to get song information.  Using the pyechonest.track module, you can find the relevant information of a segment to make a good transition.  The information needed is pitch, duration, timbre, and loudness.

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

The Infinite Jukebox is a piece of software developed using the Echonest API.  The goal of this software is to give it a song, and it calculates jumps in the song where a transition can be made that fits the flow of the music.  Transitions are determined based on the weighted Euclidean distance between the timbre, pitch, duration, and loudness of the segments.  If the distance is below a given threshold, the transition will be "good".

This algorithm can be easily modified to ignore distance.  For our purpose, the weighted Euclidean distance will not include the duration, but the pitch, timbre, and loudness will be used.  This will fulfil our purpose of determining a good transition in a song with ignoring tempo, and allows us to better determine transitions between 2 songs if the tempo varies between them.


[Echonest API]: http://developer.echonest.com/docs/v4
[Infinite Jukebox]: http://infinitejuke.com
