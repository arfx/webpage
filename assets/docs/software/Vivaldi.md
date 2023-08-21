# Vivaldi

#Vivalid #learn 

## Multiple Desktop Icons in taskbar

I would like to share my current workaround:

1.  Create profile desktop shortcut (chrome://settings/manageProfile)
2.  Use created shortcut to open Vivaldi using specified profile
3.  Pin it <u>opened Vivaldi Taskbar Icon </u>to taskbar
4.  Close the browser
5.  Right click on Desktop shortcut
6.  Save Target to notepad (for example C:\Users%USERPROFILE%\AppData\Local\Vivaldi\Application\vivaldi.exe --profile-directory="Profile 1")
7.  Click on Change Icon and save the path to notepad (for example: %USERPROFILE%\AppData\Local\Vivaldi\User Data\Profile 1\Vivaldi Profile.ico)
8.  Shift + right click on pinned taskbar icon created in step 2
9.  Select Properties
10.  Adjust Target to step 6
11.  Click on Change icon and paste the path from step 7
12.  Open Task Manager and restart Windows Explorer (Right click -> Restart)

https://forum.vivaldi.net/topic/42397/profile-icons-on-taskbar/35?lang=de


---

I managed to solve this case as well with the following workaround:

-   Go to Vivaldi's program folder and open vivaldi.exe, without command line parameters.
-   Pin this icon.
-   Close Vivaldi.
-   Shift + Right click icon, choose Properties.
-   In Shortcut --> Target, after "vivaldi.exe", add --profile-directory="Profile 1". Click OK. You should now have a pinned taskbar shortcut that opens Vivaldi on profile 1, without generating a new icon.
-   Repeat for "Profile 2" etcetera that you want pinned shortcuts for.
Hope this helps someone else!

FWIW, in Chrome version 88 this works perfectly without any workarounds. So I don't know if the real bug is in Windows or in Vivaldi, but it seems like it should be fixable in the browser.