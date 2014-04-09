# Random Color Generator

For generating attractive colors with an element of randomness. Returns a hex string by default.

[Live demo](https://rawgithub.com/davidmerfield/Random-Color/master/demo/index.html)

Disclaimer: Perceived luminance is hard to represent digitally. Colors are quite complicated cultural constructs Nevertheless it's useful to generate attractive colors.

## Usage

Generate a random, attractive color:
'''randomColor()
> '#F7A7D9''''

randomColor also accepts an object with the following features

### Hue

'''randomColor({hue: 'orange'})
> '#F7A7D9''''

Pass a color to return a random color which matched the hue.

'''randomColor({hue: 122})
> '#F7A7D9''''

You could also provide an integer between 0 and 360 which corresponds to the [HSV color wheel](http://en.wikipedia.org/wiki/HSL_and_HSV). This will return a random color with that hue but randomized luminosity.

'''randomColor({hue: 122})
> '#F7A7D9''''

You could also provide an integer between 0 and 360 which corresponds to the [HSV color wheel](http://en.wikipedia.org/wiki/HSL_and_HSV). This will return a random color with that hue but randomized luminosity.

### Format

'''randomColor({format: 'rgb'})
> 'rgb(100,231,87)''''
 
Pass a format to return a random color which matchs the format. Defaults to a hex string. Possible formats include hsv, hsvArray, rgb, rgbArray, and hex. 


## How it works

If you look at a representation of the HSV color space, there's broadly speaking a triangle of attractive colors to the top right for each H value between 0 and 360. 

![Attractive triangle](/demo/attractive_triangle.png "Attractive triangle")

Try to pick an S and V value which lies within this triangle. Pick lighter colors from the top left of this region. Pick darker colors from the lower right of this triangle.

If 'dull' pick outside the attractive triangle

## Code outline

If H, S or V value is passed
   set the values which are passed

1. Determine H value

If a color preference is passed (e.g. orange )
   determine hue range for color (orange hues lie roughly between 18 and 46)
   set H to random integer within that range

If 'monochrome' is passed
   set H to random between 0 and 360
   set S to 0
   set V to 0

If 'contrasts color' is passed
   determine H range for passed color
   pad this range on either side
   Set H to random outside the range of the passed color

If 'complements color' is passed
   determine H range for passed color
   pick random H value within this range
   Increase H by 180

If no hue preference is passed
   set H to random between 0 and 360

2. Decide saturation (S) and brightness (V) values

If 'unweighted' random color is passed
   set H as random between 0 and 360
   set S as random between 0 and 1
   set V as random between 0 and 1

Determine set of points which lie within attractive triangle at the passed H value

If 'bright' is passed
   pick random S,V pair within the upper section of the attractive triangle

If 'dark' is passed
   pick random S,V pair within the lower section of the attractive triangle

If 'vibrant' is passed
   pick random S,V pair within the upper right of the attrative triangle

If 'pastel' is passed
   pick random S,V pair within the upper left of the attractive triangle

If 'dull' is passed
   pick random S,V pair outside the attractive triangle

3. Other options


