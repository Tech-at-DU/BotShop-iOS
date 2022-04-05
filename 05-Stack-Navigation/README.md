# Populating TableView and Creating Stack Navigation

In this section we will be building out another kind of navigation type on top of the `TabBar` navigation we already have built out. **Stack navigation** is something you're most likely already familiar with, it's what comes builtin with storyboard's Navigation Controller. To illustrate, let's take a look at this diagram.

![Stack Navigation Img](../assets/stack-nav.png "Stack Navigation Diagram")

A navigation controller object manages its child view controllers using an ordered array, known as the **navigation stack**. The first view controller acts as the parent or root view controller to the subsequent view controllers.

What we'll be doing moving forward is setting our History page as the root controller in this stack navigation and then creating a Order List page that will be the child to the history page, meaning users will only be able to access it through the History page.


# Creating Order Model
Let's create a model for the past orders. Create a new Swift file and name it `Order.swift`.

Within the file, add:

```swift
import Foundation
import UIKit

struct Order {
    var title: String
    var image: UIImage
}
```

# Adding Some Style to the TableView
Now let's head back to our `PastOrderViewController` file.

If you run your app now, you will notice that there is not a lot of room in our `tableViewCell` to display all the information we'd like to display.

In order to give us a bit more room to work with, let's increase the height of each `tableViewCell`. Add this to the bottom of your extension:

```swift
func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
    return 100.0
}
```
If you run the app again, you’ll see that the `tableViewCell` are now taller than before.

# Implementing Stack Navigation
Now that we have more room to work with, let's go forward with utilizing our `Order` model to create objects to fill our cells with.

Place this towards the top of your `PastOrderViewController.swift` file.

```swift
let orders = [
    Order(title: "July 2020", image: UIImage(named: "box")!),
    Order(title: "June 2020", image: UIImage(named: "box")!),
    Order(title: "May 2020", image: UIImage(named: "box")!),
    Order(title: "December 2019", image: UIImage(named: "box")!),
    Order(title: "November 2019", image: UIImage(named: "box")!),
    Order(title: "October 2019", image: UIImage(named: "box")!),
    Order(title: "September 2019", image: UIImage(named: "box")!)]
```

Back to our `PastOrderCell.swift` file we need a couple of helper function to help us connect the pieces together, just as we did in our `collectionView`.

Add these two helper methods after the `setup()` method.

```swift

func setCellContents(item: Order){
    itemImage.image = item.image
    title.text = item.title
}

func setBoxContents(box: Order){
    textLabel?.text = box.title
    imageView?.image = box.image
}
```

Now going back to our `PastOrderViewController`

In our `cellForRowAt` function, we want to add:

```swift       
cell.setCellContents(item: orders[indexPath.row])
```

This piece of codes makes it possible to set the objects in our orders array into the tableview cells.

We will also want to update the `numberOfRowsInSection`  to:

```swift
return orders.count
```

If you run the app now you should see a list of past orders under the history tab. If you click on the cells of the table, you’ll notice that nothing happens. This is because we haven’t implemented a `didSelectRowAt()` method. This builtin function allows the tableview capabilities and actions to happen when a user clicks on a tableview cell.

For now, your extension should look like the following:

```swift
extension PastOrderViewController: UITableViewDataSource, UITableViewDelegate {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return orders.count
    }

    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! PastOrderCell
            cell.accessoryType = .disclosureIndicator
            cell.selectionStyle = .none
            cell.setBoxContents(box: orders[indexPath.row])
        return cell
    }

    func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return 100.0
    }

}
```

Before we’re able to do this, we will need to create a new page to hold the list of items depending on which past order the user would like to view.

# Creating Order List Page to See Items Bought in the Past

Create a new swift file and name it `OrderList.swift`

For now, let's use the information from `PastOrderViewController` and copy it into the `OrderList.swift` file and change the name of the class and extension to `Orderlist`. This is so that we can immediately implement and see the stack navigation between the two pages.

The `OrderList` file should now look like the following:

```swift
import Foundation
import UIKit

class OrderList: UIViewController {

    let orders = [
        Order(title: "July 2020", image: UIImage(named: "box")!),
        Order(title: "June 2020", image: UIImage(named: "box")!),
        Order(title: "May 2020", image: UIImage(named: "box")!),
        Order(title: "December 2019", image: UIImage(named: "box")!),
        Order(title: "November 2019", image: UIImage(named: "box")!),
        Order(title: "October 2019", image: UIImage(named: "box")!),
        Order(title: "September 2019", image: UIImage(named: "box")!)
    ]

    let tableView =  UITableView()

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        view.backgroundColor = .green
        tableView.register(PastOrderCell.self, forCellReuseIdentifier: "cell")
        tableView.delegate = self
        tableView.dataSource = self
        setUpTableView()
    }

    func setUpTableView(){
        view.addSubview(tableView)
        tableView.translatesAutoresizingMaskIntoConstraints = false
        tableView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor).isActive = true
        tableView.leftAnchor.constraint(equalTo: view.leftAnchor).isActive = true
        tableView.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor).isActive = true
        tableView.rightAnchor.constraint(equalTo: view.rightAnchor).isActive = true
    }

}

extension OrderList: UITableViewDataSource, UITableViewDelegate {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return orders.count
    }

    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! PastOrderCell
        cell.accessoryType = .disclosureIndicator
        cell.selectionStyle = .none
        cell.setBoxContents(box: orders[indexPath.row])
        return cell
    }

    func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        return 100.0
    }

}
```

Now let's go back to the `PastOrderViewController` file and add this to the bottom of the extension:

```swift
func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
    print("selected!")
    let nextVC: OrderList = OrderList()
    self.navigationController?.pushViewController(nextVC, animated: true)
}
```

If you run your app now and head to the history tab, you’ll notice that you’re now able to click on a `tableViewCell` and it will take you to a new `tableView`.

Something else you might have noticed is the _back button that magically appeared in the navigation controller._

This is a built-in feature that is given when you use stack navigation in programming and was given to you through this line:

```swift
self.navigationController?.pushViewController(nextVC, animated: true)
```

Having stack navigation is great, but as it sits right now it might not be as useful as we’d like it to be since it’s repetitive information. Let's backtrack and update this new `tableView` to include a list of items instead of another list of orders within a list of orders.

Oof, see, if it’s this hard to wrap your mind around then it definitely needs fixing!

# Push to Github

>[action]
> Let’s commit!
>
```
$ git add .
$ git commit -m “Implement stack navigation”
```

# Continue to the next section

- [06-Displaying-Cell-Data](../06-Displaying-Cell-Data/README.md)
