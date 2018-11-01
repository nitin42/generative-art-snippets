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

  <details>
    <summary>**Impulse curve**</summary>
    ```glsl
      float impulse( float k, float x ) {
        float h = k*x;
        return h*exp(1.0-h);
      }
    ```
  </details>
  
  #### Shapes
  
  #### Circle
  
  #### Generic shapes
  
  #### Box
  
  ### Colors
  
  ### Transformation
  
  #### Translation
  
  #### Rotation
  
  #### Scale
  
  ### Math
  
  #### Vector to float conversion
  
  #### Scaling coordinate system
  
  #### Linear interpolation
  
  #### Smooth randomness
