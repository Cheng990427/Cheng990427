- 👋 Hi, I’m @Cheng990427
- 👀 I’m interested in Emotion Regulation.
- 🌱 I’m currently learning online TMS and TMS's neural mechanisms.
- 📫 How to reach me 1837614420@qq.com; wechat: 13086605790

<!---
Cheng990427/Cheng990427 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
# -*- coding: utf-8 -*-
"""
Created on Wed Jan  5 20:21:22 2022

@author: Administrator
"""

import os
import pandas as pd
import shutil

newpath = NewPath
path= OldPath
os.chdir(path)
EEGdata = os.listdir(path)
global df,Info
df=pd.read_excel(SubjectInfo+GroupInfo.xlsx)
subject = df.iloc[:,0]
Group = df.iloc[:,5]

Info={}
for i in range(len(subject)):
    Info[int(subject[i])]=int(Group[i])
    
# for file in EEGdata:
#     num = int(file[0:3].lstrip("0"))
#     print(num)
#     try:
#         if Info[num]==1 or Info[num]==2:
#             shutil.copy(file, newpath)
#         else:
#             continue
#     except:
#         "Wrong"

# --------- Change File Names ---------- #
for file in EEGdata:
    num = int(file[0:3].lstrip("0").split("_")[0])
    print(num)
    try:
        if Info[num]==1:
            print("Group1")
            oldname=file.split(".")[0]
            newname=str(num)+"_Group1"
            filename=file.replace(oldname, newname)
            os.rename(file,filename)
        elif Info[num]==2:
            print("Group2")
            oldname=file.split(".")[0]
            newname=str(num)+"_Group2"
            filename=file.replace(oldname, newname)
            os.rename(file,filename)
    except:
        print("Wrong")
 
 # --------- Change .vhdr info inside ---------- #      
EEGdata = os.listdir(newpath)
for file in EEGdata:
    if "vhdr" in file:
        f = open(file,'r')
        text=f.read()
        f.close()
        newtext=re.sub("DataFile=(\S+).eeg", "DataFile="+file.split(".")[0]+".eeg",text)
        newtext=re.sub("MarkerFile=(\S+).vmrk", "MarkerFile="+file.split(".")[0]+".vmrk",newtext)
        f = open(file,'w')
        f.write(newtext)
        f.close()
    else:
        continue
 # --------- Change .vmrk info inside ---------- #     
 for file in EEGdata:
    if "vmrk" in file:
        f = open(file,'r')
        text=f.read()
        f.close()
        newtext=re.sub("DataFile=(\S+).eeg", "DataFile="+file.split(".")[0]+".eeg",text)
        f = open(file,'w')
        f.write(newtext)
        f.close()
    else:
        continue
