# Web performance


## Learnings from Frontentmasters Course "Web Performance"


https://frontendmasters.com/courses/web-performance

* https://speakerdeck.com/stevekinney/web-performance
* https://gist.github.com/stevekinney/fe401ffb8b2b7279e56dd165b272f0c3
* https://github.com/stevekinney/web-performance

### Measure JavaScript Performance 

* https://developer.mozilla.org/en-US/docs/Web/API/Performance

```
const { performance } = require('perf_hooks');

let iterations = 1e7;

const square = (x) => x * x;
const sumOfSquares = (x, y) =>  square(x) + square(y);

performance.mark('start');

while (iterations--) {
  sumOfSquares(iterations, iterations + 1);
}

performance.mark('end');

performance.measure('My Special Benchmark', 'start', 'end');

const [ measure ] = performance.getEntriesByName('My Special Benchmark');
console.log(measure);

```
Getting extra info with node:

```
 node --allow-natives-syntax -trace_opt -trace_deopt --trace-turbo-inlining  benchmark.js
```

Special annotations:

* %NeverOptimizeFunction(add)
* %HaveSameMap(a,b)
* %OptimizeFunctionOnNextCall(add);
* %DeoptimizeFunction
* https://gist.github.com/totherik/3a4432f26eea1224ceeb

### Rendering Performance

#### Avoid Reflow, Layout Trashing
 * Separate measuring from modifying DOM
 * Don't measure but keep state somewhere else.
 * Bundle modifications (in requestAnimationFrame) 
 * https://github.com/wilsonpage/fastdom

#### Avoid Re-Rendering
* Chrome DevTools/.../More Tools/Rendering/Paint Flashing
* Chrome DevTools/.../More Tools/Layers
* Enforce Layers
  * https://developer.mozilla.org/en-US/docs/Web/CSS/will-change will-change: transform
  * Set will-change on mouseenter to 'transform' and back to 'auto' on transitionend or mouseleave

More tips
 * Make sure to use production mode / build 
 * Simple HTML
 * Simple CSS - for example one class name without any nesting
 * Set a simple class to change style 
 * Changing only opacity or CSS transform requires no repaint 
 

### Load Performance

* Cache Control Headers (https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)
  * no-store
  * no-cache
  * max-age
  * immutable
  * s-maxage (for CDNs)
* Content-Addressable-Storage: file contains hash of content
* Service Worker
* Lazy-Loading and Pre-Loading
* web pack bundle analyzer or https://www.npmjs.com/package/vite-bundle-visualizer
* import transform from 'lodash/transform'
* https://github.com/Geocld/vite-plugin-importus
* https://stackoverflow.com/questions/67084600/how-to-config-lodash-tree-shaking-in-vite
* Load components dynamically, dynamic imports
* Some best-practises in HTTP/1 are not-so-good in Http/2
  * (e.b. concatenating files)
  * inlining resources (like images)


*** Build Tools
  * https://github.com/purifycss/purifycss Still useful?


## Learnings from https://frontendmasters.com/courses/web-perf

* https://github.com/toddhgardner/perf-training-website
* https://drive.google.com/drive/folders/13sdKqO8O2L1yr6th9HgPwpncZwTpEPGl

Perceived performance depends on
  * our expectation
  * what we can do/look at something while waiting

Psychology of waiting

1. People want to start
2. Bored waits feel slower
3. Anxious times feels slower than relaxed time
4. Unexplained wait times feels slower
6. Uncertain wait times feels slower
7. People will wait for value