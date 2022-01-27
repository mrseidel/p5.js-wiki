# Terminal

To run a local server on your computer, you are first going to want to become familiar using the command line interface or terminal. The terminal provides "shell" access to your computer or a more native access to your computer without abstractions given by the GUI. You can browse directories and execute applications, much like with Finder or file explorer, but via text-based commands.

Terminal also gives you access to many command line applications that you might need for development such as node, npm, git , python, etc. This guide will be an introduction to the basics of command line interface. This guide is not a guide on the above mentioned command line applications.

On Macs, you can find the Terminal app in Applications->Utilities->Terminal; on Windows, go to the start menu and search for "command prompt"; on Linux, you can use the keyboard shortcut Ctrl+Alt+T. Run it and you'll see something like.

![Terminal](https://raw.githubusercontent.com/wiki/lmccart/itp-creative-js/images/terminal.png)

The blinking cursor is the "prompt", where you can execute a command. Here is a list of some common commands you'll need.

- cd - change directory. The following, for example, will set the current path to your desktop. You'll want to replace "shiffman" with your username. cd /Users/shiffman/Desktop.
- pwd - print working directory. This will print out the current directory.
- ls - list the contents of the current directory.

This is barely scratching the surface of [what you can do with unix commands](http://mally.stanford.edu/~sr/computing/basic-unix.html). Allison Parrish's class also has [a tutorial about using unix commands to manipulate text data](http://www.decontextualize.com/teaching/rwet/introduction-and-unix-tutorial/). There are a myriad of things you can do with the command line so keep exploring!

# A couple more terminal tips

- On Macs and Windows, if you don't feel like typing a long path to a directory on your computer, you can get to it quickly by dragging a folder from the finder or file explorer, into terminal. It'll magically transform into the path!
- You can also "auto-complete" directories and filenames using TAB.
- You can repeat previous commands by using the up and down arrow keys.

(Tutorial via Dan Shiffman.)