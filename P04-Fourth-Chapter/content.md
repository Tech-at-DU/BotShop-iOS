---
title: Users Can See Items For Sale
slug: collection-view-implementation
---
In this section we will be creating custom cells to populate the collection view with in order to display the items for sale in the New Order page. 

# Creating Custom Cells for the Collection View 
 Each cell will hold a single item for display. `Click cmd + N` and create a new swift file called `NewItemCell`.

 ```
import Foundation
import UIKit
 
class NewItemCell: UICollectionViewCell {
  
}
```

# Creating the Collection View to Hold Items 

Navigate to the `NewOrderViewController.swift`

The first thing we want to do is set up a collection view that will display all the available items to the users. 

To do this, lets instantiate a UICollectionView object in a view controller

```
var collectionView : UICollectionView!
```

Then let's set the dataSource and delegate of the collection view in the `viewDidLoad()` method. 

```
collectionView.dataSource = self
collectionView.delegate = self
```

Let's also create a function to set up the view for this page. This function will constrain the collectionView to our screen. 

```
func setViews(){

    self.view.addSubview(collectionView)
    collectionView.widthAnchor.constraint(equalTo: self.view.layoutMarginsGuide.widthAnchor, multiplier: 1.0).isActive = true
    collectionView.heightAnchor.constraint(equalTo: self.view.layoutMarginsGuide.heightAnchor, multiplier: 1.0).isActive = true
    collectionView.centerXAnchor.constraint(equalTo: self.view.centerXAnchor).isActive = true
    collectionView.centerYAnchor.constraint(equalTo: self.view.layoutMarginsGuide.centerYAnchor).isActive = true

}
```

Remember to call `setViews()` in the `viewDidLoad()` method. 

# Visualizing the Collection View 
Inside the `viewDidLoad()`, register the custom cell we just created.

```
collectionView.register(NewItemCell.self, forCellWithReuseIdentifier: "cell")
```

Outside of the `NewOrderViewController` Class, create an extension to instantiate `UICollectionViewDataSource`, `UICollectionViewDelegate` in the `NewOrderViewController`. 

You will get an error that says this does not conform the the protocol `UICollectionViewDataSource`. 

Go ahead and click the fix button. 

You should now see collectionView functions for  `numberOfItemsInSection` and `cellForItemAt`. 
The `numberOfItemsInSection` tells the collection view how many items you want to show in its grid.

For now let's  `return 10` items

The `cellForItemAt` returns an object of type `UICollectionViewCell`. This is where you set up the cells with your customCell. 

Lets register our custom cell within `cellForItemAt`. Since we haven’t done anything in our custom cell file yet, then give it a basic color for now so that we are able to see it and make sure everything is working properly. 

```
let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "cell", for: indexPath) as! NewItemCell
cell.backgroundColor = .green
return cell
```

Run the app now. 

You should see 10 green squares in your New Order page.

The items are very small and leave a lot to be desired.
 
What we can do is add more functionality to the collectionView. We want to change the size of each of the items to be larger and make the most of our collectionView so that there isn’t as much negative or empty space. 

Add this to the bottom of your extension: 

```
func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
    return CGSize(width: collectionView.frame.width/2.2, height: collectionView.frame.height/3)
}
```

Run the app again and you’ll see that green squares are larger and filling up more space. 

We’re now a step closer to what we’d like our collection view to look like! Great work! 

# Push to Github

>[action]
> Let’s commit!
>
```
$ git add .
$ git commit -m “Set up basic collection view”
```


# Adding Details to Collection View Cells 
It’s great that we have our green squares, we’re proud they exist. But they’ve done their jobs and now it’s time for us to improve these green squares to showcase our lovely robots! 

## Creating Item Model 
Let's start by creating a model for our items. 
Click 'cmd + N' and create a new swift file called `Item`.

Inside `Item.swift` add the following: 

```
struct Item{
    var title: String
    var image: UIImage
}
```

## Setting Up Inside of Custom Cell 
Let's go back to our `NewItemCell` file and set up the elements that will make up our cell. 

Within the cell, we will have an image and a title vertically stacked together. Let's go ahead and instantiate our stackview, image, and title. 

```
let stackView: UIStackView = {
    let stackView = UIStackView()
    stackView.axis = .vertical
    stackView.spacing = 20
    stackView.translatesAutoresizingMaskIntoConstraints = false
    stackView.distribution = .fill
    return stackView
}()

let image: UIImageView = {
    let image = UIImageView()
    image.translatesAutoresizingMaskIntoConstraints = false
    image.contentMode = .scaleAspectFit
    return image
}()

let title: UILabel = {
    let title = UILabel()
    title.translatesAutoresizingMaskIntoConstraints = false
    title.textColor = .white
    title.font = UIFont(name: "AvenirNext-Bold", size: 20)
    title.textAlignment = .center
    title.text = "testing"
    return title
}()
```

## Adding Constraints
Similar to what we did when setting up the collection view, let's create another setup method in the `NewItemCell` file to arrange the image and title within the stackview of the cell. 

```
func setup() {
    contentView.addSubview(stackView)
    
    stackView.widthAnchor.constraint(equalTo: contentView.widthAnchor, multiplier: 0.80).isActive = true
    stackView.heightAnchor.constraint(equalTo: contentView.heightAnchor, multiplier: 0.70).isActive = true
    stackView.centerXAnchor.constraint(equalTo: contentView.centerXAnchor).isActive = true
    stackView.centerYAnchor.constraint(equalTo: contentView.centerYAnchor).isActive = true
    
    stackView.addArrangedSubview(image)
    image.heightAnchor.constraint(equalTo: stackView.heightAnchor, multiplier: 0.55).isActive = true
    
    stackView.addArrangedSubview(title)
}
```
Remember to call `setup()` within the `init` method of the cell file!

At the bottom of your class include the `required init` if you haven't already: 

```
required init?(coder: NSCoder) {
    fatalError("init(coder:) has not been implemented")
}
```

If you run the app now, you’ll see “testing” is written in all of your cells. You might be wondering where the images are.

# Displaying Item Images in Custom Cells 
Let's start this by going back to the `NewOrderViewController` and creating an array of items that utilizes out `Item` model to specify the title and image. 

```
let data = [
    Item(title: "Respiratory", image: UIImage(named: "robot1")!),
    Item(title: "Muscular", image: UIImage(named: "robot2")!),
    Item(title: "Endocrine", image: UIImage(named: "robot3")!),
    Item(title: "Excretory", image: UIImage(named: "robot4")!),
    Item(title: "Lymphatic", image: UIImage(named: "robot5")!),
    Item(title: "Nervous", image: UIImage(named: "robot6")!)
]
```

Let’s update our collectionView with our new data. 

Update `numberOfItemsInSection` to:

```
return data.count
```

Then in `cellForItemAt`, specify the cell data after the background color declaration: 

```
cell.data = self.data[indexPath.row]
```

As you can see we have an error saying `NewItemCell` has no member, `data`. This is because we haven’t set up a way for the data array to be able to get implemented into the custom cell we made earlier. 

Let's fix this by going to the `NewItemCell` file and adding the following:

```
var data: Item? {
    didSet{
        guard let data = data else { return }
        image.image = data.image
        title.text = data.title
    }
}
```

If you run the app now you should see the robot images and their proper names displayed in the collectionvVew. 

# Push to Github

>[action]
> Let’s commit!
>
```
$ git add .
$ git commit -m “Users can see items for sale in collection view” 
```