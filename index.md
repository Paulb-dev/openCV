### Welcome to my GitHub Page

### Data
If you want to train your own haar cascades for openCV or Tensorflow you will need a lot of data (images).
There are a lot of methods to get this data. I recommend to use google or you can make your own images with any cam.
If you want to get this data from Google I recommend to use the "Fatkun downloader". 

Fatkun downloader url = "https://chrome.google.com/webstore/detail/fatkun-batch-download-ima/nnjjahlikiabnchcpehcpkdeckfgnohf?hl=de"
    
### Training
    If you get your data (images) you are ready to train your cascade. 
    A simple method  to use is the "Cascade Trainer GUI", you can find a documentation on there own website.

Cascade Trainer GUI url = "https://amin-ahmadi.com/cascade-trainer-gui/"

```markdownd
```python
import cv2
import numpy as np

path = "path of cascade"
cameraNo = 0 //camera port
objectName = "" //object name
frameWidth = 640 //frame width
frameHeight = 480 //frame height
color = (255,0,255) //color

cap = cv2.VideoCapture(cameraNo)
cap.set(3, frameWidth)
cap.set(4, frameHeight)

def empty(a):
    pass
cv2.namedWindow('Result')
cv2.resizeWindow('Result', frameWidth, frameHeight+100)
cv2.createTrackbar('Scale','Result', 400,1000,empty)
cv2.createTrackbar('Neig','Result', 8, 20, empty)
cv2.createTrackbar('Min Area','Result', 0, 100000, empty)
cv2.createTrackbar('Brightness','Result', 180, 255, empty)

cascade = cv2.CascadeClassifier(path)

while True:
    cameraBrightness = cv2.getTrackbarPos('Brightness','Result')
    cap.set(10, cameraBrightness)
    success, img = cap.read()
    img = cv2.rotate(img, cv2.ROTATE_180)
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    scaleVal = 1+ (cv2.getTrackbarPos('Neig','Result')/1000)
    neig = cv2.getTrackbarPos('Neig','Result')
    objects = cascade.detectMultiScale(gray,scaleVal,neig)
    for (x,y,w,h) in objects:
        area = w*h
        minArea = cv2.getTrackbarPos('Min Area','Result')
        if area > minArea:
            cv2.rectangle(img,(x,y),(x+w,y+h),color,2)
            cv2.putText(img, objectName, (x,y), cv2.FONT_HERSHEY_SIMPLEX , 1, (255,0,0), 2, cv2.LINE_AA)
            roi_color = img[y:y+h,x:x+w]
    cv2.imshow('Result',img)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```
### Result
If you have trained  your model you can test it with the python code above.

If you get any errors you can try this:
```
1.|check that python is installed
2.|python -m pip install --upgrade pip
3.|pip install opencv-python
```
![image](https://i.ytimg.com/vi/su3pHwPyrVY/maxresdefault.jpg)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Paulb-dev/openCV/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
