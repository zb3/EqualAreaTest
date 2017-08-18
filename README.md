# Equal Area Test

It's an interactive web based app that let's you see how good you are at comparing areas of various 2D figures.
See it in action [here](https://zb3.github.io/EqualAreaTest/)

Tested on desktop chromium and firefox only, but at least some parts should work™ on Edge.


## History

Oh wait that's not Wikipedia... but anyway, I got the idea in august 2014 but couldn't start until in january 2015, then a week later the development stopped and I forgot about the whole thing... only do discover it on my hard drive in december 2016... so I decided to finish it. But for some reason I didn't release it, so in august 2017 I thought "3 years is enough time" and finally released this thing.

BTW I was about to remove this section coz it sucks, but since it's called history - let me keep it.


## Some info


### Computing area

There are two ways used to compute areas in this app. The first one is using mathematical formulas to do it (for polygons and ellipses), and the second is just counting pixels on a `canvas` element. Of course, the first is faster and the second is more correct (because in this app we care about what's displayed).

### Finding solutions

The goal is to move the lines inside a so called frame to a point where area of all polygons inside that frame, defined by those lines will be equal. This is not done via a mathematical formula, but by searching. The algorithm doesn't just try all possible points as this could be too expensive and inaccurate.

The search starts at a randomly choosen point. Then we calculate the "score" of the solution, and we try to move in four directions (by a given amount, let's say `R`) to see what happens. If we were able to score more, we choose the best direction and we move. At first by `R`, then again until we're able to increase our score. This process is then repeated (we're obviously not able to "go back") till the point where any move by `R` makes it worse. If so, we decrease `R` until we can score something or it's very small, and then we start searching again.


## Bonus game

`util.js` file may contain interesting stuff even if for you the app isn't actually interesting.

Functions there ("not really" documented):
`eat.util.lineline` - collision between line segments
`eat.util.linewithcircle` - collision between a line segment and a circle
`eat.util.pointlinedist` - name says it all
`eat.util.insideFrame([0, [x1, y1], [x2, y2], ..., [xn, yn]])` - point inside a polygon?
`eat.util.normalizePoly` - remove duplicate and degenerate vertices
`eat.util.splitPolysByLine` - this one is hardcore... analyse this if you want to know how to split an arbitrary 2D polygon by a given line.
`eat.util.ellipseAreaFromAngles` - name also says it all
`eat.util.polysArea` - simply compute the area of a given set of polygons

You can try to deobfuscate the code (it wasn't obfuscated on purpose) and analyse how it works. It took me a while to figure out how `splitPolysByLine` works (I wrote that...), but it was fun :)