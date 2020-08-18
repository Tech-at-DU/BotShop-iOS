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

Since we also had the `orders` specified in `OrderList.swift`, be sure to comment it out there as well. 

Instead, let's create a new variable for orders and have it be an empty array. 

```
 var orders: [Order] = []
```

## Associating Items by Dates 
Here, we'll be creating a function that will handle the items within the orders. Place this after the `setUpTableView()` method.

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

Locate the `cellForRowAt` function in the `PastOrderViewController` file and add the following line of code to display the dates in the Past Order Page:

```
cell.textLabel?.text = "\(indexPath.row) \(orders[indexPath.row].title)"
```

Now, we will utilize the `setBoxContents` helper function we created earlier in the `PastOrderCell` file to set the information we created, into their designated cells. 

```
cell.setBoxContents(box: orders[indexPath.row])
```

With the information in the cells set, all that's left to do is to display the information after a user selects a date to view from. 

In the `didSelectRowAt` method, update it to the following:

```
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    print("selected!")
    let nextVC: OrderList = OrderList()
    nextVC.currentOrder = orders[indexPath.row]
    self.navigationController?.pushViewController(nextVC, animated: true)
}
```

## More Errors 

You should now have an error that says:

```
Value of type 'OrderList' has no member 'currentOrder'
```

Let's go to the `OrderList.swift file` and add this towards the top of the class: 

```
var currentOrder: Order!
```

# Updating Order List to Display Items Instead of Dates 

In the `OrderList.swift` file, you should have two errors saying 'orders' is undefined. This is because we moved the orders array earlier. 

At the top of the class create an array to old the items: 

```
var orderItems: [Item] = []
```

Now in the `numberOfRowsInSection` in the extension, we can update the information to display:

```
return currentOrder.items.count
```

And we can update the `cellForRowAt` to be: 

```
let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! PastOrderCell
cell.setCellContents(item: currentOrder.items[indexPath.row])
cell.accessoryType = .disclosureIndicator
cell.selectionStyle = .none
return cell
```

The OrderList extension should now look like the following: 

```
extension OrderList: UITableViewDataSource, UITableViewDelegate {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return currentOrder.items.count
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! PastOrderCell
            cell.accessoryType = .disclosureIndicator
            cell.selectionStyle = .none
            cell.setCellContents(item: orderItems[indexPath.row])
        return cell
    }
    
    func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return 100.0
    }
    
}
```



# Push to Github

>[action]
> Let’s commit!
>
```
$ git add .
$ git commit -m “Users can see items from past orders”
```