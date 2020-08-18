---
title: "Overview Of Bot Shop"
slug: overview-of-bot-shop
---

It’s the year 3000 and the everyday person is now 75% machine and requires the services of microbots for inner bodily maintenance. It’s your job to create an app that enables people to order the bots they need.

As the only iOS developer capable for such an important task, you will have the best equipment and tools available to you to create a 100% programmatic native iOS app using Swift and Xcode. 

# Why Is This Important
Aside from saving billions of people by giving them access to the microbots they need; programmatic Swift iOS applications are an industry standard that allow for more speed, power, and control in the mobile development process. In hand with programmatic iOS development, tab bars are a handy tool that enable users to navigate apps.

> [action]
> Can you think of 3 different mobile apps that use tab bars as their source for in-app navigation? What are some things that all those tab bars have in common? Are there any differences?


# Who Is This For?
iOS beginners who already have some experience with Xcode and are familiar with coding in Swift.

**What You Should Already Know**

You should know how to:

- navigate your way around Xcode
- differentiate between table views and collection views
- organize your code using MVC

Resources can include (but are not limited to):

- Completion of MOB 1.1
- Strong understanding of Swift

**Estimated Completion Time:**

4 hours

# Learning Outcomes

By the end of this tutorial, you should be able to...

1. Create an iOS application programmatically using agile development
2. Setup navigation in the app using tabbar
3. Create tableviews and collectionviews
4. Implement custom fonts and custom tabbar icons
5. Have a better understanding of stacks


>[action]
> Take a moment to write down these learning outcomes and reflect on them. Make sure that as you progress through the tutorial that you're furthering your understanding, and that by the end, you have completed all of the outcomes.

# What We're Building
At the end of this tutorial you will have built your own mobile shopping app!

## New Order Page  
![New Order Screen Img](../assets/new-screen.png "Finished New Order Screen")

The New Order page is made up of a collection view and shows the items that can be purchased. Each cell in the collection view is a custom cell that includes an image and label within a vertical stackview.

## Past Order Page

![Past Order Screen Img](../assets/history-screen.png "Finished Past Order Screen")

The Past Order page is a table view that displays dates of orders made in the past. Each cell in the table view is a custom cell that includes an image and label within a horizontal stackview.

## Items List Page

![Order List Screen Img](../assets/order-list-screen.png "Finished List of Past Orders Screen")

The Items List page is a table view that displays the individual items bought on a specific date. Users can get to this page by clicking on a table view cell from the Past Order page. The cells on this table view will not be clickable.

# Different Types of Navigation

## Stack Navigation

![Stack Navigation Diagram](../assets/stack_navigation.png "Stack Navigation Diagram")


The transition from the Past Order page to the Items List page illustrates a **stack navigation**.

By selecting an item in the view controller, it pushes a new view controller onscreen using an animation, thereby hiding the previous view controller. Tapping the back button in the navigation bar at the top of the interface removes the top view controller, thereby revealing the view controller underneath.

## Tabbar

![Stack Navigation Diagram](../assets/tabbar.png "Stack Navigation Diagram")

The transition from New Order page to Past Order page illustrates navigation from thr tabbar. A user must click on a tabbar icon in order to navigate between pages.

Tab bar controller’s views are embedded (using the inherited view property) in the app window. The tab bar controller automatically selects that view controller and displays its contents, resizing them as needed to fit the tab bar interface.

For our project, we will have two icons on the tabbar but you can have at most is 5 icons displayed on the tabbar at a time. When you add a sixth you get the first four icons plus a <em>More</em> tab with the other two.

> [action]
> Can you think of 2 different kinds of scenarios where it might be better to use stack navigation over tabbar and vice versa?


# User Stories
User stories is a tool used in agile software development to capture a feature or task from the users perspective.

1. As a buyer, I want to see available microbots so that I can purchase the one I need
2. As a buyer, I want to see previous orders of microbots so that I can remember which ones I like and do not like
3. As a buyer, I want to be able to favorite the microbots I like so that I can easily find them next time


# If You Get Stuck
Getting stuck when coding (and debugging) is a natural part of the programming process. If you find yourself stuck on a problem or lost, feel free to take a break, get some water, take a walk, and come back with a fresh mind. Then retrace your steps in the tutorial. Make sure you've follow each step of the tutorial. It's easy to make typos or to accidentally skip over important steps.
