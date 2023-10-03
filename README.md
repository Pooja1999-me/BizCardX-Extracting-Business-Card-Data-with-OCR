# BizCardX-Extracting-Business-Card-Data-with-OCR
This project was done through google colab

# Installing required packages

pip install streamlit
pip install streamlit_option_menu
pip install easyocr

# Installing the required libraries

import easyocr
import cv2
import pandas as pd
import re
import sqlite3
import base64
import streamlit as st
from streamlit_option_menu import option_menu

# Image processing

1. read the image
2. resize the image
3. converting color to gray scale image
4. set threshold value brefore passing to OCR Engine
   
img = cv2.imread(image)
orig_img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
rect,thresh_image = cv2.threshold(orig_img,70,255,cv2.THRESH_TOZERO)

# Extracting the data from image

Extract the data from image using easyocr using following command : 

reader = easyocr.Reader(['en'], gpu=False)
res=reader.readtext(thresh_image,detail=0,paragraph=True)

# To store the data in to sql server

1. creating a table in sqlserver by connecting python with with sql database using sqlite3
2. create string using result
3. retrive the the pericular entity like,phone no,email-id,address etc by using regular expressions
emails = re.findall(r'[A-Za-z0-9\.\-+_]+@[A-Za-z0-9\.\-+_]+\.[a-z]+', text)
4. convert the image to binary form by using base64 to store the image in sql server
5. store the retrieved data to table
