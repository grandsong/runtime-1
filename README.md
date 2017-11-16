Runtime!
=========

Meet Halle, the official Operation Spark robot.

![Halle](http://i.imgur.com/yUKA9EN.gif)

Halle has some cool moves but nobody to play with. Let's build our own game using Halle!

# Step 1 - Getting Started

Install this project into your Cloud9 workspace by typing `opspark install` into a terminal and choosing the `runtime` project.

You can run the game by opening `index.html` and then choosing *Preview*. You should see Halle running on a blank background and you should be able to press the appropriate keys to make her jump and shoot. 

Now go back and look at the `index.html` file in Cloud9. `index.html` is an example of the kind of code you might see in a real-world project. The majority of the code is not in `index.html` itself but is loaded as external scripts. 

```
<script src="js/util/load.js"></script>
<script src="js/util/spin.min.js"></script>
<script src="js/util/point.js"></script>
<script src="js/spritesheet.js"></script>
...
<script src="js/view/ground.js"></script>
<script src="js/player/halle.js"></script>
<script src="js/player/playerManager.js"></script>
<script src="js/opspark.js"></script>
```

The scripts are organized so that each script handles one aspect of the game, with each name describing what they do. Professional developers break code into scripts or modules so that the code is easier to understand and so that many people can work on the code at the same time.

Some of the scripts are *library* or *third-party* code. This is code that other people wrote that we can use to do cool stuff.

```html
<script src="bower_components/easeljs/lib/easeljs-0.8.1.min.js"></script>
<script src="bower_components/PreloadJS/lib/preloadjs-0.6.1.min.js"></script>
<script src="bower_components/TweenJS/lib/tweenjs-0.6.1.min.js"></script>
<script src="bower_components/SoundJS/lib/soundjs-0.6.1.min.js"></script>
<script src="bower_components/opspark-draw/draw.js"></script>
```

For this project, we will be using the [create.js](http://createjs.com/) library to draw and animate our game. 

# Step 2 - Brainstorming

Before we start coding, we have to decide what kind of game we want to build with Halle. Look at the kind of moves that Halle can make and imagine how they would fit into **your** game. 

You will need to decide on a general *theme* for the game. What kind of world is Halle in? Is she in space, in a factory, on the streets of New Orleans? 

What are the *game mechanics*? What are the goals and what are the challenges? What might Halle encounter as the game progresses? Are there points or a score? How does the game end? 

Finally, come up with a good *name* for your game. Having a great name for a project is an important step, but don't worry, you can always change it later. 

# Step 3 - Adding The Heads-Up Display

Most games display *status information* like the current score or number of lives remaining overlaid with the running game at either the top or bottom of the screen. We call this a "Heads-Up Display" and we've already written one for you in `js/view/hud.js`

To include it you will want to add the following script to `index.html` in the `<head>` element underneath the commment that says `<!-- add any additional scripts here -->` 

    <script src="js/view/hud.js"></script>

Find this file in your project and open it. You should see that it declares a function and assigns it to `window.opspark.makeHud`. Read the documentation for `makeHud` and follow it's instructions for adding the heads-up-display to the game. You will want to make a change to the code in `index.html` at `TODO 1`. Once that is done, you should see the heads-up display!

Hint: The code to add will look like this:
    
    var hud = opspark.makeHud();
    view.addChild(hud);

It creates a Heads Up Display (HUD) using the opspark.makeHud() method and adds it to view.

![Heads-Up Display](http://i.imgur.com/VG1KvnA.png)

Now, add one more line of code to `index.html` where you created your heads-up display.

    window.hud = hud;

By assigning the `hud` variable to a property on the `window` object, we can play with it in the console. 

![hud variable in console](http://i.imgur.com/nxwu637.png)

Open up the console in Chrome Developer Tools and type out each of these statements.

Hint: To open the Chrome Developer Tools right click on the page and select 'inspect'

    hud.updateScore(10);

    hud.updateOf(1000);

    hud.setIntegrity(25);

    hud.setIntegrity(100);

    hud.kill();

**What do they do?**

# Step 4 - Adding A Background 

Include the script `js/view/background.js` by adding the following code to the `<head>` element of `index.html`

    <script src="js/view/background.js"></script>

Modify `index.html` at `TODO 2` to call our newly included code. You will need to supply the appropriate arguments to the function. 

```js
var background = opspark.makeBackground(app,ground);
view.addChild(background);
```

Once this is done correctly you should see Halle on a yellow background. 

![Halle On Yellow Background](http://i.imgur.com/iqo5v3F.png)

# TODO
Open up `js/view/background.js`

Adjust the backgroundFill variable to a color you like and then change the second argument so that it only shows the background color above the the ground. 

As a last step, depending on the background you've built, your heads-up-display may be hard to see or just plain ugly. Modify the colors used by `js/view/hud.js` to match your background.

Our first goal is to create a great background for our game. That will require learning to draw with create.js.

# INFO: Drawing With Create.js
All drawing code for the background should go at `TODO: 3` in `js/view/background.js` within the `render()` function. 
In order to draw something you will create a *shape* using one of the following functions:

Image | Code
------|------
![rect](http://i.imgur.com/gwbZLZl.png)    | `var shape = draw.rect(width, height, color, strokeColor, strokeWidth);`
![line](http://i.imgur.com/Zy8nY0C.png)   | `var shape = draw.line(fromX, fromY, toX, toY, strokeColor, strokeWidth);`
![circle](http://i.imgur.com/Zc9hJqU.png)    | `var shape = draw.circle(radius, color, strokeColor, strokeWidth);`
![image](http://i.imgur.com/BGZCnX8.png) `var href='img/moon.png'`    | `var shape = draw.bitmap(href);`

**Adding your own Images**
The moon.png image is stored in the img folder. You can add your own custom images too! Once you have found the image you would like to add (you can easily find png pictures by adding .png to your google image search) you can upload that file to your cloud9 workspace. 
- Go to File -> Upload Local Files -> Select / Drag & Drop downloaded image. 
- Move that image into the img folder
- use 'img/<name of your picture>' for the href

In order to make that shape show on sreen you will need to add that shape to the `background` by calling

    background.addChild(shape);

Your shape will be created so that it appears at the upper-left hand corner of the screen, at `(0,0)` in your game's coordinate system, but you can place a shape anywhere on the screen by setting it's `x` and `y` properties.
    
    shape.x = 100;
    shape.y = 45;

Remember that `x` and `y` refer to a coordinate system which has an origin (0,0) in the upper-left hand corner. `x` becomes larger as you move to the right. `y` becomes larger as you move downward.

![cartesion coordinate system](http://i.imgur.com/jyZuFer.png)

We've defined a couple of variables that should help you draw shapes in the right place.

`canvasWidth` is the total width of the game screen  
`canvasHeight` is the total height of the game screen  
`groundY` is the y coordinate of the ground line  

See the [opspark-draw documentation](https://libraries.io/bower/opspark-draw) for more details on drawing functions you can use or look at the source directly in your project at `bower_components/opspark-draw/draw.js`. You can also use anything in the [create.js API](http://www.createjs.com/docs/easeljs/modules/EaselJS.html).

# Step 5 - Create Your Own Background
All drawing code for the background should go at `TODO: 3` in `js/view/background.js` within the `render()` function. 

Create a great background for your game. With the draw functions provided and your JavaScript knowledge, you can create almost anything.

If you need some inspiration, here are some things to try:

# Star Field

![Star Field](http://i.imgur.com/Vsdw99h.png)

Use a [for loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for) to draw a bunch of objects to the screen. 

```js
var circle;
for(var i=0;i<100;i++) {
    circle = draw.circle(10,'white','LightGray',2);
    circle.x = canvasWidth*Math.random();
    circle.y = canvasHeight*Math.random();
    background.addChild(circle);
}
```

Try changing the code to make the result look more like actual stars.

# Moon

![Moon](http://i.imgur.com/ntD7AfF.png)

You can add images to your background using `draw.bitmap()`

```
var moon = draw.bitmap('img/moon.png');
moon.x = 300;
moon.y = 25;
moon.scaleX = 1.0;
moon.scaleY = 1.0;
background.addChild(moon);
```

Try moving the moon to a good location for your game.

Try changing the size of the moon by changing the moon's `scaleX` and `scaleY` properties


# INFO: Animation

create.js allows us to perform animation in our game. If you look in the upper left-hand corner of the game, you will see something like "57 fps". That means the game is running at 57 frames-per-second. Each "frame" is one drawing of our game and so we are redrawing the game 57 times every second. By making slight changes to what we draw over time we can give the illusion of motion. 

We don't have to completely re-create our game 57 times a second. Instead, we can setup a scene and then make slight modifications to it over time. In `background.js`, the `render()` function sets up our scene and the `update()` function is called once per frame. Whatever changes we make to the scene are drawn on the next frame. 

# Step 6 - Create a box

To illustrate this, let's draw a box on the screen. We will call it `backgroundBox`. In `background.js`, declare a variable `backgroundBox` directly after the `background` variable declaration.

    var backgroundBox;

Then in the `render()` function, store a rectangle in `backgroundBox` and add it to the background

```js
backgroundBox = draw.rect(100,100,'Blue');
backgroundBox.x = 0;
backgroundBox.y = 0;
background.addChild(backgroundBox);
```

You should now see a blue box in your background. Change the values of `backgroundBox.x` and `backgroundBox.y` so that the box appears on the ground in front of Halle.

![Halle and Blue Box](http://i.imgur.com/hDCmj47.png)

# Step 7 - Animating The Box

We can perform animation by making changes to our scene in the `update()` function. Remember that it is called once for each frame of the game.

In the `update()` function, add the following code:

    backgroundBox.x = backgroundBox.x + 1;

You should now see the box moving. What happened? Why is it doing that? Make sure you understand and make sure your partner (if you are pairing) understands as well. 

**Change the code so that the box moves towards Halle**

# INFO: Parallax

![Parallax](http://www.hallme.com/uploads/parallax-scrolling-mario.gif)

Parallax is a technique in animation for giving the illusion of depth. When you are moving, things that are close to you move quickly whereas things that are very far away may move slowly or not appear to move at all. We can use this technique in our game to create visually interesting backgrounds. 

# Step 8 - Creating a Parallax Effect

Try adding the following code to `update()`

```js
if(backgroundBox.x < -100) {
    backgroundBox.x = canvasWidth;
}
```

What is going on here?

We can take this technique one step further by applying it to *many* boxes. 

Go ahead and remove your `backgroundBox` from the screen by commenting out this line of code

    // background.addChild(backgroundBox);

After the declaration of `backgroundBox` declare a variable `buildings` and assign it an empty array.

    var buildings = [];

In `render()` create several boxes using a `for` loop and add them to `buildings` array. 

```js
var buildingHeight = 300;
var building;
for(var i=0;i<5;++i) {
    building = draw.rect(75,buildingHeight,'LightGray','Black',1);
    building.x = 200*i;
    building.y = groundY-buildingHeight;
    background.addChild(building);
    buildings.push(building);
}
```

You should see this:

![Halle With Buildings](http://i.imgur.com/LSKBOsR.png)

Make sure you understand what each line of this code does. Change how the building appear. Can you make them have different heights? Different colors?

![Halle With Buildings With Background](http://i.imgur.com/kyeRy7x.png)

Now, write code in `update()` that animates the boxes so that they move towards Halle. Use the technique we applied to `backgroundBox` to make the buildings continually appear in the game as Halle walks. 

# Step 9 - Setting Up Gameplay

You've created a rad background and are now ready to move on to gameplay. You'll be coding up and designing some game elements which Halle can interact with. The game manager provides an API for creating objects which move around the screen and can be run into, jumped over, or shot with Halle's gun. 

To create a new game manager, add the following code to `index.html` after `TODO: 3` 
    
    var game = opspark.createGameManager(app,hud);

The "level" file is where we are going to define all of our gameplay for our game. Add the following script to `index.html` in the `<head>` element underneath the comment that says `<!-- add any additional scripts here -->` 

```html
<script src="js/level01.js"></script>
```

And then add the following code to `index.html` following the creation of the game manager

    opspark.runLevelInGame(game);

Open up `js/level01.js` file in your editor. You should see this:

![Level01.js](https://i.imgur.com/hVsROUh.png)

This file is where we are going to be writing our code for the next couple of steps.

# Step 10 - Creating Your First Obstacle

An obstacle is the simplest element in our game. It moves at a fixed speed toward Halle as the game progresses. The obstacle must be avoided by either jumping or ducking and cannot be destroyed by being shot with Halle's gun. If the obstacle collides with Halle, Halle takes damage. If Halle takes enough damage, she dies and the game is over. 

We will create our first obstacle in `js/level01.js` inside of the `runLevelInGame` function. 

Add this code below the comment that says `// BEGIN EDITING YOUR CODE HERE`

    var hitZoneSize = 25;
    var damageFromObstacle = 10;
    var myObstacle = game.createObstacle(hitZoneSize,damageFromObstacle);

This code declare a variable `myObstacle` and creates a new obstacle using the game's `createObstacle()` function. The `createObstacle` function takes two parameters which define the size of the object (`hitZoneSize`) and how much damage the obstacle does when it collides with Halle (`damageFromObstacle`)

Add this code to the code you just wrote

    myObstacle.x = 400;
    myObstacle.y = 100;

This position that obstacle somewhere on screen by modifying the `x` and `y` properties of `myObstacle` 

Finally, add this code:

    game.addGameItem(myObstacle);    

Once this is done correctly, you should see a gray circle on the screen which moves towards Halle.

![Gray Circle](https://i.imgur.com/Yyk0bEK.png)

The circle you see on the screen is the "hit zone" for the obstacle. Once that hit zone collides with Halle, you should see Halle's health indicator decrease by the amount you specified in `damageFromObstacle`. Halle has hitzones too. Open up `index.html` and find the `debugHalleHitZones` variable and change it to `true` You should now see the circles that make up Halle's hitzone.

![Halle Hitzone](https://i.imgur.com/vdwaY4M.png)

Change the `y` property of `myObstacle` so that it eventually collides with Halle

The hitzones in our game are used for collision detection and always present, but when we are playing our game we don't actually show them. Instead of circles we draw something that represents our obstacle. 

Let's make our first obstacle be a saw blade. Add the following code:

    var obstacleImage = draw.bitmap('img/sawblade.png');
    myObstacle.addChild(obstacleImage);

This loads up an image and adds it to our obstacle. You should now see a saw blade on the screen. 

![Saw blade](https://i.imgur.com/T9eSaWb.png)

You should also notice that saw blade doesn't fit within the hitzone. That is because when we `myObstacle.addChild()` the image is placed at the origin of the hitzone. You should adjust the `x` and `y` property of `myObstacle` so that it fits within the hit zone.

    obstacleImage.x = -25;
    obstacleImage.y = -25;

When you are done you should see:

![Saw blade correctly positioned](https://i.imgur.com/P6PIIEe.png)

You can hide your hitzones for now. 

In `index.html` change the `debugHalleHitZones` variable to false.

In `js/level01.js` pass `false` to the method `game.setDebugMode()` 

# Step 11 - Many Obstacles

Declare a function `createSawBlade` with two parameters `x` and `y`

```js
var createSawBlade = function(x,y) {
    // your code goes here
}  
```

Identify the code that creates your saw blade and adds it to the game and move it into the body of `createSawBlade()`. Adapt that code to use the `x` and `y` parameters to place the saw blade at `(x,y)` on the screen.

Call `createSawBlade()` three times with different `x` and `y` arguments in order to place the saw blade at different locations. You should place the saw blades so Halle can jump over some and duck others.

![Three saw blades](https://i.imgur.com/h1uGz6p.png)

# Step 12 - Level Data

In a professional game, the programmers write the code for a game engine which runs on data which is built by game designers. This data, as well as all of the artwork, defines the entire world of the game. Separating the game code from the data allows you to easily modify the behavior and gameplay of the game without actually modifying the code. 

Look at the `levelData` variable in `js/level01.js`, you should see three objects in the `gameItems` property. 

Delete your calls to the `createSawBlade` function and replace them with code that uses the data from the `gameItems` property of `levelData` to define where the saw blades are placed. Use the Array [forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) function. 

Add a couple more saw blades to your game.

![Lots Of saw blades](https://i.imgur.com/HXJtMAN.png)

# Step 13 - Roll Your Own Obstacles

You are now ready to add new kinds of obstacles to your game. To do this, decide what kinds of obstacle you want in your game and choose a name for it. As an example, I am going to create a very boring obstacle which I will call "box". **You** should name your obstacle something else, and change the code accordingly.

First, write a function that creates your obstacle

```js
var createBox = function(x,y) {
    // ????
};
```

Then, test it by calling that function directly.

```
createBox(100,200);
```

Then, modify `levelData` to add additional obstacles with that type. Here is an example object you should add to the `gameItems` property of `levelData`

```js
{type: 'box',x:100,y:200}
```


Finally, modify your function that you pass into `forEach()` to handle that new type of obstacle. 

# Step 14 - Enemies!

Obstacles are only one kind of thing you might find in a game. In most games, you have enemies you have to avoid or shoot as well as different items which you can collect to increase your score or give you powers. We started our game with obstacles because they were the simplest thing to make, but now that we understand the basics we can create more complex things for Halle to interact with.

If you look in `src/js/game.js` at the `createObstacle()` function, you will see the following code:

```js
function createObstacle(radius,damage) {
    var gameItem = createGameItem('obstacle',radius);
    gameItem.velocityX = -2;

    gameItem.onPlayerCollision = function() {
        changeIntegrity(-damage);
    };
    return gameItem;
}
```

`createObstacle()` calls `createGameItem()`, sets a couple of properties on the returned object, and then returns that same object. This provides a clue as to how we might work with the code. We are going to be calling `createGameItem()` for the rest of the tutorial instead of `createObstacle()`. Let's try it out and see what it can do.

We will be adding all of the code to `js/level0.js`. Before we begin, find the call to `game.setDebugMode()` and change the argument to `true` in order to show the hitzones.

We are going to create a new game item similar to how we created our other obstacles. Add the following code:

```js
var enemy =  game.createGameItem('enemy',25);
var redSquare = draw.rect(50,50,'red');
redSquare.x = -25;
redSquare.y = -25;
enemy.addChild(redSquare);
```

This creates a new game item but we need to position it on screen:

```js
enemy.x = 400;
enemy.y = groundY-50;
```

Finally you can call `addGameItem()` in order to show the enemy on screen.

```js
game.addGameItem(enemy);
```

When that is done correctly you should see a red square on the screen.

![Red Square](https://i.imgur.com/MrpvAjk.png)

Feel free to customize how your enemy looks. Try making it bigger or drawing some other shapes.

# Step 15 - Game Item Properties

The variable `enemy` is an object created by `createGameItem()` which has a number of properties you can set in order to customize how the item behaves in the game. In this step, we are going to play around with those properties. You will write this code in `js/level01.js` anywhere after you have declared and initialized the `enemy` variable. 

## velocityX/velocityY

You may have noticed that our enemy is not moving like the saw blades in the previous steps. That is because a game item created by `createGameItem` does not have any *velocity* when it is first created. A game item's `velocityX` property says how many pixels it will move in the X direction for each frame. Similarly, the `velocityY` property says how many pixels it will move in the Y direction for each frame. 

Try writing this:

```js
enemy.velocityX = 1;
```

What happened?

Modify the code you just wrote so that the square collides with Halle.

## rotationalVelocity

The `rotationalVelocity` property of a game item allows for you to change the rotation over time. The value of `rotationalVelocity` determines how many degrees the objects rotates in each frame.

Write the code to set the `rotationVelocity` property of the `enemy` game item to the value `10` and see what happens.

## onPlayerCollision

The `onPlayerCollision` property holds a different kind of value. Instead of a number or a string, its value is a function. The function is called whenever that game item collides with Halle. You may have noticed that our enemy passes through Halle without any kind of effect. That is because when the game item is first created, the function in the `onPlayerCollision` property does nothing. 

However, we can change that. Fist, write an empty function and assign it to the `onPlayerCollision` property.

```js
enemy.onPlayerCollision = function() {
};
```

To test that is is being called correctly, add the following code inside the function you just created.

```js
console.log('The enemy has hit Halle');
```

Open the JavaScript console and confirm that this is working properly.

To make the enemy do damage when it collides with Halle, you can call the `game.changeIntegrity()` function. 

Calling it with a negative number:

`game.changeIntegrity(-10);`

causes Halle to lose *integrity* or take damage

Calling it with a positive number:

`game.changeIntegrity(10);`

causes Halle to gain *integrity* or lose damage 

Try calling the `changeIntegrity()` function on the `game` object in your `onPlayerCollision` function with a couple different arguments and see what happens.

## onProjectileCollision

The `onProjectileCollision` property works much like `onPlayerCollision` but instead the function is called whenever Halle successfully shoots the game item.

Write some code that prints out "Halle has hit the enemy" whenever Halle shoots an enemy. Once this is done, you should be able to open the JavaScript console and see the message whenever you shoot an enemy.

The `game.increaseScore()` function lets you change the score of the game. Add this code to the function you just wrote

`game.increaseScore(100);`

You should see your score increase when Halle shoots an enemy.

## Behaviors

`onPlayerCollision` and `onProjectileCollision` are examples of *event callbacks* which allow you to create complex behavior in your game. You can change how your enemy looks or acts in these functions. 

Each game item has three built-in behaviors that you can call in response to events

`fadeOut()` will cause the item to disappear by fading out
`shrink()` will cause the item to decrease in size out of existence
`flyTo(x,y)` will cause the item to quickly move to a place on screen defined by `x` and `y`

Try adding the following code to the function assigned to `enemy.onPlayerCollision`

```js
enemy.fadeOut();
```

Now use one of the behavior functions described above in the function assigned to `enemy.onProjectileCollision` to make the enemy disappear whenever Halle shoots it.

# Step 15 Part 2 - Design An Enemy

You now should know enough to make your own enemy. To get started, take all of the code you wrote in the last step and move it into a new function called `createEnemy`

```js
function createEnemy() {
    // all code from step 14
}
```

Introduce two parameters `x` and `y` into your function

```js
function createEnemy(x,y) {
```

Then use `x` and `y` in your function body to place the enemy in a location given by those parameters.

You can now call the `createEnemy()` function multiple times to make several enemies. 

```
createEnemy(400,groundY-10);
createEnemy(800,groundY-100);
createEnemy(1200,groundY-500);
```

Once you have completed this step, you will have a working enemy for your game. Now you need to make it your own. Change the code in your `createEnemy` function to customize the enemy for **your** game. 

Finally, add an object for your enemy locations in `levelData.gameItems` and then modify your code to create enemies from that data. 

# Step 16 - Design A Reward

Create a new game item that is neither enemy nor obstacle. The game item should be positioned such that Halle must jump to be able to reach it. When she collides with it, it should disappear and the score should be increased. 

# Congratulations

You've written your first game! Give yourself a chance to play with what you created. Think about how you could make it better and what you would like to see in the game. Then, try changing the code to make it happen. 

Any of the code in your game can be modified. Look around in the source code and try to understand it. You can read the documentation for [easel.js](http://www.createjs.com/docs/easeljs/modules/EaselJS.html) to draw more interesting shapes or [tween.js](http://www.createjs.com/tweenjs) to make interesting animations. 

Good luck!

