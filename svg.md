# svg

## Icons
    
[https://www.svgrepo.com/](https://www.svgrepo.com/)

[https://icones.js.org/](https://icones.js.org/)

[https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs)

## SVG code

[https://svgjs.com/docs/3.0/manipulating/#resizing](https://svgjs.com/docs/3.0/manipulating/#resizing)

[https://yqnn.github.io/svg-path-editor/](https://yqnn.github.io/svg-path-editor/)

[https://css-tricks.com/libraries-for-svg-drawing-animations/](https://css-tricks.com/libraries-for-svg-drawing-animations/)

[https://svgbox.net/icon-set/materialui](https://svgbox.net/icon-set/materialui)

[https://github.com/LingDong-/psvg](https://github.com/LingDong-/psvg)

[https://github.com/LingDong-/Okb.js](https://github.com/LingDong-/Okb.js)

[https://habr.com/ru/company/ruvds/blog/463329/](https://habr.com/ru/company/ruvds/blog/463329/)

[https://svgjs.com/docs/3.1/plugins/svg-math-js/](https://svgjs.com/docs/3.1/plugins/svg-math-js/)

[https://stackoverflow.com/questions/10798397/how-may-i-use-inline-svg-gradient-on-an-element-like-line](https://stackoverflow.com/questions/10798397/how-may-i-use-inline-svg-gradient-on-an-element-like-line)

- SVG NOISE
    
    Creating Textures (Noise) Using SVG Filters & CSS Gradients
    
    You want noise in your gradient? You're in luck!
    
    [Perlin noise](https://en.wikipedia.org/wiki/Perlin_noise) is a type of gradient noise. The SVG standard specifies a filter primitive called `[<feTurbulence>](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feTurbulence)`, which implements the Perlin function. It allows the synthesis of artificial textures like clouds or marble—the noise you want.
    
    ## Step 1: Define an SVG Graphic
    
    Create a small SVG file called `noise.svg`.
    
    ```
    <svg
      xmlns='http://www.w3.org/2000/svg'
      xmlns:xlink='http://www.w3.org/1999/xlink'
      width='300' height='300'>
    
        <filter id='n' x='0' y='0'>
                <feTurbulence
                  type='fractalNoise'
                  baseFrequency='0.75'
                  stitchTiles='stitch'/>
        </filter>
    
        <rect width='300' height='300' fill='#fff'/>
        <rect width='300' height='300' filter="url(#n)" opacity='0.80'/>
    </svg>
    
    ```
    
    This graphic defines two rectangles. The first is filled with a solid color. The second is translucent with the noise filter applied. The
    second rectangle is overlayed on the first to provide a noise effect.
    
    ### SVG Options
    
    1. Fist and most obvious is that you can change the dimensions of the graphic. However, the CSS `background-repeat` property can be used to fill an element, thus 300×300 should suffice.
    2. The filter's `type` attribute can be `fractalNoise` or `turbulence`, which specifies the filter function. Both provide a different visual,
    but in my opinion, the noise filter is a little more subtle.
    1. The filter's `baseFrequency` attribute can range from
    0.5–0.9 to provide a course to fine texture, respectively. This range is visually optimal for either filter in my opinion.
    1. The first rectangle's `fill` can be changed to provide a different base color. Later, however, we essentially combine this
    color with a translucent CSS gradient, which also defines a color(s). So white is a good starting point here.
    1. The second rectangle's `opacity` can range from 0.2–0.9 to set the filter intensity, where a higher number increases the intensity.
    
    At this point, you could tweak the aforementioned options, set this
    noise graphic as a background image via CSS, and call it a day. But if
    you want a gradient, like the OP, go to Step 2.
    
    ## Step 2: Apply a CSS Gradient
    
    Using the `[background-image](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image)` property, you can set the SVG noise graphic as the background on any element and overlay a [gradient](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Images/Using_CSS_gradients). In this example, I'll apply the noise graphic to the entire body and overlay a [linear gradient](https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient).
    
    ```
    body {
        /* white to black linear noise gradient spanning from top to bottom */
        background:
          linear-gradient(rgba(255,255,255,.5), rgba(0,0,0,.5)),
          url('noise.svg');
    }
    
    ```
    
    The *linear-gradient()* function creates a pseudo image, which is stacked on top of *noise.svg*. The result is a translucent gradient with our noise showing through it.
    
    ### CSS Options
    
    1. First, and most obvious, is that the defined gradient colors can
    be changed. However, if you want a solid color without a gradient, make
    the two end-point colors equal. The benefit is that you can use the same noise graphic with or without a gradient throughout a site or among
    projects.
    1. Multiple images, created with the `[-gradient()` functions](https://developer.mozilla.org/en-US/docs/Web/CSS/gradient), can be overlayed on the noise graphic and more than two color
    parameters and angles can be specified in a single gradient function to
    provide all kinds of cool visuals.
    1. The opacity of the gradient parameters—i.e. rgba() and hsla()—can be increased to intensify the defined color and reduce the noise level. Again, 0.2–0.9 is an ideal range.
    
    ## Conclusion
    
    This is a highly customizable and very light-weight (~400 bytes)
    solution that allows you to simply define noise of any color or
    gradient. Although there are several knobs to turn here, this is only
    the beginning. There are other SVG filter primitives, such as `[<feGaussianBlur>](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feGaussianBlur)` and `[<feColorMatrix>](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/feColorMatrix)`, which can provide additional results.
    
- Filters
    
    [https://www.fecolormatrix.com/](https://www.fecolormatrix.com/)
    
      [https://yoksel.github.io/svg-filters/#/](https://yoksel.github.io/svg-filters/#/)
    
    [https://justcode.today/filters/#](https://justcode.today/filters/#)
    
    [https://svgfilters.com/](https://svgfilters.com/)
    
- SVG Sprites
    
    [https://habr.com/ru/post/272505/](https://habr.com/ru/post/272505/)
    
    [https://github.com/jkphl/svg-sprite](https://github.com/jkphl/svg-sprite)
    
    [https://www.npmjs.com/package/svg-sprite](https://www.npmjs.com/package/svg-sprite)
    
- Generators
    
    [https://squircley.app/](https://squircley.app/)
    
    [https://patternpad.com/editor.html](https://patternpad.com/editor.html)
    
    [https://tabbied.com/select-artwork](https://tabbied.com/select-artwork)
    
    [https://products.ls.graphics/paaatterns/preview.html](https://products.ls.graphics/paaatterns/preview.html)
    
    [https://repper.app/](https://repper.app/)
  [https://www.magicpattern.design/](https://www.magicpattern.design/)