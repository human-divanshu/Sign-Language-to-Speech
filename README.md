#Sign Language to Speech

Written in Python 2.7 is an implementation of Open Sign Language to Speech Architecture that we are trying to build at Thapar University. The aim to develop an open archicture that people from different countries will be able to train to convert their native sign language into speech/text.

Current focus is on detecting sign language alphabets and using them to generate simple words that can be converted to speech.

# Main modules

- Live feed analyzer (Written in OpenCv2 + NumPy)
--Simple script to play around and experiment with live video feed. It has a processFrame function which already detect hands and you can add/edit code to try different things.
--This script can also be used to save frames just by changing a boolean value saveFrame to True from False.
--Download the code and read it. It is well documented.

-Neural network (Written in PyBrain)
Module written using PyBrain to make predections using the image data collected by Live feed analyzer and predict about the character/gesture that will be used to make word/sentence.

- Text to Speech
