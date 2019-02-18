<h2>Swifty Snacks 104: Get Back!</h2>

Hi Snackers, in this episode we are going to play with dismissing the keyboard, using UIGestureRecogniser.

To start, I’ll wait for you to get rid of that pesky Main.storyboard (see 101 for guidance). In AppDelegate, build out the cinema screen (aka window) that our movie will be projected onto. Set a view controller as our cinema screen’s rootViewController.

<img src="Swifty Snacks 104/image1.png">

Now, jump into our view controller to detail and execute blocks for 2 new textFields (step 1). Great, now add our textFields, as subviews, to the controller’s view (step 2). To complete the initial setup, apply AutoLayout constraints to determine the position and size of our textFields inside the bounds of the view controller(step 3).

<img src="Swifty Snacks 104/image2.png">

Run the app. You will be presented with a grey view controller, complete with 2 textFields; namely Text Field ONE & Text Field TWO. Pressing either of these text fields will trigger the keyboard to present itself.

<img src="Swifty Snacks 104/image3.png">

Our task, in this Snack, it to enable the user to dismiss the keyboard using touch.

To detect touch we will use the class UITapGestureRecognizer, as it has been designed to ‘look for single or multiple taps.’ Set the keyword ‘tapRec’ to an instance of this class, then add a target to the same keyword. Now, after the gesture recogniser is added to the view, a user ‘tap’ will call the function specified when setting tapRec’s target, i.e. func handleTouch.

<img src="Swifty Snacks 104/image4.png">

Future Phil says:
Bruh, just add ‘view.endEditing(true)’ in the handleTouch method.

<img src="Swifty Snacks 104/image5.png">

USE ‘view.endEditing(true)’ in place of the following: -

Before proceeding, let’s take a look at our TextView’s in more detail. UITextView is a subclass of UIControl, ‘the base class for controls, which [..] convey specific action or intention in response to user interactions.’ In our app when one of the textFields is pressed, it becomes the firstResponder — ‘first object in a responder chain to receive an event or action message.’ When a UITextField becomes the firstResponder the keyboard is presented for obvious reasons. To dismiss the keyboard, it is necessary for the ‘active’ textField to resign first responder status i.e. resignFirstResponder. Therefore, in our handleTouch method we must identify which textField is currently the first responder, before instructing it to resign first responder status.

<img src="Swifty Snacks 104/image6.png">

Snackers, here’s where our friend, Stack Overflow, enters the scene. Mr Google. please consult with Stack Overflow to find how best to identify the current firstResponder. What’s that you say?

https://stackoverflow.com/questions/5029267/is-there-any-way-of-asking-an-ios-view-which-of-its-children-has-first-responder/14135456#14135456

Thanks Jakob Egger. This UIResponder class extension sends an action to a unspecified target. Importantly, ‘the default implementation [of sendAction]dispatches the action [..] if no target is specified, to the first responder.’ Consequently, the findFirstResponder function is sent to the firstResponder object. In response the firstResponder is set as the _currentFirstResponder variable.

<img src="Swifty Snacks 104/image7.png">

Finally, we can complete the handleTouch function to a) get the current first responder object [UIResponder.currentFirstResponder?], one of our two textFields, and b)instruct it to resign first responder status [.resignFirstResponder()].

<img src="Swifty Snacks 104/image8.png">

The keyboard has been defeated. Hoorah!!!

“I think if you shield yourself from the darkness, you’ll not appreciate — and fully understand — the beauty of life” — Jocko Willink
