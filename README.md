# javascript-parallax

javascript-parallax

Added boilerplate for html, css and js
Added images for parallax backgrounds
Initialize canvas, context, height and width in js (default setting)
Initialize gameSpeed to 5
Initialize the images to represent each layer of the parallax background using new Image() (similar to document.createElement("img"))
Create animate function
Add default ctx.clearRect(0, 0, width, height) to clear canvas after each animation frame to prevent smudging
Add drawImage function to animate with the backgroundLayer as 1 of the image parameter (remember there is 4-9 parameters depending on how much control you want)
requestAnimationFrame(animate) at the end of animate function and call it to begin animating
Initialize variable x to 0 and replace it with the hardcoded 0 at destination x coordinate in drawImage
x -= gameSpeed to move the animation to the left according to gameSpeed value;
Set a condition where if x is less than the number of pixels of the background layer(because it is moving to the left), bring it back to 0
Setting the if condition to x less than the pixels of the background layer(in this case 2400px) and setting x to 2400 will allow it to show the full width of 2400px and another 2400px of empty space
To solve this, you need to put the same image into that 2400px of empty space so that it endlessly loop
Create a second variable x2 to represent the duplicate of the same image layer and set it to 2400
Duplicate the drawImage function inside animate and replacing destination x with x2 in the duplicate
Create the same condition below your original x if condition but replace x with x2
There is gap between the 2 images scrolling to the left as they are resetting independent of each other
This is due to the gameSpeed variable which x and x2 uses and there is a remainder in the value when it deducts from the last pixels
You can hardcode gameSpeed to a number which can be divisible by the total pixels but that is not dynamic(considering this is a game and you want the speed to be slower and faster at different areas)
To prevent the gap, you can offset the condition by deducting the gameSpeed AND adding the value of the position of the other image to account for the gap
In this case, if (x < -2400) x = 2400 + x2 - gameSpeed and vice versa for x2
All of the above is to show the logic in creating the parallax effect
You can refactor them by using javascript built in methods such as objects instead of hardcoded variables
Remove x, x2, drawImage functions and the all the conditions leaving only clearRect and requestAnimationFrame intact
Create a class called Layer which will act as a blueprint when you pass values and properties inside the constructor inside Layer
The constructor will have 2 parameters called image and speedModifier
Inside the constructor, you will use the this keyword to invoke the key value pairs of x, y at 0 for the first image and the width and height for the first image when called
Create a x2 key value pair setting the value equals to the width of the image to represent the duplicate
Assign this.image and this.speedModifier to the parameters you created which will pass the arguments to image and speedModifier whenever you invoke the constructor method inside Layer
Assign this.speed to the global variable gameSpeed multiplied by this.speedModifier
Create an update function after the constructor which will reset the image when the image moves offscreen (similar to the if conditions that you previously did), only this time you can do it for all 5 layers
Create a draw function after update function to redraw after update runs
Place this.speed = gameSpeed multiplied by this.speedModifier inside update to dynamically update game speed
To reset images, recreate the previous if condition inside update function this time with this keyword using the values from the constructor
Do the same for x2 variable
If the images have not reset yet, do the same x = x - gameSpeed(which is x -= gameSpeed) as before only with this keyword and using Math.floor to remove decimal places
In the draw function, add back the drawImage function you did previously only this time with the properties used in the constructor for x and x2
You use 5 parameters this time because the width and height is inside the constructor along with image, dx and dy
The Layer class is complete and to test it create a new constant variable for one of the layers (layer4 for example) and assign new Layer() to it (es6 feature to call the class method)
Pass the corresponding background layer variable and the desired speedModifier numeral to new Layer()
Call layer4.update and layer4.draw inside animate to test the animation
Once the above works, you can now create new constant variables for each layer
To prevent repetition of calling each layer of update and draw inside the animate function, create a new variable called gameObjects assigning it to an array of the newly created layer1 to 5 variables as array items
Remove the manual calls from the animate function and create a forEach function for gameObjects and call them inside the function instead
Change the values of speedModifier in each layer, ascending in this case, to create a parallax effect
From this point on, it is all quality of life changes for users or to refactor
Create a new div with id container inside body element, with a p element that has a span element of id showGameSpeed
Create input element below p element with type of range, min, maxm value, class and id of slider attributes;
Place canvas inside of div at the top
Style container with absolute positioning and canvas to relative with the same width and height
Center container with top left transform translate
Slider is set to 100%
Initialize slider variable in js linking it to the slider id in html
Assign slider.value to gameSpeed
Initialize showGameSpeed and link it to showGameSpeed span id in html
Create event listener for slider to listen for change whenever the target value of the event(in this case the slider) changes
Assign gameSpeed to the event's target value inside the event listener and do the same for showGameSpeed text content
//TODO refactor x and x2 to a single variable x
