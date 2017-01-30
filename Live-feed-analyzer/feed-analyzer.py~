

import numpy as np
import cv2
from Tkinter import *
import Image, ImageTk
import copy


#############################################
#
# Control processing function. Can be edited
#
#############################################

frameNumber = 0 # may be used for saving
dataCollection = False

def processFrame(frame):
    global frameNumber
    global dataCollection
    min_YCrCb = np.array([0,133,77], np.uint8)
    max_YCrCb = np.array([255,173,127], np.uint8)    
    
    f1 = copy.deepcopy(frame)
    #f2 = copy.deepcopy(frame)
    ################################# 
    # add custom code after this
    #################################
    
    # Convert image to YCrCb
    imageYCrCb = cv2.cvtColor(f1, cv2.COLOR_BGR2YCR_CB)
    # Find region with skin tone in YCrCb image
    skinRegion = cv2.inRange(imageYCrCb, min_YCrCb, max_YCrCb)
    # Do contour detection on skin region
    contours, hierarchy = cv2.findContours(skinRegion, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    # Draw the contour on the source image
    for i, c in enumerate(contours):
        area = cv2.contourArea(c)
        if area > 2000:
            cv2.drawContours(f1, contours, i, (0, 0, 0), -1) # -1 fills the countour, else you can give outline thinkness
            
    
    gray = cv2.cvtColor(f1, cv2.COLOR_BGR2GRAY)
    ret, final = cv2.threshold(gray, 5, 255, cv2.THRESH_BINARY_INV)
    
    # if data collection mode is true
    if dataCollection:
        cv2.imwrite("data/frame-"+str(frameNumber)+".bmp", final)
        frameNumber = frameNumber + 1
    #################################
    # add custom code before this
    #################################
    return f1, final

#############################################
#
# Control processing function ends here
#
#############################################

#####################################################
#
# Main GUI. DO NOT CHNAGE ANYTHING UNTIL MAIN GUI ends
#
######################################################

window = Tk()  #Makes main window
window.wm_title("Live Feed Experimenter")
window.config(background="#D9D9D9")
window.attributes('-zoomed', True) # set window to maximum


#Capture video frames
cap = cv2.VideoCapture(0)

def show_frame():
    ret, frame = cap.read()
    frame = cv2.resize(frame, (432, 324))
    frame = cv2.flip(frame, 1)
    # all processing is done here
    f1, f2 = processFrame(frame)
    # display image
    img1 = Image.fromarray(frame)
    imgtk1 = ImageTk.PhotoImage(image=img1)
    
    img2 = Image.fromarray(f1)
    imgtk2 = ImageTk.PhotoImage(image=img2)
    
    img3 = Image.fromarray(f2)
    imgtk3 = ImageTk.PhotoImage(image=img3)    
    
    display1.imgtk = imgtk1 # Show the live feed
    display1.configure(image=imgtk1)
    
    display2.imgtk = imgtk2 # Show the processed feed
    display2.configure(image=imgtk2)
    
    display3.imgtk = imgtk3 # Show the processed feed
    display3.configure(image=imgtk3)
    
    window.after(10, show_frame) 

# Application heading label
mainLabel = Label(window, text="Live Feed Experimenter\nSend bugs or crash reports to human.divanshu@gmail.com with screenshot")
mainLabel.grid(row=0, column=0, columnspan=6)
Label(window, text="Input Feed").grid(row=1, column=0, columnspan=2, pady=2)
Label(window, text="Hand Detect").grid(row=1, column=2, columnspan=2, pady=2)
Label(window, text="Output Feed").grid(row=1, column=4, columnspan=2, pady=2)


# will show the live feed
display1 = Label(window)
display1.grid(row=2, column=0, columnspan=2, pady=2)  # on left side
# will show the processed feed
display2 = Label(window)
display2.grid(row=2, column=2, columnspan=2, pady=2) # on right side

display3 = Label(window)
display3.grid(row=2, column=4, columnspan=2, pady=2) # on right side

#############################################
#
# Main GUI ends. DONOT CHANGE BEFORE THIS
#
#############################################

show_frame() #Display
window.mainloop()  #Starts GUI
