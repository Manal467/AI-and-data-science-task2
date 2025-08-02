# AI-and-data-science-task2  


**Step 1: Import Required Libraries** 

```
import cv2 
import time
import numpy as numpy
```
Import OpenCV library for image/video processing

Import time library to control processing speed

Import numpy for array operations (though not directly used here)

**Step 2: Load Cat Face Classifier**
python
cat_classifier = cv2.CascadeClassifier('haarcascade_frontalcatface.xml')
Create a classifier using the 'haarcascade_frontalcatface.xml' file which contains training data for cat face detection

**Step 3: Initialize Video Capture**
python
cap = cv2.VideoCapture('cats.mp4')
Open the video file 'cats.mp4' for reading

**Step 4: Check if Video Opened Successfully**
python
if not cap.isOpened():
    print("Error: Could not open video.")
    exit()
Verify if the video opened successfully, otherwise print error message and exit

**Step 5: Process Video Frames**
python
while cap.isOpened():
    time.sleep(0.05) 
Start loop to process each video frame

Use time.sleep to slow down processing for better visualization

**Step 6: Read Frame from Video**
python
    ret, frame = cap.read()
    
    if not ret:
        print("Error: could not read frame:")
        break 
Read next frame from video

If reading fails (e.g., at video end), print error and break loop

**Step 7: Convert Frame to Grayscale**
python
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)    
Convert color frame to grayscale as detection algorithm works better on grayscale images

**Step 8: Detect Cat Faces**
python
    cats = cat_classifier.detectMultiScale(gray, 1.4, 2)
Use classifier to detect cat faces in current frame

Parameters:

1.4: Scale factor for image detection

2: Minimum neighbors required to retain a detection rectangle

**Step 9: Draw Rectangles Around Detected Faces**
python
    for (x, y, w, h) in cats:
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 255), 2)
For each detected cat face, draw a yellow rectangle around it on the original frame

**Step 10: Display Output Frame**
python
    cv2.imshow('cats', frame) 
Display the frame with drawn rectangles in a window titled "cats"

**Step 11: Exit on 'q' Key Press**
````
    if cv2.waitKey(1) & 0xFF == ord('q'):
       break
If user presses 'q' key, break out of the loop
```
**Step 12: Release Resources and Close Windows**
```
cap.release()
cv2.destroyAllWindows()
Release video capture resources

Close all OpenCV windows
```
