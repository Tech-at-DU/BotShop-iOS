---
title: "Creating Layout"
slug: layout-setup
---

# Creating Basic New Order Page 
Go to the ViewController.swift file that came with your project setup. Right click on the file and click <em>Rename</em> and change the class from ```ViewController``` to ```NewOrderViewController```. You will also need to change the name of the class inside of that file from ```class ViewController``` to ```class NewOrderViewController```.

Run the app again and make sure you’re still able to see the red screen. We will return to this page again later on. 

# Creating Basic Past Order Page 

Create a new swift file and name it ```PastOrderViewController```. Add ```PastOrderViewController``` and add ```viewDidLoad()``. Then let's set the background color as green.


> [solution]
> See if you can remember how to add a new file to your project and set the background color to green. 
>
```
To add a new file: 
Cmd + N > Swift file > Name it: "PastOrderViewController" 

Your file should now look like this: 

class PastOrderViewController: UIViewController {
 
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        view.backgroundColor = .green 
    }
 
}
```
If you run your app now you’ll notice that there is no way for you to get to your Past Order page to see if it is green or not. We can fix this navigational nightmare by creating a tab bar for your app. 
