# Generative Art Snippets

A collection of some useful snippets such as shapes, animations, math, custom bezier curves and other small utilities which can be used in crafting computational art.

## Table of contents

- [Shaping Functions](#shaping-functions)

- [Shapes](#shapes)
  
  - [Circle](#circle)
  
  - [Generic shapes](#generic-shapes)
  
  - [Box](#box)

- [Colors](#colors)

- [Transformation](#transformation)
  
  - [Translation](#translation)
  
  - [Rotation](#rotation)
  
  - [Scale](#scale)

- [Math](#math)
  
  - [Vector to float conversion](#vector-to-float-conversion)
  
  - [Scaling coordinate system](#scaling-coordinate-system)
  
  - [Linear interpolation](#linear-interpolation)
  
  - [Smooth randomness](#smooth-randomness)

### Shaping Functions

**Shaping Functions** are the mathematical functions used in crafting shapes, for example - plotting a line using linear  interpolation. Application of these functions includes animating shapes, developing envelopes for music or controlling the flow of values in shaders.

- [Some useful shaping functions by Inigo Quilez](http://www.iquilezles.org/www/articles/functions/functions.htm) - This blog post explains some interesting functions along with their use cases.
- [Visualisation of shaping functions](https://shaping-functions.surge.sh) - This visualisation of shaping functions gives you an idea about the tempo (or motion) and how you can use it in your shaders.

### Shapes

#### Circle

```glsl
float circle(in vec2 px, in float rad){
  vec2 dist = px-vec2(0.5);

  return 1. - smoothstep(rad - (rad * 0.01), rad + (rad * 0.01), dot(dist, dist) * 4.0);
}
```

#### Generic shapes

Create any shape (circle, hexagon, triangle, etc) using the below function by specifying the number of sides and the current pixel position.

```glsl
#define PI 3.14159265359
#define TWO_PI 6.28318530718

float genericShape(vec2 pt, int sides) {
  vec3 color = vec3(0.0);
  float d = 0.0;

  pt = pt * 2. - 1.;

  // Angle and radius from the current pixel
  float a = atan(pt.x, pt.y) + PI;
  float r = TWO_PI / float(sides);

  // Shaping function that modulate the distance
  d = cos(floor(.5 + a/r) * r - a) * length(pt);
}
```

#### Box shape

```glsl
float box(vec2 pt, vec2 size){
  size = vec2(0.5) - size * 0.188;

  vec2 uv = smoothstep(size, size + vec2(1e - 4), pt);
  uv *= smoothstep(size, size + vec2(1e - 4), vec2(1.0) - pt);

  return uv.x*uv.y;
}
```

### Colors

Animate colors -

```glsl
uniform float u_time;

vec3 colorA = vec3(sin(u_time), cos(u_time), 0.85);
vec3 colorB = vec3(tan(u_time), sin(u_time), 0.35);
```

Animate and then mix the color with a value -

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

```glsl
uniform vec2 u_resolution;
uniform float u_time;

vec2 pt = gl_FragCoord.xy/u_resolution.xy;

vec2 translate = vec2(cos(u_time),sin(u_time));

pt += translate * 0.35;
```

#### Rotation

```glsl
uniform float u_time;

mat2 rotate2d(float _angle){
  return mat2(cos(_angle),-sin(_angle), sin(_angle),cos(_angle));
}

vec2 st = gl_FragCoord.xy/u_resolution.xy;

st -= vec2(0.5);
st = rotate2d( sin(u_time)*3.1425 ) * st;
st += vec2(0.5);
```

#### Scale

```glsl
uniform float u_time;

mat2 scale(vec2 _scale){
  return mat2(_scale.x,0.0, 0.0,_scale.y);
}

vec2 st = gl_FragCoord.xy/u_resolution.xy;

st -= vec2(0.5);
st = scale(sin(u_time) * 3.1425 ) * st;
st += vec2(0.5);
```

### Math

#### Vector to float conversion

Use dot product to convert vector to float type.

```glsl
float result = dot(vec2(0.5, 0.85), vec2(12.9898,78.233));
```

#### Scaling coordinate system

Scale a coordinate by `x` units

```glsl
vec2 pt = gl_FragCoord.xy/u_resolution.xy;

pt *= 10.0;
```

#### Linear interpolation

This is what I am using with Noise algorithm

```glsl
// 'i' is an integer and 'f' is a float value
mix(rand(i), rand(i + 1.0), f)
```

#### Smooth randomness

Need to apply smoothness when using 2D random noise ? Use this -

```glsl
// 'i' is an integer and 'f' is a float value
mix(rand(i), rand(i + 1.0), smoothstep(0.,1.,f));
```
