Word Cloud Layout
This is a Wordle-inspired word cloud layout written in JavaScript. It uses HTML5 canvas and sprite masks to achieve near-interactive speeds.

See here for an interactive demonstration along with implementation details.

Example cloud of Twitter search results for “amazing”

Usage
See the samples in examples/.

API Reference
# d3.layout.cloud()

Constructs a new cloud layout instance.

# on(type, listener)

Registers the specified listener to receive events of the specified type from the layout. Currently, only "word" and "end" events are supported.

A "word" event is dispatched every time a word is successfully placed. Registered listeners are called with a single argument: the word object that has been placed.

An "end" event is dispatched when the layout has finished attempting to place all words. Registered listeners are called with two arguments: an array of the word objects that were successfully placed, and a bounds object of the form [{x0, y0}, {x1, y1}] representing the extent of the placed objects.

# start()

Starts the layout algorithm. This initialises various attributes on the word objects, and attempts to place each word, starting with the largest word. Starting with the centre of the rectangular area, each word is tested for collisions with all previously-placed words. If a collision is found, it tries to place the word in a new position along the spiral.

Note: if a word cannot be placed in any of the positions attempted along the spiral, it is not included in the final word layout. This may be addressed in a future release.

# stop()

Stops the layout algorithm.

# timeInterval([time])

Internally, the layout uses setInterval to avoid locking up the browser’s event loop. If specified, time is the maximum amount of time that can be spent during the current timestep. If not specified, returns the current maximum time interval, which defaults to Infinity.

# words([words])

If specified, sets the words array. If not specified, returns the current words array, which defaults to [].

# size([size])

If specified, sets the rectangular [width, height] of the layout. If not specified, returns the current size, which defaults to [1, 1].

# font([font])

If specified, sets the font accessor function, which indicates the font face for each word. If not specified, returns the current font accessor function, which defaults to "serif". A constant may be specified instead of a function.

# fontStyle([fontStyle])

If specified, sets the fontStyle accessor function, which indicates the font style for each word. If not specified, returns the current fontStyle accessor function, which defaults to "normal". A constant may be specified instead of a function.

# fontWeight([fontWeight])

If specified, sets the fontWeight accessor function, which indicates the font weight for each word. If not specified, returns the current fontWeight accessor function, which defaults to "normal". A constant may be specified instead of a function.

# fontSize([fontSize])

If specified, sets the fontSize accessor function, which indicates the numerical font size for each word. If not specified, returns the current fontSize accessor function, which defaults to:

function(d) { return Math.sqrt(d.value); }
A constant may be specified instead of a function.

# rotate([rotate])

If specified, sets the rotate accessor function, which indicates the rotation angle (in degrees) for each word. If not specified, returns the current rotate accessor function, which defaults to:

function() { return (~~(Math.random() * 6) - 3) * 30; }
A constant may be specified instead of a function.

# text([text])

If specified, sets the text accessor function, which indicates the text for each word. If not specified, returns the current text accessor function, which defaults to:

function(d) { return d.text; }
A constant may be specified instead of a function.

# spiral([spiral])

If specified, sets the current type of spiral used for positioning words. This can either be one of the two built-in spirals, "archimedean" and "rectangular", or an arbitrary spiral generator can be used, of the following form:

// size is the [width, height] array specified in cloud.size
function(size) {
  // t indicates the current step along the spiral; it may monotonically
  // increase or decrease indicating clockwise or counterclockwise motion.
  return function(t) { return [x, y]; };
}
If not specified, returns the current spiral generator, which defaults to the built-in "archimedean" spiral.

# padding([padding])

If specified, sets the padding accessor function, which indicates the numerical padding for each word. If not specified, returns the current padding, which defaults to 1.

# random([random])

If specified, sets the internal random number generator, used for selecting the initial position of each word, and the clockwise/counterclockwise direction of the spiral for each word. This should return a number in the range [0, 1).

If not specified, returns the current random number generator, which defaults to Math.random.

# canvas([canvas])

If specified, sets the canvas generator function, which is used internally to draw text. If not specified, returns the current generator function, which defaults to:

function() { return document.createElement("canvas"); }
When using Node.js, you will almost definitely override this default, e.g. using the canvas module.
