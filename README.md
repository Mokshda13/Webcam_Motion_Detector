# Webcam_Motion_Detector
This program allows us to detect motion of an object across the frame and output the time interval of motion.The libraries used are opencv and time.
Videos here are treated as stack of pictures called frames.The intensity values of two frames are compared to detect an object.
### Python Code:
Import the required libraries:
```python
import cv2, time
from datetime import datetime
```
Assign first frame and status list to None and also define an empty 'times' list:
```python
first_frame=None
status_list=[None,None]
times[]
```
Initialize video capture:
```python
video=cv2.VideoCapture(0)
```
Define an infinite while loop to treat stacks of images as video:
```python
while True:
```
Start reading frame(image) from video:
```python
check, frame= video.read()
```
Initialize motion:
```python
status=0
```
Convert color image to gray_scale image:
```python
gray=cv2.cvtColor(frame,cv2.COLOR_BGR2GRAY)
```
Convert gray scale image to GaussianBlur so that change can be found easily:
```python
gray=cv2.GaussianBlur(gray,(21,21),0)
```
Assign the value of first frame:
```python
if first_frame is None:
    first_frame=gray
    continue 
```
Difference between static background and current frame(which is GaussianBlur) :
```python
delta_frame=cv2.absdiff(first_frame,gray)
```
If change in between static background and current frame is greater than 30 programme will show white color(255):
```python
thresh_frame=cv2.threshold(delta_frame,30,255,cv2.THRESH_BINARY)[1]
thresh_frame=cv2.dilate(thresh_frame,None,iterations=2)
```
Find contour of moving object:
```python
(cnts,_)=cv2.findContours(thresh_frame.copy(),cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)
    for contour in cnts:
        if cv2.contourArea(contour)<10000:
            continue
```
Make green rectangle around the moving object:
```python
(x,y,w,h)=cv2.boundingRect(contour)
cv2.rectangle(frame,(x,y),(x+w,y+h),(0,255,0),3)
```
Append status of motion:
```python
status_list.append(status)
```
Append start time of motion:
```python
if status_list[-1]==1 and status_list[-2]==1:
    times.append(datetime.now())
```
Append end time of motion:
```python
if status_list[-1]==0 and status_list[-2]==1:
    times.append(datetime.now())
```
Display image in gray frame:
```python
cv2.imshow("Gray Frame",gray)
```
Display the difference in currentframe to the staticframe(very first_frame):
```python
cv2.imshow("Delta Frame",delta_frame)
```
Display the black and white image in which if intencity difference greater than 30 it will appear white:
```python
cv2.imshow("Threshold Frame",thresh_frame)
```
Display color frame with contour of motion of object 
```python
cv2.imshow("Color Frame", frame) 
```
Stop the whole process if 'q' is entered:
```python
if key==ord('q'):
```
if something is moving then the end time of movement is appended:
```python
if status==1:
    times.append(datetime.now())
break
```
Print all the lists:
```python
print(status_list)
print(times)
```
Destroy all the windows:
```python
cv2.destroyALlWindows
```


    
    


    

    

    




