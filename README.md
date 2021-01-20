# This is a c++ version of the npm package hexmap

so it can be easily used in other platforms with a single core code base

the idea is to use open-gl instead of p5js as I was doing with the typescript version for seeing if everything works. This will probably eventually be done since I also want to learn some open-gl, and this seems like the perfect project. Anyway, I'll be working on that, hopefully it's not too complicated.

## project structure:

- all code goes in src/
- /src/hexmap/ contains all code hexmap needs to work (no graphics)
- /src/draw/ contains all code needed to draw hexagons, points, vectors, etc
- /tests/ contains multiple programs (each with with their own main()) that each do different things. For example, /tests/draw_test.cpp draws components to make sure /src/hexmap functions are working properly and accurately. I'm also thinking about making a test that generates a couple hundred hashes from random points to see if anything crashes, and another test for each icosahedron triangle that tests key points; if each one generates a proper hash point (position is good, it's accurate), it should work for all points (here multiple resolutions would be tested, but if it works for the first 50 or so it should work for all of them up to the point where rounding error and number resolution (int, double) becomes a problem).
- that's pretty much it for now, this should be up and running in a couple time periods, depends on how long it takes me to learn some open-gl.

### important notes

- in chexmap (c++ version of hexmap), icosahedron class contains static methods. In js version, a wrapper Icosahedron object with wrapper instance methods calls c++ static icosahedron functions, and stores variables (resolution, map orientation, and rotation method) for ease of use.

## compatibility notes (with dart & js)

# js / node

- this should be pretty easy, since can pass objects back & forth between js & c++

# dart

- this will be slightly more involved:
  - need to write wrapper class for c++ in c since can only call c from dart

# general (all things considered)

- should icosahedron have instance methods or only have obj with static functions that take params?
  - instance:
    - (node) can you store obj in node env or something like that? (either way need way to store obj somewhere, +1 to instance)
    - (dart) need to store icosahedron obj in c++ c wrapper, same as above (+1 to instance, just need to call static functions from c wrapper with icosahedron obj, but how to get orientation & rotation_method?)
  - static:
    - (node) no benefits really
    - (dart) easier to implement c wrapper, but not by much
