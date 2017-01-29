#Sign Language to Speech

Written in Python 2.7 is a combination of scripts that aim at converting any sign language to speech.

Current focus is on detecting sign language alphabets and using them to generate simple words that can be converted to speech.

# Scripts

- Live feed analyzer
    Module written using OpenCV2 and NumPy to analyze the live video feed from any camera and detect skin to track hands. This modules is also used to collect data to train the neural network for prediction later on. Read the documentation in Live feed analyzer directory for more information.

- Neural network
    Module written using PyBrain to make predections using the image data collected by Live feed analyzer and predict about the character/gesture that will be used to make word/sentence.

- Text to Speech
