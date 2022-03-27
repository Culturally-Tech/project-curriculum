## Resources

### Exemplar

[YouTube Video](https://www.youtube.com/watch?v=2nucjefSr6I)

### Student Facing Repo

[Student GitHub Repo](https://github.com/stephencastaneda/MarioGameStarterCode )

### Finished Exemplar

[CodeSandbox Exemplar](https://i3n98s.csb.app/)

### Kaboom JS Documentation

[Kaboom JS Docs](https://kaboomjs.com/)

## Breakdown

Decription: 

We are going to be creating a mock of the classic video game, Mario! Our game will have two levels. Once you have the knowledge to build two levels you have the knowledge to build on many more levels. We are starting with an index.html and game.js file.

### Setup - Namita

Students should first clone the repo: https://github.com/stephencastaneda/MarioGameStarterCode

You can explain the following to students about what is already in their code:

1. We have a script that points to kabooms documentation

```javascript
   <script src="https://kaboomjs.com/lib/0.5.0/kaboom.js"></script>
```

2. We script tag to the bottom of your index.html that links to your game.js file

```javascript
    <script src="game.js"></script>
```

3. We applied some light styling. We just wanted to make sure our game board takes up the entire screen and we prevent the user from scrolling. This is normally something that would be done in a css file but because we have such little need for css and kaboom does the work for us, we just added it via style tag in our html.

```html
    <style>
     body {
       margin: 0;
       overflow: hidden;
     }
   </style>
```

**Format on Save Settings Fix*

Students will need to adjust their format settings to make sure formatting doesn't get in the way of us using kaboom's syntax. 

Click the hamburger menu at top left of screen > File > Preferences > Settings > In the "search settings" field search "format on save" > Uncheck the box

** Opening preview in new tab

Click on the boxes in the top right hand corner of the preview screen to open your preview in full screen. You will be toggling back and forth between your code and full screen view a lot.

### Layers and Sprites - https://youtu.be/2nucjefSr6I?t=343 - Stephen

Head over to your game.js file. Let’s initialize our kaboom

```javascript
kaboom({
 global: true,
 fullscreen: true,
 scale: 1,
 debug: true,
});
```

Let's add our game scene

```javascript
scene("game", () => {

})
```

Then add the start function and pass it our game

```javascript
start("game")
```

Save the work and you should see a checker like board meaning our new kaboom has been initilalized.

Let’s make the background color black by adding the `clearColor` property in our kaboom initialization

```javascript
kaboom({
 global: true,
 fullscreen: true,
 scale: 1,
 debug: true,
// add the property below
clearColor: [0, 0, 0, 1]
});
```
Save your work and you should now see a black background.

Let's add our layers

```javascript
scene("game", () => {
// we've  added background object and ui layers and since object is default we add it outside the array
 layers(['bg', 'obj', 'ui'], 'obj')

})
```

We are going to add our maps for our gameboard, but first we need to load our sprites.

Go to the imgur page here https://imgur.com/a/F8Jkryq

For this section demonstrate how you are using imgur to host your image files and only referencing the links from the url in the code. Students DO NOT need to do this with you. Just have them copy 'Sprite Paths Level 1' code from their repo. This code should be posted outside of the `scene()` function right after our `kaboom()` initilization at the top of the page.

It should look like this when they're finished copying

```javascript
loadRoot('https://i.imgur.com/');
loadSprite('coin', 'wbKxhcd.png');
loadSprite('evil-shroom', 'KPO3fR9.png');
loadSprite('brick', 'pogC9x5.png');
loadSprite('block', 'M6rwarW.png');
loadSprite('mario', 'Wb1qfhK.png');
loadSprite('mushroom', '0wMd92p.png');
loadSprite('surprise', 'gesQ1KP.png');
loadSprite('unboxed', 'bdrLpi6.png');
loadSprite('pipe-top-left', 'ReTPiWY.png');
loadSprite('pipe-top-right', 'hj2GK4n.png');
loadSprite('pipe-bottom-left', 'c1cYSbt.png');
loadSprite('pipe-bottom-right', 'nqQ79eI.png');
```

Let’s create our map within our scene function. **(Explain briefly how the map works but students can copy Map Level 1 Part A from their GitHub repo)**

Add the map code to the scene function

```javascript
scene("game", () => {
 
layers(['bg', 'obj', 'ui'], 'obj')

// start by adding the = signs which will be the bottom of our board and will leave a space so our sprite can fall down
// then you can add the rest which will act as constraints of your game

const map = [
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',      
'==============================   ====='
]

})
```

*Using the kaboom js function can someone tell us how we assign a character in our case the ‘=’ to a sprite? What is the syntax?*

ANSWER

```javascript
'=': [sprite('block')]
```

Now let’s use our levelCfg function to add our config for this scene! Let’s do it!

```javascript
scene("game", () => {
 
layers(['bg', 'obj', 'ui'], 'obj')

const map = [
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',
'                                      ',      
'==============================   ====='
]

const levelCfg  = {
width: 20,
height: 20,
// the block is the same block we imported from imgur
'=': [sprite('block', solid())]
// the below line adds it as game level and we pass through our map and levelCfg
}
const gameLevel = addLevel(map, levelCfg)

})
```

Now let's refresh our page and we shoud see our game board with the blocks!

Let's make our board a bit larger in the kaboom function change the scale to 2

```javascript
 scale: 2
```

### Place Sprites on the First Level -  https://youtu.be/2nucjefSr6I?t=953 - Namita

We’ve got the bottom blocks. Let’s add some more sprites!

We’ve added all of  the characters that will eventually represent sprites to our map. All of these characters will eventually represent our coin, mushroom, block, top of our pipe, and bottom of the pipe. **(Explain briefly how the map works but students can copy Map Level 1 Part B from their GitHub repo)**

```javascript
const map = [
   
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "     %   =*=%=                        ",
     "                                      ",
     "                            -+        ",
     "                    ^   ^   ()        ",
     "==============================   ====="
   ]
```

Let’s assign values now in our levelCfg

```javascript
const levelCfg  = {
width: 20,
height: 20,
'=': [sprite('block'), solid()],
'$': [sprite('coin')],
'%': [sprite('surprise'), solid(), 'coin-surprise'],
'*': [sprite('surprise'), solid(), 'mushroom-surprise'],
'}': [sprite('unboxed'), solid()],
'(': [sprite('pipe-bottom-left'), solid()],
')': [sprite('pipe-bottom-right'), solid()],
'-': [sprite('pipe-top-left'), solid()],
'+': [sprite('pipe-top-right'), solid()],
}
```

Refresh and you should see all of your sprites added. The pipes are a bit too big so let’s scale them.

```javascript
'(': [sprite('pipe-bottom-left'), solid(), scale(0.5)],
')': [sprite('pipe-bottom-right'), solid(), scale(0.5)],
'-': [sprite('pipe-top-left'), solid(), scale(0.5)],
'+': [sprite('pipe-top-right'), solid(), scale(0.5)],
```

Refresh and now the pipes should be scaled proportionally to the rest of our board.

Let’s add some evil mushrooms and add one mushroom for the future. **(This sprites for these mushrooms already exist from the copy and paste earlier)**

```javascript
'^': [sprite('evil-shroom'), solid()],
'#': [sprite('mushroom'), solid()],
```

Refresh and you will see our evil mushrooms, but you won’t see the additional mushroom we added for now.

### Adding Mario - https://youtu.be/2nucjefSr6I?t=1290 - Namita

Let’s use the kaboom method of add and save it to a variable named player so that we can use it later. This player will essentially be our mario character.

```javascript
const player = add([
  sprite('mario'), solid(),
// let's give him a position
  pos(30, 0),
// let's give him gravity
  body(),
// to get rid of any weird behavior we're going to also add origin bot
  origin('bot')
])
```

Refresh and we should see Mario fall onto our game board like only Mario can! Notice that Mario falls directly on the blocks and stops because our blocks are solid.

Let’s add our score! Use the add function!

```javascript
// save it to a variable so we can use it later 
const scoreLabel = add([
// adding text and giving it the score as the text
 text(score),
// position on the grid
 pos(30, 6),
// let's add it to our UI layer. Remember we set it up to have everything use our object layer as default so this is our first time using the UI layer. So it won't interfere with anything happening in our game
layer('ui'),
// add a value of score
{
 value: score,
}
])

// add some text so we can see the level we are on. This will be useful for later when we have multiple levels. 

add([text('level' + score, pos(4,6))])
```

Refresh and you will get an error that the score isn’t defined. Simply replace the score variable with the string ‘test’ in the three places it appears. This is just so we can temporarily mock the score variable behavior until we get it up and running.

The changes should look like this 

```javascript
text(score) => text('test')

value:score => value:'test'

add([text('level' + score, pos(4,6))]) => add([text('level' + 'test', pos(4,6))])

```
Now if you refresh you’ll see our text that reads 'test' appear! Later on this is where our level and score will be.


### Keyboard Events - https://youtu.be/2nucjefSr6I?t=1508 - Stephen

Let’s make our player move. Add the following

```javascript
// move the MOVE_SPEED and JUMP_FORCE variables to the top of the file. Make sure they are placed outside of the `scene()` function

const MOVE_SPEED = 120
const JUMP_FORCE = 360

// this code should be place within the `scene()` function

keyDown('left', () => {
   player.move(-MOVE_SPEED, 0)
})

keyDown('right', () => {
   player.move(MOVE_SPEED, 0)
})

// let's make our player jump too

keyPress('space', () => {
 if (player.grounded()) {
 player.jump(JUMP_FORCE)
 }
})
```

Refresh and test and now Mario should be able to move right and left and jump! He can jump, but he’s not big enough to jump on the higher blocks. Let’s change that!

### Make Mario Big - https://youtu.be/2nucjefSr6I?t=1670 - Stephen

Right underneath our `add([text(‘level’ + ‘test’, pos(4, 6))])` function let’s add a function to make Mario bigger so he can jump a bit higher on the larger blocks

```javascript
function big() {
 let timer = 0
 let isBig = false
  return { 
   update() {
   if (isBig) {
// dt is a kaboom method that gives you the delta time since the last frame
   timer -= dt()
   if (timer <=0) {
   this.smallify()
  }
 }
},
   isBig() {
   return isBig
},
    smallify() {
    this.scale = vec2(1)
    timer = 0
    isBig = false
},
    biggify() {
    this.scale = vec2(2)
    timer = time
    isBig = true
  }
 }
}
```

Now we just add our `big()` function onto our Mario player. 

```javascript
const player = add([
  sprite('mario'), solid(),
  pos(30, 0),
  body(),
  big(),
  origin('bot')
])
```

You will notice that even after adding the `big()` function mario still jumps the same, but we will change that later. 

### Coin and Mushroom -  https://youtu.be/2nucjefSr6I?t=1851  - Namita

Now let’s grow a mushroom. Let’s add the following code directly under our mario player code.

```javascript
player.on("headbump", (obj) => {
  // if our sprite has the tag coin-surprise we will spawn or create a new sprite which in our case is a coin sprite
 if (obj.is('coin-surprise')) {
// by using gridPos we put the newly spawned object directly on top of where the old one was
  gameLevel.spawn('$', obj.gridPos.sub(0, 1))
  destroy(obj)
  }
})
```

Refresh the page and make mario hit the first brick with a question mark and you’ll see a coin appear!

Now let’s add our unboxed sprite to replace the old brick on headbump

```javascript
player.on("headbump", (obj) => {
 if (obj.is('coin-surprise')) {
  gameLevel.spawn('$', obj.gridPos.sub(0, 1))
  destroy(obj)
  gameLevel.spawn('}', obj.gridPos.sub(0, 0))
  }
})
```

Now let’s do the same thing for our mushroom surprise. *This would be a good opportunity to give students a minute to do this themselves since it’s basically a repeat of the same thing they just did.*

Add the `mushroom-surprise` conditional to your existing `player.on("headbump"...)` function

```javascript
player.on("headbump", (obj) => {
 if (obj.is('coin-surprise')) {
     gameLevel.spawn('$', obj.gridPos.sub(0, 1))
     destroy(obj)
     gameLevel.spawn('}', obj.gridPos.sub(0, 0))
  } 
  if (obj.is('mushroom-surprise')) {
      gameLevel.spawn('#', obj.gridPos.sub(0, 1))
      destroy(obj)
     gameLevel.spawn('}', obj.gridPos.sub(0, 0))
    }
  })

```

Now refresh your page. When you hit the first question mark brick you'll see a coin. When you hit the second you should see a mushroom.

Now let’s make our mushroom move. Let’s first add a mushroom tag to our mushroom sprite.

```javascript
'#': [sprite('mushroom'), solid(), 'mushroom'],
```

Now we will use action to make our mushroom move.

```javascript
action('mushroom', (m) => {
  m.move(10, 0)
})
```

Refresh your page, you’ll notice that the mushroom moves but it doesn’t drop when it gets to the end of the brick. Any idea how we can fix this?

Yup, you got it! Let’s add gravity by adding the `body` component to our mushroom sprite.

```javascript
'#': [sprite('mushroom'), solid(), 'mushroom', body()],
```

Now if you refresh your page you'll see when the mushroom falls off the brick it falls down.

Now let’s make Mario grow if he eats the mushroom. We can add this code right above our keyDown events.

```javascript
player.collides('mushroom', (m) => {
 destroy(m)
// we previously created our biggify function that we can now pass a value for time
 player.biggify(6)
})

player.collides('coin', ( c ) => {
 destroy( c )
// we want to increment our score label when mario collides with a coin
 scoreLabel.value++
 scoreLabel.text = scoreLabel.value
})
```

Let’s add a coin tag to our coin sprite.

```javascript
'$': [sprite('coin'), 'coin'],
```

Let’s refresh the page. Hit the first question mark box and jump with Mario to collide with the coin. Now you should see the score appear as NaN when Mario collides with a coin. This is something we have to fix. May be a good point to pause and ask students to look at their code and figure out why it’s currently showing up as NaN. We will fix this soon.

You will also notice that Mario gets bigger when he eats a mushroom! We’re almost there but we also want him to jump higher when he eats the mushroom so he can get on the higher level.

 We need to add a couple of new variables at the top of our file

```javascript
let CURRENT_JUMP_FORCE = JUMP_FORCE
const BIG_JUMP_FORCE = 550
```

So when he gets bigger we need to make the `CURRENT_JUMP_FORCE = BIG_JUMP_FORCE`

```javascript
smallify() {
    this.scale = vec2(1)
// add the line of code below to our smallify function
CURRENT_JUMP_FORCE = JUMP_FORCE  
    timer = 0
    isBig = false
},
    biggify() {
    this.scale = vec2(2)
// add the code below to our biggify function
CURRENT_JUMP_FORCE = BIG_JUMP_FORCE
    timer = timer
    isBig = true
```

Let’s also make our mushroom move faster

```javascript
action('mushroom', (m) => {
  m.move(20, 0)
})
```

Refresh our page. It’s still not jumping higher. Can anybody figure out why it’s still not changing? *Check your code.*

Right! We need `player.jump` to jump at the `CURRENT_JUMP_FORCE`. Let's change the variable we're passing to the `player.jump` function to `CURRENT_JUMP_FORCE`

```javascript
keyPress('space', () => {
 if (player.grounded()) {
 player.jump(CURRENT_JUMP_FORCE)
 }
```

Refresh your page, collide with a mushroom, and now you’ll see Mario has bunnies like LeBron! 👑

### Let's Make the Little Guys Move -  https://youtu.be/2nucjefSr6I?t=2402 - Stephen

Let’s make the little guys move now! Right underneath our last `player.collides` function let’s add

```javascript
player.collides('dangerous', (d) => {
// we are going to trigger a lose scene when ever player collides with a sprite with the dangerous tag
 go('lose', score: { scoreLabel.value })
})
```

Now we have to write our lose scene. Come completely out of our previous scene. *This code will need to exist outside of the closing curly and parentheses.*

Add the following for our scene

```javascript
scene('lose', ({ score }) => {
 add([text(score, 32), origin('center'), pos(width()/2, height()/2)])
})
```

Add a dangerous tag to our evil mushroom

```javascript
'^': [sprite('evil-shroom'), solid(), 'dangerous'],
```

Let’s make our evil shrooms move. Add the following code within your old scene. You could place this after your last `player.collides` function

```javascript
action('dangerous', (d) => {
 d.move(-ENEMY_SPEED, 0)
})
```

Let’s add our `ENEMY SPEED` variable at the top of the file with our other variable declarations.

```javascript
const ENEMY_SPEED = 20
```

Refresh now if you collide you will go to the losing scene. It still says test because we need to pass in our score variable in a few places

1.

```javascript
const scoreLabel = add([
 text(score)
 pos(30, 6)
layer('ui')
{
 value: score,
}
])
```

2. At the bottom of our file pass it into the start function

```javascript
start("game", { score: 0 })
```

3. Pass it into the game itself towards the top of your file

```javascript
scene("game", ({ score }) => 
```

Refresh and you should be able to collide with a coin to see the score change and collide with an evil mushroom to see the score displayed.

Let’s now kill the mushrooms if we jump on them

At the top of your file where you declared the other variables declare a isJumping variable

```javascript
let isJumping = true
```

If our player is grounded we want is jumping to be true

```javascript
keyPress('space', () => {
 if (player.grounded()) {
// add the below code within this conditional
 isJumping = true
 player.jump(CURRENT_JUMP_FORCE)
 }
 })
```

Above the above `keyPress` keyboard event add the following 

```javascript
player.action(() => {
 if(player.grounded()) {
   isJumping = false
  }
})
```

Now let’s add the following code to our `player.collides` with our `dangerous` tag

```javascript
player.collides('dangerous', (d) => {
// if mario is jumping during the collision then we will destroy the mushroom if not then we lose
 if (isJumping) {
  destroy(d)
} else {
 go('lose', { score: scoreLabel.value})
 }
})
```

Let’s now tackle the death fall in the event our player falls into the gap.. Declare a variable at the top

```javascript
const FALL_DEATH = 400
```

If the player falls in the gap we want it to be a game over. Let’s use the action function for this. It’s important to note that action runs every frame so we are essentially checking something each frame so it comes in handy. Let’s add the following code underneath our last `player.collides` function

```javascript
player.action(() => {
// pretty handy function to keep camera position on player
  camPos(player.pos)
// if our players position on y axis is greater than fall death we want to go to the lose screen
  if (player.pos.y >= FALL_DEATH) {
 go('lose', { score: scoreLabel.value })
   }
})
```

Refresh and try it out! You can see now the camera is actually following our user. Now let’s cause our player to jump in the gap and you should see that we go to the lose screen.

### Go to the Next Level - https://youtu.be/2nucjefSr6I?t=2865 - Stephen

Let’s make our game go to the next level when the player collides with the pipe and presses down on the keyboard. Add the following underneath your last `player.action` function

```javascript
player.collides('pipe', () => {
  keyPress('down', () => {
     go('game', {
          level: (level + 1),
          score: scoreLabel.value
     })
   })
})
```
Let’s pass the level into our `start` function at the end of the file

```javascript
start("game", { level: 0, score: 0 })
```

We also need to pass the level into our current game at the top of the file

```javascript
scene("game", ({ level, score }) =>
```

Lastly, let’s make sure our level displays. Add the level to your add text function.

```javascript
//since our level is set to 0 we want to make sure it says 1 instead to the user so we add 1
//we also use the parseInt function to make sure it displays a number
//we adjust the position slightly so it doesn't overlap our score
  add([text('level ' + parseInt(level + 1) ), pos(40, 6)])
```

Refresh now you’ll see our level displayed. 

We need to make a couple slight adjustments to make sure our game is functioning as it should and we can go to the next level. Let’s add pipe tags to the top left and top right so it only effects the top two pipes.

```javascript
'-': [sprite('pipe-top-left'), solid(), 'pipe'],
'+': [sprite('pipe-top-right'), solid(), 'pipe'],
```

Refresh and jump on the pipe and press down. You should see the level text at the top change to level 2. At the moment it will take you to the same level/board because we haven’t yet written the code for our next level. Let’s do that now!

### New Level Map - https://youtu.be/2nucjefSr6I?t=3085 - Namita

Let’s change our one map into an array of `maps`. Add sqaure brackets around the outside of your first map, then add an empty array. Change `map` to `maps`.

There `maps` array should now look like this.

```javascript
const maps = [
 [
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "     %   =*=%=                        ",
     "                                      ",
     "                            -+        ",
     "                    ^   ^   ()        ",
     "==============================   =====",],
[ ],
]
```

Now let’s adjust our addLevel function

```javascript
//we now want to get our maps array and use our level variable which will first be set to 0
const gameLevel = addLevel(maps[level], levelCfg)
```

Let’s copy our first map and use it as a start for our second map. Place your cursor between empty array and press enter. Copy your first map into this array.

There maps should now look like this. Essentially, the same maps repeated.

```javascript
const maps = [
 [
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "     %   =*=%=                        ",
     "                                      ",
     "                            -+        ",
     "                    ^   ^   ()        ",
     "==============================   =====",
],
[ 
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "     %   =*=%=                        ",
     "                                      ",
     "                            -+        ",
     "                    ^   ^   ()        ",
     "==============================   =====",
],
]
```

Refresh your page and go to the next level by pressing down on the pipes. At the moment the levels look the same, but let's change that. First, let’s load in some blue sprites for the next level. Underneath your last loaded sprite, let’s add a few more. **Have students copy the code from their GitHub repos under Sprite Path 2.**

It will look like this and should be placed with the other loaded sprites towards the top of the file.

```javascript
loadSprite("blue-block", "fVscIbn.png");
loadSprite("blue-brick", "3e5YRQd.png");
loadSprite("blue-steel", "gqVoI2b.png");
loadSprite("blue-evil-shroom", "SvV4ueD.png");
loadSprite("blue-surprise", "RMqCc1G.png");
```
Most of our logic has already been done for us. Let’s now add our sprites to our `levelCfg`. We are going to reuse our same `dangerous` and `coin-surprise` tags!

```javascript
"!": [sprite("blue-block"), solid(), scale(0.5)],
"£": [sprite("blue-brick"), solid(), scale(0.5)],
"z": [sprite("blue-evil-shroom"), solid(), scale(0.5), "dangerous"],
"@": [sprite("blue-surprise"), solid(), scale(0.5), "coin-surprise"],
"x": [sprite("blue-steel"), solid(), scale(0.5)]
```
Now let’s add our characters to our map. **(Students should copy and paste the map from Map Level 2 in their GitHub repo for the second map)**

```javascript
const maps = [
 [
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "                                      ",
     "     %   =*=%=                        ",
     "                                      ",
     "                            -+        ",
     "                    ^   ^   ()        ",
     "==============================   =====",
],
[ 
     "£                                    £",
     "£                                    £",
     "£                                    £",
     "£                                    £",
     "£                           x        £",
     "£      @@@@@@             x x        £",
     "£                       x x x        £",
     "£                     x x x x  x   -+£",
     "£             z   z x x x x x  x   ()£",
     "!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!",
],
]
```

Refresh and you should now be able to go on to level 2 once you press down when on the pipe!

We did it! 

Complete level 2 just like you did the first level by reaching the pipe and pressing the down arrow. You’ll notice an error when finishing level 2 because we don’t have a level 3. Let’s loop the levels so we don’t run into this error. Find the `player.collides` function for our pipe tag and utilize the modulus operator.

```javascript
player.collides('pipe', () => {
  keyPress('down', () => {
     go('game', {
// add the modulus maps.length
          level: (level + 1) % maps.length,
          score: scoreLabel.value
     })
   })
```

Refresh and there you have it!!! We did it!

## Extension Activity

1. You need to add one more additional sprite to map 1 and map 2
2. Extra points if you can make the sprite interactice (ex. when mario collides with it he gains a point)



