# Your First Project

## Creating a New Project

OpenFL includes a "create" command that can help generate an empty or sample project for you.

To create an empty project, open a command-prompt (Windows) or terminal (Mac/Linux) and run the following command:

    openfl create project HelloWorld

You can replace "HelloWorld" with whatever you want to call your project.

The project you just created is now placed in your 'Users-Folder'; if you did not have customized the path for your projects, yet. For example in Windows the path will be like: 'C:\Users\Your-User-Name\' ; So the 'HelloWorld'-Project can be found at 'C:\Users\Your-User-Name\HelloWorld\'.

In the command-prompt of Windows ( CMD ) you can use the system-variable ' %USERPROFILE% ' to locate the actual Users Home-folder; E.g. ( for copying the image ) :

    cp "%USERPROFILE%\Downloads\Downloaded-Image.png" "%USERPROFILE%\My-Project\Assets\My-New-Image.png"

If you instead use the PowerShell or running Linux you can use the $HOME-Variable; E.g. ( for moving the image ) :

    mv "$HOME/Downloads/Downloaded-Image.png" "$HOME/My-Project/Assets/My-New-Image.png"

## ... instead Creating a New Project based on an Example if you don't wish to use your own Image

OpenFL contains multiple samples for illustrating different features of the platform. One of the simple samples is called "DisplayingABitmap", as we build our first project, we will quickly walk through the steps to recreate this sample. You can also generate a copy of it yourself using:

    openfl create DisplayingABitmap

## Adding an Image

The first thing we will do is add an image. First, copy an image (PNG or JPG format) to the "Assets" folder of the project. We will be using [this image](https://raw.githubusercontent.com/openfl/openfl-samples/master/DisplayingABitmap/Assets/openfl.png), but you can download or copy any image you like.

Open the "Source/Main.hx" file in the editor of your choice. It should look something like this:

```Haxe
package;

import openfl.display.Sprite;

class Main extends Sprite {

    public function new () {

        super ();

    }

}
```

In order to import our image, we will want to import the `openfl.Assets` class, and add a `getBitmapData` call. There is more than one way to load an image in OpenFL, but the `Assets` class is designed to make this very simple.

You will want to use the name of your image, so if it is called "myimage.png", be sure to replace the example below with the right text to match your file name.

```Haxe
package;

import openfl.display.Sprite;
import openfl.Assets;

class Main extends Sprite {

    public function new () {

        super ();

        var bitmapData = Assets.getBitmapData ("assets/openfl.png");

    }

}
```

The `openfl.display.BitmapData` type represents the pixel data for an image. You can use this directly to read pixels, perform fills, and multiple other pixel-based effects. Often however, you will load directly from a file, and will not need to modify the data.

The easiest to display our data is using the `openfl.display.Bitmap` type, you can use the same `BitmapData` with multiple `Bitmap` instances, however you want it to display.

```Haxe
package;

import openfl.display.Bitmap;
import openfl.display.Sprite;
import openfl.Assets;

class Main extends Sprite {

    public function new () {

        super ();

        var bitmapData = Assets.getBitmapData ("assets/openfl.png");
        var bitmap = new Bitmap (bitmapData);
        addChild (bitmap);

    }

}
```

In order to see our `Bitmap` instance, we use `addChild` to make it visible on the display list. The "display list" is an easy-to-use method of drawing that is available in OpenFL, you can read more about it [here](openfl_basics/display_list.md).

## Positioning an Object

When you use the display list, you can use `x` and `y` properties to control where an object will be drawn.

```Haxe
package;

import openfl.display.Bitmap;
import openfl.display.Sprite;
import openfl.Assets;

class Main extends Sprite {

    public function new () {

        super ();

        var bitmapData = Assets.getBitmapData ("assets/openfl.png");
        var bitmap = new Bitmap (bitmapData);
        addChild (bitmap);

        bitmap.x = 100;
        bitmap.y = 200;

    }

}
```

If we set the bitmap position to (100, 200), instead of drawing at the upper-left of the window, it will be 100 and 200 pixels away from the corner, respectively. You can use any value you want, but for this sample, we will center the image.

Since the `x` and `y` values of a display object use the upper-left corner of the object, the math for centering our object will look something like this:

    var centerValue = (totalWidth - imageWidth) / 2;

We can determine the width of our window using the `stage.stageWidth` and `stage.stageHeight` values. We can use the `width` and `height` values of our bitmap to find how large it is. The resulting code looks like this:

```Haxe
package;

import openfl.display.Bitmap;
import openfl.display.Sprite;
import openfl.Assets;

class Main extends Sprite {

    public function new () {

        super ();

        var bitmapData = Assets.getBitmapData ("assets/openfl.png");
        var bitmap = new Bitmap (bitmapData);
        addChild (bitmap);

        bitmap.x = (stage.stageWidth - bitmap.width) / 2;
        bitmap.y = (stage.stageHeight - bitmap.height) / 2;

    }

}
```

## Running the Project

We are going to test our project with three different platforms, you can use [many more](advanced_setup/platforms/README.md).

If you open a command-prompt (Windows) or terminal (Mac/Linux), change to the directory of the project we created.

If you are using a code editor with OpenFL support built-in, you may be able to compile using a shortcut, such as Ctrl+Enter or a "Run" button in the editor. For sake of consistency, we will go over the steps for how you would build the project yourself from a command-line.

    openfl test neko

This command should run the project using Neko, a runtime included with the Haxe compiler.

    openfl test html5

If you use "html5" instead, the "openfl" command will open a local web server, as well as your default web browser.

    openfl test flash

The "flash" target will create a Flash SWF, and will use the default handler on your system for SWF files. You may wish to download a standalone "content debugger" Flash projector and set it to the default for SWF files on your system, as it is the best environment for testing Flash projects.

If you would like to run the command from a different folder on your system, you can also add an additional argument to the "test" command:

    openfl test ../DisplayingABitmap flash

## Issues

Any problems? Please visit our helpful [community forums](http://community.openfl.org) if you are experiencing trouble!
