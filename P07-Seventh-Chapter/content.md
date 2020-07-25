---
title: Displaying Items Based On Order
slug: displaying-items-in-past-orders
---
Right now our app has two tableviews in a navigation stack that displays the various dates of orders that have been made in the past. What we would like is to be able to click on a date, then see a list of all the items that were bought on that date. 

# Adding Items to the Order 
First thing's first, we need to associate the Item and Order models; let's open the `Order.swift` file.

Within the file, add: `var items: [Item]`

Your Order model should now look like the following: 
```
struct Order {
    var title: String
    var image: UIImage
    var items: [Item]
}
```

# Refactor Order to Display Items 
Let's head to the `PastOrderViewController.swift` file and comment out the `orders` constant we had made in the previous chapter. 

Instead, let's create a new variable for orders and have it be an empty array. 

```
 var orders: [Order] = []
```

## Associating Items by Dates 
Here, we'll be creating a function that will handle the items within the orders. 

Let's create a  `getItems()` function
```
func getItems(){

}
```

Inside the function, let's write out the possible items that can be purchased
```
let robot1 = Item(title: "Respiratory", image: UIImage(named: "robot1")!)
let robot2 = Item(title: "Muscular", image: UIImage(named: "robot2")!)
let robot3 = Item(title: "Endocrine", image: UIImage(named: "robot3")!)
let robot4 = Item(title: "Excretory", image: UIImage(named: "robot4")!)
let robot5 = Item(title: "Lymphatic", image: UIImage(named: "robot5")!)
let robot6 = Item(title: "Nervous", image: UIImage(named: "robot6")!)
```

Below that, let's create the list of Orders and determine which items were bought on which date. Feel free to play around with this part as you'd like. 
```
let ordersList = [Order(title: "July 2020", image: UIImage(named: "box")!, items: [robot1, robot3]),
                Order(title: "June 2020", image: UIImage(named: "box")!, items: [robot2, robot3, robot6]),
                Order(title: "May 2020", image: UIImage(named: "box")!, items: [robot4, robot1]),
                Order(title: "December 2019", image: UIImage(named: "box")!, items: [robot2, robot5, robot6])
]
```

Below the `ordersList`, let's register each of our orders in the ordersList to be in our `orders` variable. 

```
for box in ordersList {
    orders.append(box)
}
```

Remember to call `getItems()` in the `viewDidLoad()` method!

# Viewing Items in Order List 





>[action]
> Let’s commit!
>
\```bash
$ git commit -m “Users can see items from past orders”