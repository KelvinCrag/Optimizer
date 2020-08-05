# Optimizer
Fix your android battery drain by optimization.

## Summary
Probably you have been faced with high battery consumption in the first 3-4 days after updating or flashing your device, the android system is the first in the list of consumption and has 30-40% of use! This guide will help to remove this problem.
It should be after flashing or installing updates on older versions of Android starting from 6 and below.
You have encountered such a system dialog as "Optimizing app xx from xx"

You can often watch how the Android system consumes energy more than other applications. This is the result of not allowing the system to optimize.
If in Android 6 and earlier optimization was forced, then starting with Android 7 and higher. A new option was added to skip this step and optimize applications on the fly (JIT, Just-In-Time) while using applications.
At the same time, the initial optimization has not been deleted and only starts if the following conditions are met:

> the phone is connected to the charger,

> fully charged,

> turned on (the phone itself, not the screen),

> is not used,

> inactive (like after at least 30 minutes).


If these conditions are met, optimization begins.

## Quick note
If you dirty flash a lot you might randomly experience longer app launch times after flashing a ROM and the only apparent way to fix it was to do a clean flash.
I experienced this a few times and decided to investigate and saw that it had something to do with how dex2oat works after you dirty flash (it refuses to optimise properly?). 

What I found fixed the issue was to manually run dex2oat on everything after it booted into the system, and after it has finished the process (could take super long depending on how many apps you have), everything went back to its speedy state.

(And it seems improve idle drain (big battery usage by system), because we're forcing doing task that only can run if some condition only, but also sometimes can unexpectedly happens while phone was idle, so it's causing huge idle drain usage)

### How to:
<p>
<details>
<summary>If you have root/magisk:</summary>

1. Open terminal and enter the following commands (allow the terminal for root in magisk when it asked):


su -c "cmd package bg-dexopt-job"


2. Just wait until it completed by itself (on Android 10 will display "Success", on Nougat-Pie it just a new prompt line)
</details>
</p>

<p>
<details>
<summary>If you don't have root:</summary>

> Prepping your phone - 

1. Navigate to settings

2. Go to **System > About Phone > Build number**

3. Tap on **Build Number** 7 times or until you see the *You are now a developer* toast message.

4. Now, Go back to **System > Advanced > Developer options > Enable USB Debugging**

5. Once enabled, Go to your PC


> Running command -

1. On your computer, enter the following commands in a console/terminal window:

adb shell
cmd package bg-dexopt-job


If you don't have adb installed go [here](https://developer.android.com/studio/releases/platform-tools)

## F.A.Q

- How do I install the script in **linux and MacOS**?
> You don't. Just manually run the command above in terminal.

- How do I install the script in **windows**?
> Simple. Put the script 'optimizer_script.bat' from [releases](https://github.com/KelvinCrag/Optimizer/releases) in the same folder with your installed adb, by default it supposed to be c:/adb/platform-tools
</details>
</p>

## F.A.Q

- If I can run the command manually why should I still download the script you made?
> Well, it saves your stress. Instead of typing the command and avoiding misspelled command just run my script.

- What if I got tired waiting and stopped the whole thing?
> Disconnecting your phone will abort the process, it is completely safe to interrupt the process.
On non-rooted devices you might see an error like this "user 2000 nor current process has Android.permission.Update_Device_Stats"

- Is the error massage I received very bad, am I going to lose my data?
> The error is safe to ignore and you don't need to worry. 
If you're concerned you can run that command a second time and the error should not occur during the second run.

- In Android 7+, did they hide this from the user's eyes or delete it? Does this mean that the optimization has been removed?
> No, this is not such. This option was not lost, but simply postponed, and the postponement of this task causes the battery to run out. Do you think that optimization is happening in the background? The answer is not correct. It only starts under special conditions. Lack of this optimization will drain the battery. Optimization is not performed because we do not know how to fulfil the conditions necessary for its launch. The consequence of this is the accelerated discharge of the phone.
 
- What can I expect from the Optimization measures?
> Better battery life and performance. Idle drain would be reduced to minimal.

- Why do we need this optimization?
> It is because application developers cannot do this for each set of hardware and each device is already. It compiles applications into the most efficient code for its processor. So just use your device and let it take care of the cache itself or help your device make full optimization with simple command.


Note : You can also do this optimization; after clean flash, after complete restore app from titanium backup/migrate or from Google (Play Store).


## Curious what the code does? See here: https://android.googlesource.com/platform/frameworks/base.git/+/f7edab63d9358b9a4e0dbec3243f6db9f50a2bbe

credit : 
- tomascus @ xda-developers
- TomHenson @ mi community
- anupritaisno1 @ https://forums.oneplus.com/threads/charging-battery-performance-caches-and-battery-calibration-myths-busted.993896/


