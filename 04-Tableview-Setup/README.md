# Users Can See TableView

Right now when the history tab brings us to an empty green page. We want to be able to see a list of dates that show the users past orders. We then want to be able to click on one of the cells and be brought to another page that shows us the list of all the bots that were bought during that order.

# Creating a Custom TableView Cell
Similar to how we built out the `collectionView`, let's first build out a custom `tableViewCell` for our `tableView` to use later on. Each `tableViewCell` will hold a label and image. Create a new file and name it `PastOrderCell.swift`

You will notice many similarities in how we set up the `tableViewCell` from setting up our `collectionViewCell`.

```swift
import Foundation
import UIKit

class PastOrderCell: UITableViewCell{

    let stackView: UIStackView = {
        let stackView = UIStackView()
        stackView.axis = .horizontal
        stackView.spacing = 10
        stackView.translatesAutoresizingMaskIntoConstraints = false
        stackView.distribution = .fill
        return stackView
    }()

    let title: UILabel = {
        let title = UILabel()
        title.font = UIFont(name: "AvenirNext-Bold", size: 20)
        title.textColor = UIColor(red:0.29, green:0.29, blue:0.29, alpha:1.0)
        title.translatesAutoresizingMaskIntoConstraints = false
        return title
    }()

    let itemImage: UIImageView = {
        let image = UIImageView()
        image.translatesAutoresizingMaskIntoConstraints = false
        image.contentMode = .scaleAspectFit
        return image
    }()

    override init(style: UITableViewCell.CellStyle, reuseIdentifier: String?){
        super.init(style: style, reuseIdentifier: reuseIdentifier)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

}
```

We have a title and image within a `stackView`, just like how we set it up in the `collectionView`, only this stack view has a horizontal axis instead of a vertical one.

## Constraining Title and Image to StackView

As always we should create a setup function to constrain all our elements into place. Let's put this after the `override init` method.

```swift
func setup() {

    contentView.addSubview(stackView)

    stackView.widthAnchor.constraint(equalTo: contentView.widthAnchor, multiplier: 0.85).isActive = true
    stackView.heightAnchor.constraint(equalTo: contentView.heightAnchor, multiplier: 0.75).isActive = true
    stackView.centerXAnchor.constraint(equalTo: contentView.centerXAnchor).isActive = true
    stackView.centerYAnchor.constraint(equalTo: contentView.centerYAnchor).isActive = true

    stackView.addArrangedSubview(itemImage)
    itemImage.widthAnchor.constraint(equalTo: stackView.widthAnchor, multiplier: 0.25).isActive = true

    stackView.addArrangedSubview(title)
    title.widthAnchor.constraint(equalTo: stackView.widthAnchor, multiplier: 0.55).isActive = true
}
```

Again, remember to call `setup()` in `override init` method or it won't be run!

Now that we have the custom `tableViewCell` setup, let's create the `tableView` that will hold the cells.

# Building Out The TableView
Navigate back to the `PastOrderViewController` file and instantiate a `UITableView` object.

```swift
let tableView =  UITableView()
```

Then, register the custom cell we just made inside the `viewDidLoad()`

```swift
tableView.register(PastOrderCell.self, forCellReuseIdentifier: "cell")
```

Now outside of the class, create an extension to the `PastOrderViewController` for the `UITableViewDataSource` and `UITableViewDelegate`.

Go ahead and click "fix" to add protocol stubs, just like we did when setting up the collectionView in the previous chapter.

For now, we will have `numberOfRowsInSection` have a return value of 10.

In `cellForRowAt` let's register our custom `tableView` cell and set it up as the cell in the `tableView`.

```swift
let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! PastOrderCell
    cell.accessoryType = .disclosureIndicator
    cell.selectionStyle = .none
return cell
```

Once again we need to set the delegate and dataSource in the `viewDidLoad()` method.

```swift
tableView.delegate = self
tableView.dataSource = self
```

## Constraining TableView
Let's also create a function to set up the view for this page. This function will constrain the `tableView` to our screen.

```swift
func setUpTableView(){
    view.addSubview(tableView)
    tableView.translatesAutoresizingMaskIntoConstraints = false
    tableView.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor).isActive = true
    tableView.leftAnchor.constraint(equalTo: view.leftAnchor).isActive = true
    tableView.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor).isActive = true
    tableView.rightAnchor.constraint(equalTo: view.rightAnchor).isActive = true
```

Remember to call `setUpTableView()` in the `viewDidLoad()` method.

Your file should now look like the following:

```swift
import Foundation
import UIKit

class PastOrderViewController: UIViewController {

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

extension PastOrderViewController: UITableViewDataSource, UITableViewDelegate {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return 10
    }

    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath) as! PastOrderCell
            cell.accessoryType = .disclosureIndicator
            cell.selectionStyle = .none
        return cell
    }


}
```

If you run the app now, you will see an empty `tableView` under the history tab. Currently there is no information in the `tableView` cells and nothing happens when you click on a cell.

What we would like is for there to be a box image and a date listed; then we want to be able to click on a cell and see a list of all the items the user bought on that date.

# Push to Github

>[action]
> Let’s commit!
>
```
$ git add .
$ git commit -m “Build out basic table view”
```
