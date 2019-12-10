# Force Sensing Mouse and its Applications
Chen Liang, Suresh Gandhi
## Abstract
Many human-computer interaction techniques - such as mouse and user interfaces - are designed in 2D space. While this could be an easy and intuitive way to interact, a drawback of this design idea is the increasing difficulty of interacting as more and more windows are opened. This project proposed an idea to mitigate this issue: several force sensors are attached to the bottom of the mouse to provide an additional degree of freedom. Some user interfaces are also brought to '3D' space to utilize the much expanded space. The aim is to increase the interaction efficiency and provide more space for storing user interfaces, while keep everything easy to use and reduce the cost of learning for users. By doing so, user could still interact in a familiar way with similar user interfaces, with just a minor change.
<div style="text-align:center">
  <img src="https://liangch0505.github.io/images/c667_Motivation1.png" />
</div>
<div style="text-align:center">
  <img src="https://liangch0505.github.io/images/c667_Motivation2.png" /><br>
  <i>When too many windows opened, it's very hard to select the one you want, or interact between two different windows.</i>
</div>
## Characteristics
<b>Low learning cost: </b>  No fancy 3D effect. No additional interaction devices. User still uses mouse to interact with similar user interfaces, just have to press the mouse and realize that interfaces are stacked together.
<b>Low deployment cost: </b> Each sensor costs $2 only. Software can be directly used on Windows systems.
<b>Effective: </b> Interaction can be easier and faster, especially in situations where many windows are opened.
## Images of the Mouse
<div style="text-align:center">
  <img src="https://liangch0505.github.io/images/c667_Mouse1.jpg" /><br>
  <img src="https://liangch0505.github.io/images/c667_Mouse2.jpg" /><br>
  <i>Detailed Circuit: four force sensors are in the top of the figure.</i>
</div>
## Hardware Configuration
4 film pressure resistors are attached to each corner of the mouse, with each one sensing force from 0N to ~20N. All sensors are connected to computer via Arduino. Detailed circuit is as the following:
<div style="text-align:center">
  <img src="https://liangch0505.github.io/images/c667_Circuit.png" /><br>
  <i>Detailed Circuit: four force sensors are in the top of the figure.</i>
</div>
## Software Implementation Detail
Two software applications are created:
### Stacked Windows
This program runs on Windows systems. It organizes and stacked all similar windows together (This is based on the program names. For example: folders (File Explorer), videos (VLC Players), webpages (Chrome), etc.). Thus, it can be considered that all similar windows are organized into a 'cube', where each layer in the cube is a window. User cannot see all windows explicitely, but user should be aware that there are more windows behind the current window so that it can be switched to different windows. To group similar windows, it set the positions and sizes of similar windows to be the same, and change the window focus based on the pressure user applied on the mouse.<br>
This program supports 4 different switching mode: uniform, left-right, top-bottom, and single. Uniform means window switches when user uniformly press the mouse. Left-right and top-bottom means user can either switch backwards (out of screen) by pressing left two sensors or bottom two sensors) or switch forwards (in to the screen) by pressing right two sensors or top two sensors. Single means only one of four sensors is used for pressure sensing. It can be found that uniform and single are easy to operate, but they support only one direction switching. Left-right and top-bottom supports bi-directional switching, but user may have to press only one side of the mouse, which might be a little bit difficult.<br>
A threshold is added to avoid switching to be accidentally activated. This can be changed based on user's habit. For bi-directional switching modes, this threshold is the difference between two groups of sensors.<br>
To provide a smooth control, we mapped the force to the switching speed as shown in the figure below. Thus, if user is trying to hard press the mouse, the switching speed is increased exponentially.<br>
<div style="text-align:center">
  <img src="https://liangch0505.github.io/images/c667_Software_StackedWindows_SwitchingSpeed.png" /><br><br>
  <i>Smaller force for precise control. Larger force for fast switching (because user's purpose is very obvious).</i>
</div>
<br>
All implementation is done with Python. Two packages are used for achieving functionality:

* Pyfirmata: For communication between Python and Arduino
* Pywinauto and win32gui: Automate window control (change focus, position, size, etc)

<br><br>
<b>Demo Videos:</b>

* Basic Switching: [Youtube](https://www.youtube.com/watch?v=yk7EaKMPcWo)
* Drag and drop files while switching: [Youtube](https://www.youtube.com/watch?v=7OA2kFTEiaA)

### Games
TODO
## How it works
### For Stacked Windows:
Imagine if you are working on a large project. You have many folders opened and all of them are important so you cannot close them. You also have many web pages opened for reference. Besides, you are also working with many arduino files, and they are opened in separate windows. At this time, there are some difficulties to interact with these windows: first, it is very hard to drag one file from one folder to another, because you have to firstly find those two windows among a number of opened folders, and then you have to move them to correct positions (i.e. not overlapped so that you can drag files), and this can take a considerable amount of time; second, with many web pages opened, each web page has a very small tab and you cannot see the title of each very well, and you also have a higher chance to accidentally close one of them - because close button takes half of the space of the tab. <br>
With the solution proposed in this project, all these windows will be grouped into only three windows: folders, webpages, and Arduino IDE. User can still view any window he/she wants by just pressing the mouse on the corresponding window to switch, and there are even extra space left for other applications as well. In this scenario, the efficiency can be much improved, as user can easily achieve some interaction among these well-organized windows with some very simple methods, such as pressing the mouse.
## Implementation Challenges

* Bottom of mouse may not be flat, causing some sensors not being pressed. A (Temporary) Solution: add a soft pad below each sensor
* Serial Communication lag. Possible Solution: Get better hardware apparatus
