LHSlideBar
==========

LHSlideBar is a side bar slide in navigation for iOS. Currently it works just for the iPhone in portrait but I am planning to adapt it to landscape and the iPad soon.

To use LHSlideBar add the following files into your project:
- LHSlideBarController.h
- LHSlideBarController.m
- LHTableViewController.h
- LHTableViewController.m

**Note:** You also must include the "QuartzCore" framework into your project.

LHSlideBar requires **iOS 6**+ to work and uses ARC.

### Implementing LHSlideBar

After adding the relevent files into your project (listed above) you create a new instance of LHSlideBar using the `- (id)initWithViewControllers:(NSArray *)viewControllers` call. With this you need an array of view controllers you want to display with the controller to be passed as the `viewControllers` variable.

If you set this as `nil` or just use `- (id)init` you can use the `- (void)setViewControllers:(NSArray *)viewControllers` call to set or update you view controllers at a later date. ***Note:*** When you update the view controllers for a slide bar then the first view controller in the array will automatically be swapped to.

Below is some example code for setting up LHSlideBar:

```
ViewControllerOne *vcOne = [[ViewControllerOne alloc] initWithNibName:@"ViewControllerOne" bundle:nil];
ViewControllerTwo *vcTwo = [[ViewControllerTwo alloc] initWithNibName:@"ViewControllerTwo" bundle:nil];
ViewControllerThree *vcThree = [[ViewControllerThree alloc] initWithNibName:@"ViewControllerThree" bundle:nil];

NSArray *viewControllers = @[vcOne, vcTwo, vcThree];
_slideBarController = [[LHSlideBarController alloc] initWithViewControllers:viewControllers];
```
Then, just add _slideBarController to you view hierarchy. It can be treated like a `UINavigationController` or `UITabBarController` as it is a subclass of `UIViewController`.

### Swapping View Controllers

To swap a view controller in your defined viewControllers array ether call:
```
- (void)swapViewControllerAtIndex:(NSUInteger)index
                 inSlideBarHolder:(UIView *)slideBarHolder
                         animated:(BOOL)animated
```
-or-
```
- (void)swapViewController:(UIViewController *)viewController
          inSlideBarHolder:(UIView *)slideBarHolder
                  animated:(BOOL)animated
```

Make sure that the `viewController` is not nil along with the `viewController` that will be found by the index. If this happens then the method will not do anything, as it needs a view controller to swap to.

### Opening the SlideBar

To open the slide bar you need to call:
```
- (void)showLeftSlideBar:(id)sender
```

This call can be made from any view controller that imports LHSlideBarController with `#import "LHSlideBarController.h"`. You can then call the previous method with the following code from a button press:

```
- (IBAction)slideBarButtonPressed:(id)sender
{
    [[self slideBarController] showLeftSlideBar:sender];
}
```

### LHSlideBar Variables

LHSlideBar has some pre-set variables for slide animation time, fade out alpha and scale down amount. These dont have to be changed, though if you want to you can.

***`@property (assign, nonatomic) CGFloat slideBarOffset`***  
Size of the space on the side of the slide bar when it is open.

***`@property (assign, nonatomic) CGFloat scaleAmount`***  
Scale of the current view controller. 0.0 to 1.0 - 1.0 being 100%

***`@property (assign, nonatomic) CGFloat fadeOutAlpha`***  
Alpha of the fade out gradient in the slideBarOffset space. 0.0 to 1.0

***`@property (assign, readonly, nonatomic) CGFloat animTime`***  
Maximum time for the slide bar animation to slide in or out. Minimum of 0.1s

### LHTableViewController

LHTableViewController shows a table in the slide bar to allow selecting which vuew controller you want to use. All the control rows are displayed in section 0. (Future plans are to make this calss subclass-able to allow customisation and addition of information in the other sections of the table.)
