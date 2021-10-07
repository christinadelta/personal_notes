## Install Mex-File Plug-in for Fast MATLAB Port I/O


These steps will probably work only on windows (if they wotk).

### Step 1:
Log in as a user with Administrator rights.

### Step 2:
Disable UAC (User Account Control).  An easy way to do this in Windows Vista is to: Start-Run-MSCONFIG. Select the Tools tab, scroll down to the option for "Disable UAC" and select it. Next, press the "Launch" button. You must then RESTART the system for this change to take effect.

I am not sure if this step is needed. Will take a look at it.

### Step 3:
Download and copy the [inpoutx64.dll](http://apps.usd.edu/coglab/psyc770/IO64.html) file to the C:\WINDOWS\SYSTEM32 directory.

### Step 4:
Download the [io64.mexw64, config_io.m, inp.m and outp.m](http://apps.usd.edu/coglab/psyc770/IO64.html) files to a working directory of your choice. This directory will be added to your MATLAB path in step-6 below.

### Step 5:
Start MATLAB in ***Run as Administrator*** mode (Right-click icon and select "Run as Administrator").

### Step 6:
Add the directory containing the downloaded m-files to your MATLAB path via the *File/SetPath/AddwithSubfiles*... menu command.

### Step 7:
Run **config_io** from the MATLAB command window.  If there's no error message at this point, you've successfully installed the software.

### Step 8:
<span style="text-decoration: underline">Optional</span>: If you need to re-enable UAC (User Account Control), follow the instructions in step-2 but select "Enable UAC" instead of "Disable UAC".

### Step 9:
 Test the status of a single input line using the bitget() function:
 
 ```
% Read current value of an input port at the specified address.
% Note that the value returned by inp(address) is coerced into an 8-bit format using uint8.

response = uint8(inp(address));

% Take some action if the least-significant-bit is currently at logical-0 level
if (bitget(response,1) == 0)
   display('Input is active')
end

```
