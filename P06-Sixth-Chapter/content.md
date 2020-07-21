---
title: "Creating Tabbar"
slug: create-tabbar
---
# Creating Tabbar 
Create a new swift file and name it ```TabBarController```. Add ```class TabBarController``` and add ```viewDidLoad()``. TabBarController will be of type UITabBarController and will conform to the UITabBarControllerDelegate protocol. 

Your file should look like the following:
```
import UIKit
 
class TabBarController: UITabBarController, UITabBarControllerDelegate{
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }

}
```
Because we’re using a delegate you will want to implement the protocol by adding this into viewdidload: 

```
self.delegate = self
```

This sets default delegate functionality in your controller. Delegates in general are a design pattern that allows one object to send messages to another object when a specific event happens.

Next we will set up the icons in the tabbar. We will need two buttons in order to navigate between our two pages. To do this, first we need to declare two variables.

```
var firstItemImageView: UIImageView!
var secondItemImageView: UIImageView!
```

Then we want to create a function to set up the tab bar icons. This function takes the UIImageViews we have and adds them as subviews in the tab bar, placing our icons within it. 

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

Lastly we want to set up the viewcontrollers within the tabbar. 

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
Now call both setup functions in your ```viewDidLoad()```

```
setupViewControllers()
setupTabBarIcons()
```

## Testing What We Have So Far 
Now, let’s run the app and see what we have!

You should see an error, “Use of unresolved identifier ```View Controller``` this is because we changed the name to ```NewOrderViewController```. If we update the name in our ```SceneDelegate.swift``` file to ```NewOrderViewController```, after we run the app we will only be able to see the ```NewOrderViewController``` page. But what about our other page? 

### Let's Fix This
Locate the **mainController** constant we created in the beginning of the tutorial within ```SceneDelegate```. Change the mainController to be ```TabBarController()```.

It should look like this: 
'''
let mainController =  TabBarController()
'''

Now lets run the app again! 

You should now have a tabbar at the bottom of your simulator and be able to click the tabbar icons to travel between the two pages and see a green screen and a red screen. 

>[action]
>can you add a few more pages and icons to the tabbar? 
> What is the maximum number of icons a tabbar can hold? 


>[action]
> Let’s commit!
>
\```bash
$ git commit -m “Users can navigate between pages using tabbar” 

Great progress so far! We now have our navigation setup. Our app still looks a bit lack-luster, lets continue to build out our pages. 