# ASCIIGraphics

This is a python library for easy graphics in the terminal.
See the `example.py` file of GitHub for an example with lots of comments

# How To Use

## Setup
The following steps are a suggestion only. 

1. Find the file called `ASCIIGraphics.py` and put it in the same folder as your project.
2. At the top of your code type `import ASCIIGraphics as graphics`. This will give you access to all the functionality in `ASCIIGraphics.py`
3. Ensure you have numpy and pynput installed. `ASCIIGraphics.py` needs these to run.
     - Use `pip install numpy` and `pip install pynput`
     - See [here](https://packaging.python.org/en/latest/tutorials/installing-packages/) for more information.
4. You can test to see if `ASCIIGraphics.py` is working by typing `graphics.test()` in your code.
     - See `example.py` for an example of this.
6. This code can only be run in specific places. For exampe, WindowsPowershell is fine, but the default IDLE that comes with python is not. This may require some trial and error and likely depends on your computer. For me, opening Powershell and running the comand `python [path to file]` works.
7. After running the test code a screen with a large box will appear. A smaller box is in the top left corner. Use arrow keys to move and escape to quit. If the screen doesn't appear to be rendering properly, press escape, put the output terminal in fullscreen, and run it again.
8. Congragulations, you have completed setup!!!



## Boxes
Everything that can be displayed on screen is a box. Boxes have a plate (initial appearence), size, and position when first created. There are 4 main things that you can do with boxes: display, move, add them onto eachother, and update.
### Creating Boxes
`Box` is a class. It has one required argument and three optional ones: size, pos, fill, and custom_pattern.
#### `size`
This is the only required argument for the Box class. It takes a tuple of two integers in the form of `(x_width, y_height)`. The box instance will be this size.
#### `pos`
The position of the box class. It takes a tuple of two integers or floats (floats will be rounded when used) in the form of `(x_pos, y_pos)`. The default value is `(0, 0)`.
#### `fill`
How the box's plate will appear. It takes a string and will raise `ValueError` if it is not an fill option. Allowed values are `['box', 'rounded box', 'lines', 'grid', 'solid fill', 'solid empty', 'custom']`. 
#### `custom_pattern`
If `fill = 'custom'` then `custom_pattern` will be used. This takes a multiline string and turns it into the `plate` of the box instance. 
It is important to note that the `size` value must be equal to or larger than the size of the string. Otherwise a `ValueError` is raised.
### Methods
#### `draw(self, other_box, from_scratch=True)`
Put the `plate` of `other_box` onto the `plate` of the calling object.
If `from_scratch` is set to False this will have the same effect as `draw_next`
#### `draw_next(self, other_box)`
Put the `plate` of `other_box` onto the `face` of the calling object.
The difference between `draw` and `draw_next` is that `draw` effectively clears all previous changes to the `face`. `draw_next` keeps previous cahnges.
#### `move(self, x, y)`
Change the pos value by x and y.
It is important to note that the positive direction is down and to the right.
#### `collide(self, other_box)`
Returns True if the two boxes are overlapping at all. 
### Display
This is increadibly easy. Every time you want to render the box onto the screen, simply put it in the print fuction. 
`print(Box(5, 5))`
### Important for Understanding
There are three important variables in the Box class. plate, face, and pos. 
#### plate
plate is the basic "look" of a box. This is assighned upon creation and is never changed. It is affected using the `fill` and `custom_pattern` arguments. Under the hood this is a numpy array of characters. 
#### face
This is the dynamic appearence of a box. It can be modified using the `draw` and `draw_next` methods. `face` is also a numpy array of values and is derived from the `plate`. The difference is that `face` is what is rendered when the instance is printed.
#### pos
A simple tuple that holds the sprites position. This can be changed with the `move` method. It dictates where the `other_box` goes when drawing. 

## User Input
This uses the [pynput](https://pynput.readthedocs.io/en/latest/) library to handle input from the keyboard. This will have to be downloaded before use. 

`pressed_keys` is a set that contains all curently pressed keys. 
They are stored as strings such as `'a', 'B', '5', ')', 'up', 'esc', and 'enter'`. 

## "Extra" Stuff
The `init()` and `qquit()` functions. 
### `init(catch_system=True)`
Currently I can only gauruntee compatibility for Windows. If the OS is not Windows a `RuntimeError` is raised. However, setting `catch_system` to False disables this catch. Instead, the program will throw an error at the first non-compatible code it comes across.

Other than ensure that the OS is compatible, `init` also starts the `keyboard_listener`. 

### `qquit()`
Stops the keyboard listener and calls `quit()`
Doesn't do anything else as of now. 

It is only called `qquit` becuase `quit` was taken.



