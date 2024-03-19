# Directional Displace Gizmo

Directional Displace is a Nuke gizmo that allows you to specify the displacement of pixels in an image using an HSV matte. It functions similarly to a normal map but in two dimensions.

## The Problem

ST maps are a common way to represent displacement in 2D images. They work by mapping the position of each pixel in an input image to a new position in an output image. For each pixel in the output image, the red and green channels in the ST map define the x and y coordinates of the corresponding pixel in the source image. In ST maps the X and Y values are normalized to be between 0 and 1, where `(0, 0)` is the bottom left corner of the image and `(1, 1)` is the top right. For example, if the pixel at `(0,0)` in the source image is blue, and the color of the pixel at `(0.5, 0.5)` in the ST map is `rgb(0, 0, 0)`, then the color of the pixel at `(0.5, 0.5)` in the output image will also be blue.

The following ST map would not make any changes to the input position. It gets redder from left to right as the X values of the pixels increase, and greener from bottom to top as the Y values increase.

IMAGE REQUIRED

The following ST map would set every pixel in the output image to be the pixel at `(1, 0)` (the bottom right) of the source image.

IMAGE REQUIRED

The value of every pixel in the ST map is `rgb(1, 0, 0)`, which means that every single pixel in the output image will be take from `(1, 0)` in the source image

While ST maps are very useful for representing displacements, they're not very human-readable. Directional displacement maps are meant to act as a more intuitive way to represent displacement in images by defining the displacement in terms of angle and intensity.

## How Directional Displacement Maps Work

In a normal map, the RGB channels of an image are used to encode the XYZ components of a vector. In a directional displacement map, the HSV channels of an image are used to encode the angle, magnitude, and phase shift of a pixel displacement.

The hue of the directional displacement map defines the angle of displacement as seen below. Since hue is already represented as an angle in most color pickers, setting the direction of displacement usually means swiveling the color picker to point in the direction that you want your image to move.

IMAGE REQUIRED

The saturation of the directional displacement map defines the magnitude of displacement. The more saturated the color, the stronger the effect.

IMAGE REQUIRED

The value (darkness) of the directional displacement map defines the phase shift of the displacement. By default, setting the `position` knob of the node to 0 will create no displacement and setting the knob to 1 will create maximum displacement. Changing the map's value allows you to change this behavior--for example, a map with value 0.5 will have maximum displacement at `position` 0 and no displacement at `position` 1.

IMAGE REQUIRED

### Controls
**Inputs**: 
- `src`: The image to be displaced
- `map`: The directional displacement map

**Knobs**
- `position`: The amount of displacement effect to apply. 0 corresponds to no displacement, 1 corresponds to maximum displacement
- `scale`: The intensity of the displacement effect.