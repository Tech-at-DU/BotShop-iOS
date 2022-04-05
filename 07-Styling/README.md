# Styling The App

Currently the app has a bulky design and an oddly X-mas color scheme to it. This is mainly to help you see how various parts come to be during development.

In this section, you will be customizing the app further and making it your own.

## Adding Custom Colors
Having a nice color scheme can do a lot to make your app feel more put together and polished. You can check out websites like:

- [Color Hunt](https://colorhunt.co/)
- [Flat UI Colors](https://flatuicolors.com/)

If you happen to find a color you would really like to use that is not in RGB, you can use various resources to convert the current format into an RGB format:

### HEX to RGB
- [RGB & HEX Conversion Site](https://www.rgbtohex.net/hextorgb/)

### Decimal to RGB
- [RGB & Decimal Conversion Site](https://convertingcolors.com/decimal-color-14277081.html)


After finding a color you'd like to use, take the RGB components of it and input it into Xcode with the following format:

```swift
UIColor(red:0.49, green:0.84, blue:0.87, alpha:1.0)
```

The `UIColor` object generates a color from Red, Green, Blue, and alpha components. The values range from 0.0 to 1.0 for each. This is similar to the CSS `rgba()` color. The rgba color uses values from 0 to 255. 

## Changing Tabbar Color
For instance, if you wanted to change the highlight of the `TabBar` when a user clicks on a `TabBar` icon, you could input a similar line of code into the `viewDidLoad()` of your `TabBarController.swift` file.

```swift
self.tabBar.tintColor = UIColor(red:0.49, green:0.84, blue:0.87, alpha:1.0)
```

## Changing the Background Color
Similarly, we can also change the color of the backgrounds so that each screen has their own background. Feel free to put this information in the `setViews()` methods we created or put it directly into the `viewDidLoad()`

```swift
self.view.backgroundColor = UIColor(red:0.49, green:0.84, blue:0.87, alpha:1.0)
```

## Adding a Custom Font
You can also customize the font within your app! Check out some of the fonts in the following resources and pick at least 1 that you'd like to try implementing into your app.

- [Google Fonts](https://fonts.google.com/)
- [Github iOS Fonts Repo](https://github.com/lionhylra/iOS-UIFont-Names)

In one of your cell files, find where you instantiate one of your labels or buttons. Here, you can customize the text and font in a similar format like the following:

```swift
title.font = UIFont(name: "AvenirNext-Bold", size: 20)
```

> [action]
>
> Go ahead and have fun customizing the app and really making it your own!

<!-- # Feedback and Review - 2 minutes

**We promise this won't take longer than 2 minutes!**

Please take a moment to rate your understanding of the learning outcomes from this tutorial, and how we can improve it via our [tutorial feedback form](https://forms.gle/ajxuqPxeEnW8gNX77)

This allows us to get feedback on how well the students are grasping the learning outcomes, and tells us where we can improve the tutorial experience. -->

# Push to Github

>[action]
> Let’s commit!
>
```
$ git add .
$ git commit -m “Style UI with custom colors and fonts”
```
