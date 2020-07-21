---
title: "Understanding What We're Building"
slug: ui-break-down
---

# Project Breakdown
Before we jump into Xcode, let's take a closer look at what we’ll be building page by page.  

## New Order Page 
<img src="assets/new-screen.png" width="300">  

The New Order page is made up of a collection view and shows the items that can be purchased. Each cell in the collection view is a custom cell that includes an image and label within a vertical stackview. 

## Past Order Page
<img src="assets/history-screen.png" width="300"> 

The Past Order page is a table view that displays dates of orders made in the past. Each cell in the table view is a custom cell that includes an image and label within a horizontal stackview.

## Items List Page
<img src="assets/order-list-screen.png" width="300">

The Items List page is a table view that displays the individual items bought on a specific date. Users can get to this page by clicking on a table view cell from the Past Order page. The cells on this table view will not be clickable.

# Different Types of Navigation

## Stack Navigation 

<img src="assets/stack_navigation.png" width="300">

The transition from the Past Order page to the Items List page illustrates a **stack navigation**. 

By selecting an item in the view controller, it pushes a new view controller onscreen using an animation, thereby hiding the previous view controller. Tapping the back button in the navigation bar at the top of the interface removes the top view controller, thereby revealing the view controller underneath.

## Tabbar 

 <img src="assets/tabbar.png" width="300">

 The transition from New Order page to Past Order page illustrates navigation from thr tabbar. A user must click on a tabbar icon in order to navigate between pages. 

Tab bar controller’s views are embedded (using the inherited view property) in the app window. The tab bar controller automatically selects that view controller and displays its contents, resizing them as needed to fit the tab bar interface. 

For our project, we will have two icons on the tabbar but you can have at most is 5 icons displayed on the tabbar at a time. When you add a sixth you get the first four icons plus a <em>More</em> tab with the other two.

> [action]
> Can you think of 2 different kinds of scenarios where it might be better to use stack navigation over tabbar and vice versa? 
