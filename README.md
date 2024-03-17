# virtual-try-on
import os
import cvzone
import cv2
from cvzone.PoseModule import PoseDetector
cap = cv2.VideoCapture(0)
detector = PoseDetector()
shirtFolderPath = "Resources/Shirts"
listShirts = os.listdir(shirtFolderPath)
print(listShirts)
fixedRatio = 400/184 # widthOfShirt/widthOfPoint11to12
shirtRatioHeightWidth = 475/480
imageNumber = 0
imgButtonRight = cv2.imread("Resources/button.png", cv2.IMREAD_UNCHANGED)
imgButtonLeft = cv2.flip(imgButtonRight, 1)
counterRight = 0
counterLeft = 0
selectionSpeed = 10

while True:
 success, img = cap.read()
 img = detector.findPose(img)
 lmList, bboxInfo = detector.findPosition(img, bboxWithHands=False,draw=False)
 if lmList:
  #center = bboxInfo["center"]
  lm11 = lmList[11][1:3]
  lm12 = lmList[12][1:3]
  #print(lmList[11][0:3])
  imgShirt = cv2.imread(os.path.join(shirtFolderPath,listShirts[imageNumber]), cv2.IMREAD_UNCHANGED)

  widthOfShirt = int((lm11[0] - lm12[0]) * fixedRatio)
  print(widthOfShirt)
  imgShirt = cv2.resize(imgShirt, (widthOfShirt,int(widthOfShirt * shirtRatioHeightWidth)))
  currentScale = (lm11[0] - lm12[0]) / 184
  offset = int(44 * currentScale), int(48 * currentScale)
  try:
   img = cvzone.overlayPNG(img,imgShirt,(lm12[0]-offset[0],lm12[1]-offset[1]))
  except:
    pass
  imgButtonLeft1 = cv2.resize(imgButtonLeft, (0,0),None,0.5,0.5)
  imgButtonRight1 = cv2.resize(imgButtonRight, (0, 0), None, 0.5, 0.5)
  img = cvzone.overlayPNG(img, imgButtonRight1, (500, 293))
  img = cvzone.overlayPNG(img, imgButtonLeft1, (72, 293))
  if lmList[16][1] < 100:
      counterRight += 1
      cv2.ellipse(img, (100, 330), (33, 33), 0, 0,counterRight * selectionSpeed, (0, 255, 0), 20)
      if counterRight * selectionSpeed > 360:
          counterRight = 0
          if imageNumber < len(listShirts) - 1:
              imageNumber += 1
  elif lmList[15][1] > 400:
      counterLeft += 1
      cv2.ellipse(img, (540, 330), (33, 33), 0, 0,counterLeft * selectionSpeed, (0, 255, 0), 20)
      if counterLeft * selectionSpeed > 360:
          counterLeft = 0
          if imageNumber > 0:
              imageNumber -= 1
  else:
    counterRight = 0
    counterLeft = 0

 cv2.imshow("image", img)
 cv2.waitKey(1)
