---
layout: post
title: "Opaque Types in Objective-c"
date: 2013-09-08 18:05
comments: true
categories: [iOS]
---
# What is an Opaque type?
  - a type that wraps lower-level types
  - used when
    - the underlying implementation is complex
    - the user does not need to know about the inner workings.
  - The individual fields of an object based on an opaque type are hidden from clients, but the type’s functions offer access to most values of these fields

# A. Opaque types in Core Foundation
Core foundation has many "opaque types'. 
## What is Core Foundation?
Core Foundation is a library with a set of programming interfaces conceptually derived from the Objective-C-based Foundation framework but implemented in the C language.
### 1. Makes it possible for the different frameworks and libraries on OS X to share code and data.
Applications, libraries, and frameworks can define C routines that incorporate Core Foundation types in their external interfaces; they can thus communicate data—as Core Foundation objects—to each other through these interfaces.
### 2. Makes some degree of operating-system independence possible
Some Core Foundation types and functions are abstractions of things that have specific implementations on different operating systems.
### 3. Supports internationalization with Unicode strings
Uses CFString, instances of which represent an array of 16-bit Unicode characters. Flexible enough to hold megabytes worth of characters and yet simple and low-level enough for use in all programming interfaces communicating character data
## Opaque type examples in Core Foundation
- CFString: an opaque type that "represents" and operates on Unicode character arrays.
- CFArray: an opaque type for indexed-based collection functionality.

# B. Opaque types in Quartz2D
  - CGPathRef: vector graphics
  - CGImageRef: bitmap images
  - CGLayerRef: drawling layer that can be used for repeated drawing and offscreen drawing
  - CGPatternRef: repeated drawing using patterns
  - CGShadingRef: for gradients
  - CGGradientRef: for gradients
  - CGColorRef: used for colors in Quartz2D
  - CGImageSourceRef: move data into and out of Quartz
  - CGFontRef: to draw text

