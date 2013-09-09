---
layout: post
title: "Drawing on iOS"
date: 2013-09-08 15:20
comments: true
categories: [iOS, coreimage, coregraphics, quartz2d]
---

# Quartz2D:
- Two dimensional graphics drawing engine that makes up the bulk of the UIKit **Core Graphics** Framework.
- C based API
- Typically used on UIView object
- Features
  - path-based drawing
  - painting with transparency
  - shading, drawing shadows
  - transparency layers
  - color management
  - anti-aliased rendering
  - PDF document generation
  - PDF metadata access
- Works with other technologies like
  - Core Animation
  - OpenGL ES
  - UIKit

## How Quartz2D works
- Painter's model:
  - each successive drawing operation applies a layer of "paint" to an output "canvas"
  - the drawing can be modified by overlaying more paint
- The canvas can be:
  - PDF
  - Bitmap image
  - Printer

## Graphics context (the "canvas")
CGContextRef is the drawing destination. It can be: Window, Layer, Bitmap, PDF, Printer, etc.
- No need to perform device-specific calculations. Quartz takes care of it.
### Type of contexts
1. Bitmap graphics context: rectangular array (or raster) of pixels
2. PDF graphics context
- PDF files, unlike bitmaps, may contain more than one page.
- Drawing a page from a PDF file on a different device results in the image being optimized for the display characteristics of that device.
3. Window graphics context
4. Layer context: `CGLayerRef` is an offscreen drawing destination associated with another graphics context.
5. PostScript graphics context: for printing

## Graphics state
### What is a Graphic state?
- color
- line width
- current position
- text font size 

### Graphics context maintains a stack of Graphic states
When context is created, the stack is empty. When i save a context, the current state is pushed to the stack
- `CGContextSaveGState` pushes the current context onto stack
- `CGContextRestoreGState` pops the stack to restore previous context

## Quartz2D Coordinate systems
### How Quartz2D achieves Device independent representation
uses a separate coordinate system (`user space`), mapping it to the coordinate system of the output device (`device space`), using the current transformation matrix (CTM).
- CTM: affine transform matrix
  - maps points by applying translation (move), rotation (rotate), and scaling (resize) operations.
  - to draw a box 45 degrees rotated, rotate CTM first and then draw inside the box.
### Origin (0,0) is bottom-left corner.    
![Quartz2D coordinate system](https://developer.apple.com/library/ios/DOCUMENTATION/GraphicsImaging/Conceptual/drawingwithquartz2d/Art/quartz_coordinates.gif)
This is different from some other drawing coordinate systems
- UIView: top-left corner is (0,0)
  - to switch, apply a transform that translates the origin to the upper-left corner of the PDF context and scales the y-coordinate by -1.
  - However, if you use a UIImage object to wrap a CGImage object you create, no need to modify the CTM.

![Modifying the coordinate system](https://developer.apple.com/library/ios/DOCUMENTATION/GraphicsImaging/Conceptual/drawingwithquartz2d/Art/flipped_coordinates.jpg)
