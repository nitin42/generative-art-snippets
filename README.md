# Generative Art Snippets

A collection of some useful snippets such as shapes, animations, math, custom bezier curves and other small utilities used in crafting computational art.

## Table of contents

* [Shaping Functions](#shaping-functions)

* [Shapes](#shapes)
  
  * [Circle](#circle)
  
  * [Generic shapes](#generic-shapes)
  
  * [Box](#box)
  
* [Colors](#colors)

* [Transformation](#transformation)

  * [Translation](#translation)
  
  * [Rotation](#rotation)
  
  * [Scale](#scale)
  
* [Math](#math)

  * [Vector to float conversion](#vector-to-float-conversion)
  
  * [Scaling coordinate system](#scaling-coordinate-system)
  
  * [Linear interpolation](#linear-interpolation)
  
  * [Smooth randomness](#smooth-randomness)
  
  ### Shaping Functions
  
  **Shaping Functions** are the mathematical functions used in crafting shapes, for example - plotting a line using linear  interpolation. Application of these functions includes animating shapes, developing envelopes for music or controlling the flow of values in shaders.
  
  * [Some useful shaping functions by Inigo Quilez](http://www.iquilezles.org/www/articles/functions/functions.htm)
  
  * [Visualisation of shaping functions](https://shaping-functions.surge.sh)
  
  ### Shapes
  
  #### Circle
  
  ```glsl
  float circle(in vec2 px, in float radius){
    vec2 dist = px-vec2(0.5);
	  
    return 1.-smoothstep(radius-(radius*0.01),
                         radius+(radius*0.01),
                         dot(dist,dist)*4.0);
  }
  ```
  
  #### Generic shapes
  
  Create a shape (circle, hexagon, triangle, etc) using the below function by specifying the number of sides and the current pixel position.
  
  ```glsl
  float genericShape(vec2 pt, int sides) {
    vec3 color = vec3(0.0);
    float d = 0.0;
    
    pt = pt *2.-1.;

    // Angle and radius from the current pixel
    float a = atan(pt.x,pt.y)+PI;
    float r = TWO_PI/float(sides);

    // Shaping function that modulate the distance
    d = cos(floor(.5+a/r)*r-a)*length(pt);
  }
  ```
  
  #### Box
  
  ```glsl
  float box(vec2 pt, vec2 size){
    size = vec2(0.5) - size * 0.188;
    
    vec2 uv = smoothstep(size, size + vec2(1e - 4), pt);
    uv *= smoothstep(size, size + vec2(1e - 4), vec2(1.0) - pt);
    
    return uv.x*uv.y;
  }
  ```
  
  ### Colors
  
  Change the colors with a tempo -
  
  ```glsl
  uniform float u_time;

  vec3 colorA = vec3(sin(u_time), cos(u_time), 0.85);
  vec3 colorB = vec3(tan(u_time), sin(u_time), 0.35);
  ```
  
  Mix the color with a value -
  
  ```glsl
  uniform float u_time;

  vec3 colorA = vec3(sin(u_time), cos(u_time), 0.85);
  vec3 colorB = vec3(tan(u_time), sin(u_time), 0.35);
  
  void main() {
    gl_FragColor = vec4(mix(colorA, colorB, vec3(sin(u_time)), 1.0);
  }
  ```
  
  ### Transformation
  
  #### Translation
  
  #### Rotation
  
  #### Scale
  
  ### Math
  
  #### Vector to float conversion
  
  #### Scaling coordinate system
  
  #### Linear interpolation
  
  #### Smooth randomness
