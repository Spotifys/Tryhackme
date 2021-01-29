## Android Hacking 101
##### Android Mobile Application Penetration Testing


------------

##### Task1
###### Introduction 
No Answer Needed!

------------

##### Task2
###### Setup the environment
No Answer Needed!

------------
##### Task3
###### Methodology
No Answer Needed!

------------
##### Task4
###### Information Gathering


- What is the package name of the Black Hat Europe?

 [![Find With Adb](https://i.ibb.co/7S9QZc7/1.jpg "Find With Adb")](https://github.com/Spotifys/Tryhackme/blob/main/Mobile/Android%20Hacking%20101/README.md "Find With Adb")

OR

[![Find With Google Play Store](https://i.ibb.co/SQV5Sjx/2.jpg "Find With Google Play Store")](https://github.com/Spotifys/Tryhackme/blob/main/Mobile/Android%20Hacking%20101/README.md "Find With Google Play Store")

Answer:
 ```
com.swapcard.apps.android.blackhat
```
------------
##### Task5
###### Reversing


- Tool for convert dex file to smali code?

Answer:
```d2j-dex2smali```

- Which is the option for build apps with apktool?

Answer:

```b```

- What is the apk path of Black Hat Europe?

[![Find With ADB](https://i.ibb.co/t25V1r7/3.jpg "Find With ADB")](https://github.com/Spotifys/Tryhackme/blob/main/Mobile/Android%20Hacking%20101/README.md "Find With ADB")

Answer:

```/data/app/com.swapcard.apps.android.blackhat-1/base.apk```

- Command for extract apk of Back Hat Europe?

Answer:

```adb pull /data/app/com.swapcard.apps.android.blackhat-1/base.apk```

------------
##### Task6
###### Static analysis


- What is the name of the firebase instance in the app Black Hat Europe?

*Find With Mobsf*

[![Find in Mobsf Report](https://i.ibb.co/0VHWy1L/4.jpg "Find in Mobsf Report")](https://github.com/Spotifys/Tryhackme/blob/main/Mobile/Android%20Hacking%20101/README.md "Find in Mobsf Report")

Answer:

```swapcard-android-app-2014 ```


- Android-InsecureBankv2 debug realease, check this and what activity is not Protected.

Answer:

```com.android.insecurebankv2.ChangePassword```

- what is the malicious permissions in the app Android-InsecureBankv2?

Answer:

```android.permission.SEND_SMS```
