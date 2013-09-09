---
layout: post
title: "Core Image Basics"
date: 2013-09-07 23:56
comments: true
categories: [iOS,learn,note]
---

Core Image provides a mechanism for **filtering** and **manipulating** images and videos. Think Instagram filter effects.
# Example filters
- cropping
- color effects
- blurring
- warping
- transformations
- gradients

Take a **CIImage** and apply **CIFilter** to draw on **CIContext**

Example

    // 1. Get a CIImage
    CIImage *image = [CIImage imageWithContentsOfURL:myURL];

    // 2. Create a CIFilter
    CIFilter *filter = [CIFilter filterWithName:@"CISepiaTone"];

    // 3. Apply the filter to the image
    [filter setValue:image forKey:kCIInputImageKey];

    // 4. More CIFilter customization
    [filter setValue:[NSNumber numberWithFloat:0.8f] forKey:@"InputIntensity"];

    // 5. Get the resulting image from CIFilter
    CIImage *result = [filter valueForKey:kCIOutputImageKey];

    // 6. Create CIContext
    CIContext *context = [CIContext contextWithOptions:nil];

    // 7. Finally, render CIImage onto Core Graphics Image, which then can be displayed or saved.
    CGImageRef cgImage = [context createCGImage:result fromRect:[result extent];

    // 8. Convert CGImage to UIImage, so we can draw it onto view
    UIImage *resultUIImage = [UIImage imageWithCGImage: cgImage];

    // 9. Get the CGRect to draw on
    CGRect imageRect =[[UIScreen mainScreen] bounds];

    // 10. Draw the UIImage onto the CGRect region
    [resultUIImage drawInRect:imageRect];
