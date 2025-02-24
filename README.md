## Microsoft Teams Break Automation

### Overview

This script automates certain tasks in Microsoft Teams to improve efficiency. There are two scripts included:

1. **Setup Meeting Automation** – This script helps automate the process of sharing the screen and starting the recording of a Teams meeting without manually clicking multiple times. Users only need to create or join a meeting, and the script will handle the rest.
2. **Teams Break Automation** – This script simulates a break system in Teams. When executed, it stops the recording and screen share. After the set break duration (default is 15 seconds), the script will automatically open the meeting window, start the recording, and re-enable screen sharing. This script uses `cliclick` to click on the recording button automatically. Detailed setup instructions are provided below.

Note: These scripts have been tested on macOS Sequoia.

---

### Prerequisites

#### About `cliclick`

`cliclick` (short for "command-line interface click") is an open-source and free-to-use tool that allows you to simulate mouse clicks and keystrokes on macOS.

- **GitHub Link:** [https://github.com/BlueM/cliclick](https://github.com/BlueM/cliclick)

#### Installation

The easiest way to install `cliclick` is via Homebrew:

```sh
brew install cliclick
```

To find the installation path, run:

```sh
which cliclick
```

This will output the full path, which you will need to update in the script.

#### Permissions Setup

If you want to use these scripts with macOS Shortcuts, you need to grant accessibility permissions:

1. Open **System Preferences > Security & Privacy > Accessibility**.
2. Enable the checkbox for **Automator** and **Microsoft Teams**.

---

### How to Create Keyboard Shortcuts

1. After extracting the script files, move them to `~/Library/Services/`.
2. Open **System Preferences > Keyboard > Shortcuts > Services**.
3. Scroll to **General** and locate both script names.
4. Double-click where "None" is written and assign your desired shortcut.

---

### How to Modify the Scripts for Your Setup

To make this script work for your specific Teams setup, you need to update the click coordinates and `cliclick` path.

#### Editing the Scripts

1. Open the script by **double-clicking** or by opening **Automator**, selecting **Quick Action**, then **File > Open**.
2. **Modify the `cliclick` path**:
   - Locate this line in the `Setup Meeting Automation` script:
     ```applescript
     do shell script "/opt/homebrew/bin/cliclick c:1080,70"
     ```
   - Replace `/opt/homebrew/bin/cliclick` with the actual path from `which cliclick`.
   - Replace `1080,70` with the actual coordinates of the "More" button in Teams.

#### Finding the Coordinates

- **Using macOS Screenshot Tool:**
  - Open Teams and start a meeting in fullscreen.
  - Press **Cmd + Shift + 4**.
  - Move the crosshair over the **More** button (three dots) and note the coordinates.
- **Using Xcode Accessibility Inspector:**
  - Open Xcode, use the **Accessibility Inspector**, target the **More** button, and note the coordinates.

#### Modifications in `Break Automation Script`

- You need to replace this line in **two places**:
  ```applescript
  do shell script "<your cliclick path> c:<your screen button coordinates>"
  ```
- To find these lines easily, click the **hammer icon** in Automator before making changes. This will format the script properly.

#### Adjusting Break Duration

To change the break time, modify this line:

```applescript
delay 15 -- Wait for the specified time duration
```

- Time is measured in seconds. For example, to set a **10-minute** break, replace `15` with `600`.

---

### Recommendations

- Ensure that only **one Teams meeting window** is open at a time for optimal script execution.
- After joining the meeting, **close any extra Teams windows** before running the script.
- When using the **Break Automation Script**, you can use your Mac normally during the break. The script will automatically switch back to the meeting when the time is over.
- **Do not interfere** with the script when it switches back to Teams.

---

### Troubleshooting

#### `cliclick` Not Opening or Blocked by macOS

If you see a warning such as:

> "Apple could not verify 'cliclick' is free of malware."

Follow these steps:

1. Go to **System Preferences > Security & Privacy > Privacy**.
2. Scroll down and find the option to **Allow Anyway**.
3. Run the script again. If it warns you again, a **"Run Anyway"** button will appear.
4. Click **Run Anyway**, enter your **admin password**, and it should work now.

---

### Contributing

Contributions are welcome! If you encounter any issues or have suggestions for improvements, feel free to open an **issue** or submit a **pull request**.

- **Bug Reports**: If you find any bugs, please file an issue with a clear description and, if possible, steps to reproduce the problem.
- **Feature Requests**: If you have an idea for improvement, let us know!
- **Pull Requests**: Before submitting, ensure your code is well-documented and tested.

---

### License

This project is licensed under the [MIT License](LICENSE). You are free to modify and distribute it as per the terms of the license.

---

### Support

If you find this project useful, consider giving it a ⭐ on GitHub! Your support helps improve and maintain this project.

