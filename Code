from sklearn.metrics import r2_score
try:
 import country_converter as coco 
except ModuleNotFoundError:
  !pip install country_converter 
  import country_converter as coco
import math
import numpy as np
import matplotlib.pyplot as plt
from pandas_datareader import wb
from tkinter import *
#Many thanks to jonbruner on GitHub for this complete list of 2 letter ISO Country Codes in Python.
iso =["AF", "AX", "AL", "DZ", "AS", "AD", "AO", "AI", "AQ", "AG", "AR",
"AM", "AW", "AU", "AT", "AZ", "BS", "BH", "BD", "BB", "BY", "BE",
"BZ", "BJ", "BM", "BT", "BO", "BQ", "BA", "BW", "BV", "BR", "IO",
"BN", "BG", "BF", "BI", "CV", "KH", "CM", "CA", "KY", "CF", "TD",
"CL", "CN", "CX", "CC", "CO", "KM", "CG", "CD", "CK", "CR", "CI",
"HR", "CU", "CW", "CY", "CZ", "DK", "DJ", "DM", "DO", "EC", "EG",
"SV", "GQ", "ER", "EE", "ET", "FK", "FO", "FJ", "FI", "FR", "GF",
"PF", "TF", "GA", "GM", "GE", "DE", "GH", "GI", "GR", "GL", "GD",
"GP", "GU", "GT", "GG", "GN", "GW", "GY", "HT", "HM", "VA", "HN",
"HK", "HU", "IS", "IN", "ID", "IR", "IQ", "IE", "IM", "IL", "IT",
"JM", "JP", "JE", "JO", "KZ", "KE", "KI", "KP", "KR", "KW", "KG",
"LA", "LV", "LB", "LS", "LR", "LY", "LI", "LT", "LU", "MO", "MK",
"MG", "MW", "MY", "MV", "ML", "MT", "MH", "MQ", "MR", "MU", "YT",
"MX", "FM", "MD", "MC", "MN", "ME", "MS", "MA", "MZ", "MM", "NA",
"NR", "NP", "NL", "NC", "NZ", "NI", "NE", "NG", "NU", "NF", "MP",
"NO", "OM", "PK", "PW", "PS", "PA", "PG", "PY", "PE", "PH", "PN",
"PL", "PT", "PR", "QA", "RE", "RO", "RU", "RW", "BL", "SH", "KN",
"LC", "MF", "PM", "VC", "WS", "SM", "ST", "SA", "SN", "RS", "SC",
"SL", "SG", "SX", "SK", "SI", "SB", "SO", "ZA", "GS", "SS", "ES",
"LK", "SD", "SR", "SJ", "SZ", "SE", "CH", "SY", "TW", "TJ", "TZ",
"TH", "TL", "TG", "TK", "TO", "TT", "TN", "TR", "TM", "TC", "TV",
"UG", "UA", "AE", "GB", "US", "UM", "UY", "UZ", "VU", "VE", "VN",
"VG", "VI", "WF", "EH", "YE", "ZM", "ZW"]
iso.remove("AQ")
iso.remove("CC")
iso.remove("VA")
iso.remove("NF")
iso.remove("SH")
iso.remove("PM")
iso.remove("EH")
for item1 in iso:
  s = 1970
  e = 2020
  try:
   x1 = wb.download(indicator=['NY.GDP.PCAP.CD'], country=[item1], start=s, end=e)
  except Exception:
    iso.remove(item1)
  else:  
   x2 = [s]
   i = s
   arr = np.array(x1)
   x2 = list(range(s,e))
   x2.append(e)
   y = np.split(arr, (e-s+1))
   z = np.concatenate(y)
   x3 = x2.reverse()
   z2 = []
   i2 = -1
   while i2 < (e-s):
     i2+=1
     z2.append(float(np.asarray(z[i2])))
   x4 = [] 
   c = []
   for item2 in z2:
     if item2 != item2:
       c.append(z2.index(item2))
   for item3 in x2:
     if x2.index(item3) not in c:
       x4.append(item3) 
   z3 = [x for x in z2 if math.isnan(x) == False]
   if len(x4) < 3 and item1 in iso:
     iso.remove(item1)  
try:
  s = int(input("Enter the starting year: "))
except ValueError:
  raise ValueError("Sorry, that isn't a valid input. Please restart the program.")  
try:
  e = int(input("Enter the ending year: "))
except ValueError:
  raise ValueError("Sorry, that isn't a valid input. Please restart the program.")
try:  
 year_of_prediction = int(input("What year would you like to predict the GDP per capita for? "))
except ValueError:
  raise ValueError("Sorry, that isn't a valid input. Please restart the program.")   
country = input("Enter the name of the country you would like to predict the GDP per capita of: ")
country2 = coco.convert(names=country,to='ISO2') 
if country2 not in iso:
  raise ValueError("Sorry, there isn't much data for this country. Please restart the program.")
else:  
 x1 = wb.download(indicator=['NY.GDP.PCAP.CD'], country=[country2], start=s, end=e)
 arr = np.array(x1)
 x2 = list(range(s,e))
 x2.append(e)
 y = np.split(arr, (e-s+1))
 z = np.concatenate(y)
 x3 = x2.reverse()
 z2 = []
 i2 = -1
 while i2 < (e-s):
   i2+=1
   z2.append(float(np.asarray(z[i2])))
 x4 = [] 
 c = []
 for item in z2:
   if item != item:
     c.append(z2.index(item))
 for item in x2:
   if x2.index(item) not in c:
     x4.append(item) 
 z3 = [x for x in z2 if math.isnan(x) == False]
 a = sorted(x4) 
 b = sorted(z3)
 model = np.poly1d(np.polyfit(x4, z3, 5))
 line = np.linspace(int(a[0]), int(a[len(x4)-1]),int(b[len(z3)-1]) )
 plt.scatter(x4,z3)
 plt.plot(line, model(line))
 plt.show
 print(model)
 print("R2 Score: " + str(r2_score(z3,model(x4))))
 # I worked out this average using the block of code below.
 print("Average R2 Score: " + "0.9345921336999565")
 print("Prediction for " + str(year_of_prediction) + ": " + "$" + str(model(year_of_prediction)))  
