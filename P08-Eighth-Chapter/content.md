---
title: Styling The App
slug: adding-style
---

# Adding Custom Colors
Having a nice color scheme can do a lot to make your app feel more put together and polished. You can check out websites like: 

- https://colorhunt.co/
- https://flatuicolors.com/

If you happen to find a color you would really like to use that is not in RGB, you can use various resources to convert the current format into an RGB format: 

### HEX to RGB 
- https://www.rgbtohex.net/hextorgb/

### Decimal to RGB 
- https://convertingcolors.com/decimal-color-14277081.html


After finding a color you'd like to use, take the RGB components of it and input it into Xcode with the following format: 
```
UIColor(red:0.49, green:0.84, blue:0.87, alpha:1.0)
```

## Changing Tabbar Color
For instance, if you wanted to change the highlight of the tabbar when a user clicks on a tabbar icon, you could input a similar line of code into the `viewDidLoad()` of your `TabBarController.swift` file. 
```
self.tabBar.tintColor = UIColor(red:0.49, green:0.84, blue:0.87, alpha:1.0)
```

## Changing the Background Color 
Similarly, we can also change the color of the backgrounds so that each screen has their own background. Feel free to put this information in the `setViews()` methods we created or put it directly into the `viewDidLoad()`
```
self.view.backgroundColor = UIColor(red:0.49, green:0.84, blue:0.87, alpha:1.0)
```

# Adding Custom Font 
You can also customize the font within your app! Check out some of the fonts in the following resources and pick at least 1 that you'd like to try implementing into your app.

- https://fonts.google.com/
- https://github.com/lionhylra/iOS-UIFont-Names

In one of your cell files, find where you instantiate one of your labels or buttons. Here, you can customize the text and font in a similar format like the following: 
```
title.font = UIFont(name: "AvenirNext-Bold", size: 20)
```

Go ahead and have fun customizing the app and really making it your own(: 