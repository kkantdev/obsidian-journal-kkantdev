---
{"dg-publish":true,"permalink":"/documents/window-guide/how-to-install-node-js-on-windows-beginner-s-guide/","dg-note-properties":{}}
---



Installing Node.js allows you to run JavaScript code directly on your computer. Follow these steps to check your system type and install Node.js correctly.

## Step 1: Check Your System Architecture

Before downloading Node.js, you need to know if your PC uses an **x64** (AMD64/Intel) or **ARM64** processor so you get the right installer.

1. Press the **Windows Key** on your keyboard, type **cmd**, and press **Enter**.
    
2. In the Command Prompt window, type the following command and press **Enter**:
    
    DOS
    
    ```
    echo %PROCESSOR_ARCHITECTURE%
    ```
    
3. Look at the output:
    
    - **`AMD64` or `x64`**: Select the standard **x64** installer on the website.
        
    - **`ARM64`**: Select the **ARM64** installer on the website.
        
    - **`x86`**: Select the **x86 / 32-bit** installer.
        

## Step 2: Download Node.js

1. Go to the official website: [nodejs.org](https://nodejs.org/).
    
2. Click on the **LTS (Long Term Support)** tab. _LTS is recommended because it is stable and well-tested._
    
3. Select your operating system (**Windows**) and choose the architecture you identified in Step 1 (usually **x64**).
    
4. Click **Download** to save the `.msi` setup file.
    

## Step 3: Install Node.js

**1.Run the installer:**1 min.

Double-click the downloaded `.msi` file. The Node.js Setup Wizard will appear. Click **Next**.

**2.Accept the End-User License Agreement:**10 seconds.

Check the box to accept the terms, then click **Next**.

**3.Choose destination folder & default features:**30 seconds.

Leave the default installation path (`C:\Program Files\nodejs\`) and default feature selections unchanged. Click **Next**.

**4.Tools for Native Modules (Optional):**30 seconds.

You will see an option to automatically install optional tools (like Chocolatey/Python). Beginners can leave this box **unchecked** and click **Next**.

**5.Complete the installation:**1-2 min.

Click **Install**. If a Windows prompt asks for administrator permission, click **Yes**. Once finished, click **Finish**.

## Step 4: Verify the Installation

To make sure Node.js and its package manager (`npm`) were installed successfully:

1. Open a new Command Prompt window (_close any open ones first so the system updates your path variables_).
    
2. Check the Node.js version by running:
    
    DOS
    
    ```
    node -v
    ```
    
    _(You should see a version number like `v20.x.x` or higher.)_
    
3. Check the NPM version by running:
    
    DOS
    
    ```
    npm -v
    ```
    

> **Congratulations!** Node.js is now fully installed and ready to build applications.