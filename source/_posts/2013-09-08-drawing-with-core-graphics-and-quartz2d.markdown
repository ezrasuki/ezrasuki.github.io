---
layout: post
title: "Drawing with Core Graphics and Quartz2D"
date: 2013-09-08 20:42
comments: true
categories: [iOS, coregraphics, quartz2d]
---

# Various Quartz2D inititalization
## Get the current view's context
Each view has its own drawing context. Let's first get the context.
    CGContextRef graphics_context = UIGraphicsGetCurrentContext();

## Generate color
    // Create colorspace (In this case, RGB space)
    CGColorSpaceRef colorspace = CGColorSpaceCreateDeviceRGB();

    // Set up RGB constant
    CGFloat components[] = {0.0, 0.0, 1.0, 0.5};

    // Create CGColorRef using the colorspace and the RGB variable from above
    CGColorRef color = CGColorCreate(colorspace, components);

    // When done with using the color, let it go
    CGColorRelease (color);

    // After done using the colorspace
    CGColorSpaceRelease(colorspace);

# When do I use UIColor with CGColorRef?
UIColor has lots of convenience methods such as:
    [UIColor redColor]

So instead of going through all the tedious RGB specification, we can just create a `[UIColor redColor]` and then convert it to CGColor, and then use it to set context
    CGContextSetStrokeColorWithColor(context, [UIColor redColor].CGColor);

UIColor avoids the necessity to create colorspaces and components when working with colors.

# Let's actually do some drawing!
## 1. Create a UIView
Just create a project with a UIView
## 2. Modify drawRect:
### Drawing lines
    - (void)drawRect:(CGRect)rect {
        // 1. Get context
        CGContextRef context = UIGraphicsGetCurrentContext();

        // From here, set the context's attributes

        // 2. Set Line Width
        CGContextSetLineWidth(context, 5.0);

        // 3. Set Stroke Color 
        CGColorSpaceRef colorspace = CGColorSpaceCreateDeviceRGB();
        CGFloat components[] = {0.0, 0.0, 1.0, 1.0};
        CGColorRef color = CGColorCreate(colorspace, components);
        CGContextSetStrokeColorWithColor(context, color);

        // 4. Move context's point
        CGContextMoveToPoint(context, 0, 0);

        // 5. Draw line from point to another point
        CGContextAddLineToPoint(context, 150, 150);
        CGContextAddLineToPoint(context, 100, 200);
        CGContextAddLineToPoint(context, 50, 150);
        CGContextAddLineToPoint(context, 100, 100);

        // 6. Actually "stroke" to draw
        CGContextStrokePath(context);

        // 6. Memory release
        CGColorSpaceRelease(colorspace);
        CGColorRelease(color);
    }

### Drawing rectangle
    - (void)drawRect:(CGRect)rect {
        // 1. Init
        CGContextRef context = UIGraphicsGetCurrentContext();
        CGContextSetLineWidth(context, 4.0);
        CGContextSetStrokeColorWithColor(context, [UIColor blueColor].CGColor);

        // 2. Create CGRect area
        CGRect rectangle = CGRectMake(60,170,200,80);

        // 3. Add rectangle region to the context
        CGContextAddRect(context, rectangle);

        // 4. Actually "stroke" to draw
        CGContextStrokePath(context);
    }

### Drawing an ellipse
    - (void)drawRect:(CGRect)rect {
        // 1. Init
        CGContextRef context = UIGraphicsGetCurrentContext();
        CGContextSetLineWidth(context, 4.0);
        CGContextSetStrokeColorWithColor(context, [UIColor blueColor].CGColor);

        // 2. Create CGRect area
        CGRect rectangle = CGRectMake(60,170,200,80);

        // 3. Add ellipse inside the CGRect in context
        CGContextAddEllipseInRect(context, rectangle);

        // 4. Actually "stroke" to draw
        CGContextStrokePath(context);
    }

### Drawing an arc
    - (void)drawRect:(CGRect)rect {
        CGContextRef context = UIGraphicsGetCurrentContext();
        CGContextSetLineWidth(context, 4.0);
        CGContextSetStrokeColorWithColor(context, [UIColor blueColor].CGColor);

        // 1. Set begin point
        CGContextMoveToPoint(context, 100, 100);

        // 2. add arc to context
        CGContextAddArcToPoint(context, 100,200, 300,200, 100);

        // 3. stroke the context
        CGContextStrokePath(context);
    }

### Drawing an UIImage without scaling
    - (void)drawRect:(CGRect)rect {
      // 1. Get UIIMage
      UIImage *myImage = [UIImage imageNamed:@"img.jpg"];

      // 2. Start point is (0,0)
      CGPoint imagePoint = CGPointMake(0, 0);

      // 3. Just add the image at (0,0)
      [myImage drawAtPoint:imagePoint];
    }

### Drawing an UIImage with scaling
    - (void)drawRect:(CGRect)rect {
        // 1. Get UIImage
        UIImage *myImage = [UIImage imageNamed:@"pumpkin.jpg"];

        // 2. Get CGRect dimension for the entire screen
        CGRect imageRect =[[UIScreen mainScreen] bounds];

        // 3. Draw inside the CGRect
        [myImage drawInRect:imageRect];
    }
