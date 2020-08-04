---
title: "Navigating Between Pages With Tabbar"
slug: navigating-between-pages
---

In this section we will be incorporating agile development by setting up all the pages all at once and building out the navigation between pages in the app. 

That might sound intimidating at first but what we'll be doing is just having more colored pages like we did for the red screen last chapter. We simply just want to build things out for the sole purpose to make sure they exist and that we're able to navigate between the screens. From there, we will build upon our project layer by layer until you have a functional app. 

Excited? Let's get to it! 

# Displaying the New Order Page
Let's start by building out the New Order page, the first page a user will see when opening the app. 

Locate the `ViewController` file that came with your project setup, this is the same page with the red screen from last chapter. 

Inside that file, rename the `class ViewController` to `NewOrderViewController`.

Make sure you change the name in the left hand pane from `ViewController.swift` to `NewOrderViewController.swift`.

Run the app again and make sure you’re still able to see the red screen. We will return to this page again later and add more styling to it. 

# Displaying the Past Order Page
Create a new swift file and name it `PastOrderViewController`, setup its class within the file and give the view a background color of green. 

The file should now look like the following: 

```
import Foundation
import UIKit

class PastOrderViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        view.backgroundColor = .green
    }

}
```

If you run your app now you’ll notice that there is no way for you to get to the Past Order page to see if it is green or not. We can fix this navigational nightmare by creating a tab bar for your app. 

# Creating the TabBarController
Create a new swift file and name it `TabBarController`, setup the `TabBarController` class to be of type `UITabBarController` and have it conform to the `UITabBarControllerDelegate` protocol. 

Your file should now look like the following: 

```
import Foundation
import UIKit

class TabBarController: UITabBarController, UITabBarControllerDelegate{
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    
}
```

Because we’re using a delegate you will want to add this line into ``viewDidLoad()` to allow the object to be its own delegate.

```
self.delegate = self
```

This sets default delegate functionality in your controller. Delegates in general are a design pattern that allows one object to send messages to another object when a specific event happens.

# Creating Custom Tabbar Icons 
Next we will set up the icons in the tabbar. These icons can technically be any images you'd like, feel free to have fun and explore setting images as the icons later on. For the time being, we have included images in the project assets that you transfered over into the assets folder from the previous chapter. 

To get started we will need two buttons in order to navigate between our two pages. To do this, first we need to declare two variables of type `UIImageView` at the top of our  `TabBarController` class.

```
var firstItemImageView: UIImageView!
var secondItemImageView: UIImageView!
```

Then we want to create a function to set up the tab bar icons. This function takes the UIImageViews we have and adds them as subviews in the tab bar, placing our icons within it. 

Place this block of code after the `viewDidLoad()`.

```
func setupTabBarIcons(){
    
    let firstItemView = self.tabBar.subviews[0]
    let secondItemView = self.tabBar.subviews[1]
    
    self.firstItemImageView = (firstItemView.subviews.first as! UIImageView)
    self.firstItemImageView.contentMode = .center
    
    self.secondItemImageView = (secondItemView.subviews.first as! UIImageView)
    self.secondItemImageView.contentMode = .center
}
```

# Setting Up View Controllers within the Tabbar 
This is where we set up the view controllers and their assigned icons to be placed in the tabbar. Place this block of code below the `setupTabBarIcons()` method you just wrote.

```
func setupViewControllers(){       
    
    let newBoxVC = NewOrderViewController()
    let navController1 = UINavigationController(rootViewController:newBoxVC)
    newBoxVC.tabBarItem = UITabBarItem(title: "New", image: UIImage(named: "tab-box"), tag: 0)
    
    let pastBoxesVC = PastOrderViewController()
    let navController2 = UINavigationController(rootViewController:pastBoxesVC)
    pastBoxesVC.tabBarItem = UITabBarItem(title: "History", image: UIImage(named: "tab-history"), tag: 1)
    
    
    viewControllers = [navController1, navController2]

}
```

Finally, let's call both setup functions in the `viewDidLoad()`

```
setupViewControllers()
setupTabBarIcons()
```

Now, let’s run the app! 

# Putting it All Together

## Oops!

After you run the app, you should see an error:

```
"Use of unresolved identifier <em>View Controller</em>" 
```

Don't worry, errors are our friends and every error gives us an opportunity to learn! This error in particular occurred because we changed the file name from 

```
let mainController = ViewController()
```

to 

```
let mainController = NewOrderViewController()
```

Let's follow the error and go to the `SceneDelegate.swift` file and update the name from `View Controller` to `NewOrderViewController` and run the app again. 

What do you see? You might have noticed that after we run the app we are only be able to see the `NewOrderViewController` page. But we're unable to navigate to the Past Order page. Why is that? 

## Launching with TabBar

If you look at the `mainController` constant we created in the beginning of the tutorial within `SceneDelegate`, you'll see that the `mainController` is the first view controller that gets launched. We actually need to change the `mainController` to be the `TabBarController()` in order to give us access to all view controllers within our navigation controller. 

```
let mainController =  TabBarController()
```

Now lets run the app again! 

You should now have a tab bar at the bottom of your simulator and be able to click the tab bar icons to travel between the two pages and see a green screen and a red screen. 

>[action]
>Can you add a few more pages and icons to the tab bar? 
>
> What is the maximum number of icons a tab bar can hold? 


# Push to Github

>[action]
> Lets Save Our Work
>
```
$ git add .
$ git commit -m “Users can navigate between pages using tabbar” 
```


Great progress so far! We now have our navigation setup. Our app still looks a bit lack-luster, let's continue to build out our pages. 



