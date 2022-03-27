![Banner](https://telegra.ph/file/038f8df9ac34a005f1f31.jpg)
Fix your android battery drain by optimization.

# About Optimizer
When you updated or flashed your device, you probably used up a lot of battery power in the first three or four days. The Android system is the first in the list of systems consumed and has 30–40% of the use! This guide will help to eliminate this problem. Starting with Android version 6 and below, you should have seen a message from the system saying "Optimizing app xx from xx" when you flashed or installed new apps.

You can often watch how the Android system consumes energy more than other applications. This is the result of not allowing the system to optimize.
Because optimization was forced in Android 6 and earlier, and it became optional starting with Android 7 and higher, a new option was added to skip this step and optimise applications on the fly (JIT, Just-In-Time) while using applications.
At the same time, the initial optimization has not been deleted and only starts if the following conditions are met:

> the phone is connected to the charger,

> fully charged,

> turned on (the phone itself, not the screen),

> is not used,

> inactive (like after at least 30 minutes).

So if you dirty flash a lot, you might randomly experience longer app launch times after flashing a ROM, and the only apparent way to fix it was to do a clean flash.
I experienced this a few times and decided to investigate and saw that it had something to do with how dex2oat works after you dirty flash (it refuses to optimise properly).
What I found fixed the issue was to manually run dex2oat on everything after it booted into the system, and after it finished the process (which could take a super long time depending on how many apps you have), everything went back to its speedy state.
And it seems to improve idle drain (high battery usage by the system) because we're forcing tasks that can only run if certain conditions are met, but also sometimes happen unexpectedly while the phone is idle, causing huge idle drain usage. 

### How to:

## If you have root/magisk:

1. Open a terminal (e.g termux or terminal on playstore) and enter the following commands (allow the terminal for root in magisk when it asked):

`su -c "cmd package bg-dexopt-job"`

2. Just wait until it is completed by itself (on Android 10+ will display "Success", on Nougat-Pie it will bring just a new prompt line)
![Screenshot](https://telegra.ph/file/7e75e1c0165d99efa87eb.jpg)

## If you don't have root:

> Prepping your phone - 
1. Navigate to settings
2. Go to **System > About Phone > Build number**
3. Tap on **Build Number** 7 times or until you see the *You are now a developer* toast message.
4. Now, Go back to **System > Advanced > Developer options > Enable USB Debugging**
5. Once enabled, Go to your PC

> Running command without script -
1. On your computer, enter the following commands in a console/terminal window:

`adb shell cmd package bg-dexopt-job`

If you don't have adb installed go [here](https://developer.android.com/studio/releases/platform-tools)

# [Download Script](https://github.com/KelvinCrag/Optimizer/releases) [![Github All Releases](https://img.shields.io/github/downloads/kelvincrag/optimizer/total.svg)]()
 

## F.A.Q
1. How do I install the script in **Linux and macOS**?
> You don't. Just manually run the command above in the terminal.

2. How do I install the script in **windows**?
> Simple. Put the script 'optimizer_script.bat' from [releases](https://github.com/KelvinCrag/Optimizer/releases) in the same folder with your installed adb, by default it's c:/adb/platform-tools, then double click to run the script.

3. If I can run the command manually why should I still download the script you made?
> Well, it saves your stress. Instead of typing the command and avoiding misspelt command just run my script.

4. What if I got tired of waiting and stopped the whole thing?
> Disconnecting your phone will abort the process, it is completely safe to interrupt the process.
On non-rooted devices, you might see an error like this "user 2000 nor current process has Android.permission.Update_Device_Stats"

5. Is the error message I received very bad, am I going to lose my data?
> The error is safe to ignore and you don't need to worry. 
If you're concerned you can run that command a second time and the error should not occur during the second run.

6. In Android 7+, did they hide this from the user's eyes or delete it? Does this mean that the optimization has been removed?
> No, this is not such. This option was not lost, but simply postponed, and the postponement of this task causes the battery to run out. Do you think that optimization is happening in the background? The answer is not correct. It only starts under special conditions. The lack of this optimization will drain the battery. Optimization is not performed because we do not know how to fulfil the conditions necessary for its launch. The consequence of this is the accelerated discharge of the phone.
 
7. What can I expect from the Optimization measures?
> Better battery life and performance. The idle drain would be reduced to a minimum.

8. Why do we need this optimization?
> It is because application developers cannot do this for each set of hardware and each device is already. It compiles applications into the most efficient code for its processor. So just use your device and let it take care of the cache itself or help your device make full optimization with simple commands.


Note: You can also do this optimization; after clean flash, after complete restore app from titanium backup/migrate or from Google (Play Store).


### Curious what the code does? See here: [https://android.googlesource.com/platform/frameworks/base.git/+/f7edab63d9358b9a4e0dbec3243f6db9f50a2bbe](https://android.googlesource.com/platform/frameworks/base.git/+/f7edab63d9358b9a4e0dbec3243f6db9f50a2bbe)

credit : 
- Android communities
- Mobiosolutions for banner inspiration 

