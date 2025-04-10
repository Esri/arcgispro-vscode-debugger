# ArcGIS Pro Debugger Extension for Visual Studio Code

![esri_logo](https://github.com/user-attachments/assets/7bcc0bc8-25b3-442a-9920-f8d364870e9b)

> [!IMPORTANT]
> This extension is designed for ArcGIS Pro 3.5, which will release mid-2025. This extension will be avaialble
> on the VS Code Marketplace at the same time as the Pro release.

## About the Extension

This extension allows debugging ArcGIS Pro script tools (.atbx, .pyt) using Visual Studio Code (VSC).

Our aim is to provide developers a seamless workflow to attach VSC to the Python process live in 
ArcGIS Pro. This integration allows developers to leverage VSC's native Python debugging experience while developing
script tools for ArcGIS Pro.

## Features
- Easily attach to ArcGIS Pro and stand-alone Python processes
- Debug ArcGIS Pro Script Tools (.atbx) and Python Toolboxes (.pyt)
- Debug code on the local machine or remotely on a different machine

## Installation

1. Install the latest ArcGIS Pro Debugger extension from the VSC **Marketplace**:  
2. After the extension is installed, you may need to reload Visual Studio Code to activate the extension.  
   You can do this by using the **Command Palette** (Ctrl+Shift+P) and selecting **Developer: Reload Window**.  

    **Note:** You may see popups indicating the directory where ArcGIS Pro is installed and the Python interpreter path. Additionally, an **ArcGIS Pro Debugger** item will appear in the status bar (bottom-right of VSC).  
    ![image](https://github.com/user-attachments/assets/bc52f17a-fe0e-42e6-b9d7-4f3f74dd8f99)  

## Getting around

The ArcGIS Pro Debugger item in the status bar (bottom-right of VSC) is your main point of entry into controlling the ArcGIS Pro Debugger.

![image](https://github.com/user-attachments/assets/1c6e2457-7748-439d-93bf-969765a177cf)

Hovering over the status bar icon reveals at-a-glance details about the current status of the debugger.

![image](https://github.com/user-attachments/assets/81ff0d17-f8d3-4ef0-9711-28b222bd7b81)

- Click the **help** link on the top-right to get to the GitHub repository page you are reading from now.
- **Debug Mode**: Indicates whether the [ArcGIS Pro debug mode](#arcgis-pro-debug-mode) is currently **On** or **Off**.
- **Attachment Mode**: Indicates whether the [attachment mode](#attachment-mode) is currently **Process ID** or **Port**. This will also show the process or port currently attached to when attached.

Clicking the ArcGIS Pro Debugger item in the status bar will reveal available commands (a dropdown will appear at the top-middle of VSC).

![image](https://github.com/user-attachments/assets/ae422651-b799-43cd-83d4-5a80f567865a)

- **Attach Debugger to ArcGIS Pro**: Attach the debugger to ArcGIS Pro. See [local debugging](#local-debugging) and [remote debugging](#remote-debugging) for usage.
- **Remote Development**: Set an SSH host and make an SSH connection to the remote machine. See [remote debugging](#remote-debugging) for usage.
- **Set Attachment Mode**: Set the [attachment mode](#attachment-mode) to either **Process ID** or **Port**.
- **Set ArcGIS Pro Debug Mode**: Set the [ArcGIS Pro debug mode](#arcgis-pro-debug-mode) to either **On** or **Off**.

## ArcGIS Pro Debug mode

> [!IMPORTANT]  
> The ArcGIS Pro Debug Mode must be enabled in order to successfully attach to ArcGIS Pro.

1. **Open VSC**
2. **Enable or Disable ArcGIS Pro Debug Mode**
    1. Press `Ctrl+Shift+P` to open the command pallette
    2. Run the command **ArcGIS Pro Debugger: Set ArcGIS Pro Debug Mode**
    3. Select **"ON"** if starting a new debugging session.  
       Select **"OFF"** if ending an existing debug session.  

       **NOTE:** A checkmark bubble on the ArcGIS Pro icon in the status bar indicates the debug mode is currently **ON**. You can also use the hover tooltip to confirm the current state.  
       ![image](https://github.com/user-attachments/assets/c657b2c9-4e71-4aaf-9df7-f6e2800c5140)  

       **NOTE:** Attaching to ArcGIS Pro will fail when "OFF".

       **NOTE:** While "ON", you may notice a decrease in performance of ArcGIS Pro. We recommend always setting to "OFF" when you are done debugging.

## Attachment Mode

## Local Debugging

Debug your scripts on your own machine as you develop your script tool.

> [!IMPORTANT]  
> - Requires VSC and the following additional extensions:
>    - ArcGIS Pro Debugger
> - Requires ArcGIS Pro >= 3.5

1. **Open your script tool in ArcGIS Pro**:
    1. Open your ArcGIS Pro project (.aprx)
    2. Open the tool you are debugging
2. **Open VSC**
3. **Open your project folder in VSC**:  
    1. From the menu select **File** > **Open Folder**  

    **NOTE:** This will generate a `.vscode` folder in that workspace (if it is not already there). This folder will be populated with settings injected by the extension.  

    **NOTE:** You must have read/write-permission to this workspace. You may need to start VSC as administrator.  
4. **Open your script in VSC and set breakpoints**: 
    1. In VSC, open the `.py` file associated with your `.atbx`, or the `.pyt` file, that you wish to debug.
    2. Set breakpoints as needed.

    **NOTE:** For script tools (`.atbx`), some additional setup might be required to [debug execution code](#debug-script-tool-execution-code) or [validation code](#debug-script-tool-validation-code). No additional setup is required for python toolboxes (`.pyt`).
5. **Set Python interpreter**:
    1. Press `Ctrl+Shift+P` to open the command palette
    2. Choose **Python: Select Interpreter**
    3. Select the currently active ArcGIS Python interpreter from the dropdown  

    **NOTE:** You can alternatively click the **Python Interpreter** element in the status bar (bottom) of VSC to select the interpreter.  

    **NOTE:** It could be `arcgispro-py3` or a clone of it. Use the **Package Manager** in ArcGIS Pro to determine the active environment.
68. **Set ArcGIS Debug Mode to ON**
    1. See [Enable ArcGIS Pro Debug mode](#enable-arcgis-pro-debug-mode)
7. **Open the Debug Console**: 
    1. From the menu choose **View > Debug Console**.  

    **NOTE:** The debug console opens. Debug messages from the ArcGIS Pro debugger extension will appear here.  
8. **Attach to a running ArcGIS Pro instance using process ID**:  
    1. Press `Ctrl+Shift+P` to open the command pallette
    2. Run the command **ArcGIS Pro Debugger: Attach Debugger to ArcGIS Pro**
    3. Select the ArcGIS Pro process from the dropdown  
    4. If you have multiple workspaces open in the Explorer tab, select the current workspace from the dropdown list.  

    **NOTE:** You will see attaching messages appear in the **Debugger Console**.  

    **NOTE:** Once attached, the **Debug Toolbar** should appear with a socket icon indicating that you are attached and debugging.  

    **NOTE:** If you have not opened a script tool (in ArcGIS Pro), attaching will fail (more precisely, if the Python environment has not been initialized in ArcGIS Pro, there is no Python.exe process to attach to, see https://pro.arcgis.com/en/pro-app/latest/arcpy/get-started/activate-an-environment.htm)

    **NOTE:** Alternatively, you can also click on the **ArcGIS Pro Debugger** item in the status bar to perform this action.
9. **Debugging your script**:  
    1. Run the `.atbx` or `.pyt` script from ArcGIS Pro. The execution will pause at the breakpoints set in VSC, allowing you to debug the script.  

## Remote Debugging

Debug your script tool while it is running on another machine (of your coworker, for example). It may be easier to debug this way than attempting to reproduce the conditions in which the script is failing on your own machine.

> [!IMPORTANT]  
> _On the local (client, initiating) machine_
> - Requires VSC and the following additional extensions:
>    - ArcGIS Pro Debugger
> - Requires OpenSSH Client  
>
> _On the remote (host, target) machine_
> - Requires VSC and the following additional extensions:
>    - ArcGIS Pro Debugger
> - Requires OpenSSH Server
> - Requires ArcGIS Pro >= 3.5

1. **Start the SSH service:**  
    _On the remote machine_
    1. Open the PowerShell as administrator
    2. Run `Start-Service sshd`  

    **NOTE:** When you no longer need the SSH service, run `Stop-Service sshd`.  

    **NOTE:** You can run `Get-Service -Name sshd` to confirm service is running or stopped.  

    **NOTE:** Keep the PowerShell open, you will use it in the next step.
2. **Find the hostname or IP address of your remote machine:**  
    _On the remote machine_
    1. Run the command `hostname` and note the name  
    -or-  
    2. Run the command `ipconfig` and note the IPv4 address (formatted `X.X.X.X`, where each `X` is a number between 0 and 255).  

    **NOTE:** You will use either the host name or the IP address to make an SSH connection from your local to your remote machine.  
3. **Set up a remote listening port for debugpy in your ArcGIS Pro session:**  
    _On the remote machine_  
    1. Open your ArcGIS Pro project (.aprx)  
    2. Open the Python Window  
    3. Run the following code:
    ``` python
    import os, debugpy
    debugpy.configure(python=os.path.join(sys.prefix, "python.exe"))
    debugpy.listen(<port>)
    ```
    
    **NOTE:** Replace `<port>` with an open port, for example, try `5678`.  

    **NOTE:** If successful, you should see something like `('123.0.0.4', 5678)` printed to the output. **IMPORTANT:** This is not the same as the IP address obtained earlier.  
4. **Open VSC** _on the local machine_
5. **Select the ArcGIS Pro Debugger configuration type:**  
    _On the local machine_  
    1. Press `Ctrl+Shift+P` to open the command palette  
    2. Select **ArcGIS Pro Debugger: Select Configuration Type**  
    3. Choose **Attach using Port**  

    **NOTE:** The default configuration is **Attach using Process ID**, this is recommended for local debugging. For remote debugging, **Attach using Port** is recommended.
6. **Add an SSH host (skip if this was already done previously):**  
    _On the local machine_  
    1. Press `Ctrl+Shift+P` to open the command palette  
    2. Select **ArcGIS Pro Debugger: Remote Development**  
    3. Select **Add New SSH Host...**
    4. Enter the host name or IP address noted earlier and press enter
    5. Choose an option for how SSH host configuration is stored (select first option if unsure)  

    **NOTE:** Once connected, you will see SSH: <hostname/IP> on the lower left of the status bar. You can now open and edit scripts remotely.  

    **NOTE:** Alternatively, you can also click on the ArcGIS Pro Debugger in the status bar to perform this action.  
7. **Make an SSH connection:**  
    _On the local machine_  
    1. Press `Ctrl+Shift+P` to open the command palette  
    2. Select **ArcGIS Pro Debugger: Remote Development**  
    3. Select the remote machine from the list  
    4. Select the remote machine operating system from the list  

    **NOTE:** A separate VSC instance may open, continue there with all steps going forward  
    5. Enter the password and press enter  

    **NOTE:** This instance (window) of VSC is now accessing the remote machine.  
8. **Ensure all necessary components are installed on remote machine**  
    _On the local machine_  
    1. Click the Extensions tab and make sure the ArcGIS Pro Debugger extension components are installed on the SSH host  

    **NOTE:** From the Extensions tab you will see extensions installed on the remote machine. This tab will also show you extensions that are missing on the remote machine, make sure the required extensions are installed on the remote machine before proceeding (refer to the list of required extensions provided earlier). For the ArcGIS Pro Debugger extension item in the list, you may have to click on the **Install in SSH:<hostname/IP>** to install required components.  
7. **Open the remote project folder**:  
    _On the local machine_  
    **NOTE: You may skip this step if you already have a folder opened  
    1. From the menu select File > Open Folder. You can alternatively do this from the **Explorer** tab.  

    **NOTE:** The drop-down list shows folders on the remote machine  
    2. Select the project folder containing the scripts you want to debug 
    3. If prompted, re-enter the password  

    **NOTE:** From the **Explorer** tab you will see the directory tree of the remote machine. You can now open and edit scripts remotely.  

    **NOTE:** This will generate a `.vscode` folder in that workspace (if it is not already there). This folder will be populated with settings injected 
by the extension.  

    **NOTE:** You must have read/write-permission to this workspace. You may need to start VSC as administrator.  
8. **Open your script**:  
    _On the local machine_  
    1. In VSC, open the `.py` file associated with your `.atbx`, or the `.pyt` file, that you wish to debug.  

    **NOTE:** For script tools (`.atbx`), some additional setup might be required _on the remote machine_ to [debug execution code](#debug-script-tool-execution-code) or [validation code](#debug-script-tool-validation-code). No additional setup is required for python toolboxes (`.pyt`).  
9. **Set Python interpreter**:  
    _On the local machine_  
    1. Press `Ctrl+Shift+P` to open the command palette
    2. Choose Python: Select Interpreter
    3. Select the currently active ArcGIS Python interpreter (of the remote machine) from the dropdown  

    **NOTE:** You can alternatively click the **Python** element in the status bar (bottom) of VSC to select the interpreter.  

    **NOTE:** It could be `arcgispro-py3` or a clone of it. Use the Package Manager in ArcGIS Pro _on the remote machine_ to determine the active environment.  
10. **Open the Debug Console**: 
    1. From the menu choose **View > Debug Console**.  

    **NOTE:** The debug console opens. Debug messages from the ArcGIS Pro debugger extension will appear here.  

    **NOTE:** Alternatively, you can also click on the **ArcGIS Pro Debugger** in the status bar to perform this action.  
12. **Attach to a running ArcGIS Pro instance using a debug port**:  
    _On the local machine_  
    1. Press `Ctrl+Shift+P` to open the command palette
    2. Run the command **ArcGIS Pro Debugger: Attach Debugger to ArcGIS Pro**
    3. Enter the port number you chose in an earlier step  
    4. If you have multiple workspaces open in the Explorer tab, select the current workspace from the dropdown list.  

    **NOTE:** You should begin to see messages appear in the debug console. Once successfully attached, the debug toolbar should appear with a socket icon indicating that you are attached and debugging.  

    **NOTE:** Once attached, the **Debug Toolbar** should appear with a socket icon indicating that you are attached and debugging.  

    **NOTE:** If you have not opened a script tool (in ArcGIS Pro), attaching will fail (more precisely, if the Python environment has not been initialized in ArcGIS Pro, there is no Python.exe process to attach to, see https://pro.arcgis.com/en/pro-app/latest/arcpy/get-started/activate-an-environment.htm)

    **NOTE:** Alternatively, you can also click on the **ArcGIS Pro Debugger** in the status bar to perform this action.  
14. **Run your script tool in ArcGIS Pro**:  
    _On the remote machine_  
    1. Open the tool you are debugging  
    2. Run the tool

    **NOTE:** Execution of the tool will stop when a breakpoint is hit, in the UI _on the remote machine_ it will appear to have paused.  
15. **Debugging your script**:  
    _On the local machine_  
    1. The execution will pause at the breakpoints set in VSC, allowing you to debug the script.  

    **Note**: For `.pyt` scripts, specifically within the `execute` function, you will need `arcpy.SetupDebugger()` to trigger breakpoints. Injecting these will automatically be set up and torn down by the debugger when connecting and disconnecting.  


## Debug Script Tool Execution Code

If the script tool's execution code is embedded, you must first export the script from the toolbox to a Python file (`.py`) before you can debug it. Follow these steps to debug the script tool's execution code:

1. Open the script tool properties dialog and navigate to the **Execution** tab.
2. If the execution script is embedded, click the **Export script to file** button.
3. Continue debugging using the exported Python script file.
4. When you are done debugging, don't forget to embed the script again if it was previously embedded.

## Debug Script Tool Validation Code

Python code in the script tool validation is embedded in the tool and needs to be copied to an external Python file (.py) to debug it. You can then open the Python file in your IDE and set breakpoints, attach the IDE to ArcGIS Pro, and run your script tool. Upon completion of code modification, copy the contents of the Python file back into the tool validation.

1. Open the script tool properties dialog and navigate to the **Validation** tab.
2. Copy the contents of the code editor into a Python file (validation_code.py in the sample code).
3. Replace the contents of the code editor in the **Tool Properties** dialog **Validation** tab with the sample code below:  
    In the following example, validation_code.py (contents not shown) contains the `ToolValidator` class and is saved to the same directory as the toolbox.  
    ``` python
    import os
    import sys

    sys.path.append(os.getcwd())  # directory containing module must be in `sys.path`
    import validation_code

    # the following code will reload the val.py module if it's modified
    if 'validation_code' in sys.modules:
        import importlib
        importlib.reload(validation_code)

    # ToolValidator should exist at the global scope
    ToolValidator = validation_code.ToolValidator
    ```
4. Continue debugging using the validation_code.py file.
5. When you are done debugging, replace the contents of the code editor in the tool properties dialog Validation tab with those of your Python file (validation_code.py in the sample code).

## Troubleshooting

### If the extension fails to attach to ArcGIS Pro
The extension fails to attach to ArcGIS Pro with the following error message:  

> "Timed out waiting for debug server to connect"  

This can happen if Python has not yet initialized in ArcGIS Pro, or the previous session was improperly disconnected. Try these:  
* **Make sure Python has initialized:**  
   In ArcGIS Pro, Python loads as needed (when a geoprocessing tool, the Python Window, or a Notebook are opened). The debugger will not be able to attach until Python has initialized.
   1. Open the tool you are debugging, then try attaching again  
   
   **NOTE:** Opening any geoprocessing tool will cause Python to initialize. Alternatively, open either the Python Window or a Notebook.

* **Restart:**
    1. Close ArcGIS Pro
    2. Wait ~15 seconds for locks to clear (alternatively, restart Windows)
    3. Start ArcGIS Pro and try attaching again

### If code using `subprocess` hangs
Code using `subprocess` hangs indefinitly while debugger is attached to ArcGIS Pro.

* **Use subprocess.communicate() with a timeout.**
This avoids potential blocking issues while reading out data.

For example, the following script uses subprocess to run another Python file and retreives the outputs:

``` python

import arcpy
import os
import sys
import subprocess
import time

MSG_STR_SPLITTER = " | "
CREATE_NO_WINDOW = 0x08000000

def execute_subprocess(script_path: str) -> str:
    inputs = [
        os.path.join(sys.exec_prefix, "python.exe"),
        script_path
    ]
    try:
        process = subprocess.Popen(
            inputs,
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            creationflags=CREATE_NO_WINDOW,
            universal_newlines=True
        )
        # Read all output with timeout to prevent hanging
        output, error = process.communicate(timeout=30)
        msg = output.strip()
        if error:
            msg += "\n" + error.strip()
        return msg
    except subprocess.TimeoutExpired:
        process.kill()
        output, error = process.communicate()
        return f"{output.strip()}\nSubprocess timed out."
    
subproc_file = os.path.join(os.getcwd(), "subproc.py")
arcpy.AddMessage(execute_subprocess(subproc_file))
```

## Issues

Find a bug or want to request a new feature?  Please let us know by submitting an issue.

## Contributing

Esri welcomes contributions from anyone and everyone. Please see our [guidelines for contributing](https://github.com/esri/contributing).

## Licensing

Copyright 2025 Esri

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

A copy of the license is available in the repository's [license.txt](https://github-admin.esri.com/doc/LICENSE.txt) file.
