# Kinect Scrolling Plugin for Phaser Framework

I wanted to simulate scrolling horizontal in my games to display levels for example or a section of authors using only the canvas element in HTML5, but I could not find a good solution... so I decided to create my own plugin to Phaser Framework :D

//Kinect scrolling based on http://ariya.ofilabs.com/2013/11/javascript-kinetic-scrolling-part-2.html

##Load the Plugin

```javascript
this.game.kinectScrolling = this.game.plugins.add(Phaser.Plugin.KinectScrolling);
```

##Disable the kinematic motion - *_I don't know why but it is possible_*

```javascript
this.game.kinectScrolling.init(false);
```

##Start the Plugin

```javascript
this.game.kinectScrolling.start();
```

##Stop the Plugin

```javascript
this.game.kinectScrolling.stop();
```

##Complete Example

```javascript
var game = new Phaser.Game(1024, 768, Phaser.AUTO, '', {
    init: function () {
        
        //Load the plugin
        this.game.kinectScrolling = this.game.plugins.add(Phaser.Plugin.KinectScrolling);
    },
    create: function () {

        //Starts the plugin
        this.game.kinectScrolling.start();

        this.rectangles = [];

        var initX = 50;

        for (var i = 0; i < 26; i++) {
            this.rectangles.push(this.createRectangle(initX, this.game.world.centerY - 100, 250, 200));
            this.index = this.game.add.text(initX + 125, this.game.world.centerY, i + 1,
                        { font: 'bold 150px Arial', align: "center" });
            this.index.anchor.set(0.5);
            initX += 300;
        }

        //Changing the world width
        this.game.world.setBounds(0, 0, 320 * this.rectangles.length, this.game.height);
    },
    createRectangle: function (x, y, w, h) {
        var sprite = this.game.add.graphics(x, y);
        sprite.beginFill(Phaser.Color.getRandomColor(100, 255), 1);
        sprite.bounds = new PIXI.Rectangle(0, 0, w, h);
        sprite.drawRect(0, 0, w, h);
        return sprite;
    }
});
```

# Happy scrolling
Made with <3
