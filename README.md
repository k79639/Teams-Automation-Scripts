## Microsoft Teams Break Automation

### Overview

This script automates certain tasks in Microsoft Teams to improve efficiency. There are two scripts included:

1. **Setup Meeting Automation** – Automates screen sharing and recording in a Teams meeting, reducing the need for manual clicks. Users only need to create or join a meeting, and the script will handle the rest.
2. **Teams Break Automation** – Simulates a break system in Teams. When executed, it stops the recording and screen sharing. After the set break duration (default: 15 seconds), it automatically reopens the meeting window, resumes the recording, and re-enables screen sharing. This script uses `cliclick` to automate button clicks.

---

### Prerequisites

#### About `cliclick`

`cliclick` (short for "command-line interface click") is an open-source tool that simulates mouse clicks and keystrokes on macOS.

- **GitHub:** [https://github.com/BlueM/cliclick](https://github.com/BlueM/cliclick)

#### Installation

The easiest way to install `cliclick` is via Homebrew:

```sh
brew install cliclick
```

To find its installation path, run:

```sh
which cliclick
```

This outputs the full path needed for script modifications.

#### Permissions Setup

To use these scripts with macOS Shortcuts, grant accessibility permissions:

1. Open **System Preferences > Security & Privacy > Accessibility**.
2. Enable the checkbox for **Automator** and **Microsoft Teams**.

---

### Creating Keyboard Shortcuts

1. Extract the script files and move them to `~/Library/Services/`.
2. Open **System Preferences > Keyboard > Shortcuts > Services**.
3. Scroll to **General** and find both script names.
4. Double-click "None" and assign your desired shortcut.

---

### Customizing the Scripts

To tailor the scripts for your Teams setup, update the click coordinates and `cliclick` path.

#### Editing the Scripts

1. Open the script by **double-clicking it** or by opening **Automator**, selecting **Quick Action**, then **File > Open**.
2. Modify the `cliclick` path:
   - Find this line in the `Setup Meeting Automation` script:
     ```applescript
     do shell script "/opt/homebrew/bin/cliclick c:1080,70"
     ```
   - Replace `/opt/homebrew/bin/cliclick` with your actual path (from `which cliclick`).
   - Replace `1080,70` with the coordinates of the "More" button in Teams.

#### Finding the Coordinates

- **Using macOS Screenshot Tool:**
  - Open Teams and start a meeting in fullscreen.
  - Press **Cmd + Shift + 4**.
  - Move the crosshair over the **More** button (three dots) and note the coordinates.
- **Using Xcode Accessibility Inspector:**
  - Open Xcode, use the **Accessibility Inspector**, target the **More** button, and note the coordinates.

#### Modifications in `Break Automation Script`

- Replace this line **in two places**:
  ```applescript
  do shell script "<your cliclick path> c:<your screen button coordinates>"
  ```
- Click the **hammer icon** in Automator before making changes. This builds the script and formats it properly.

#### Adjusting Break Duration

To change the break duration, modify this line:

```applescript
delay 15 -- Wait for the specified time duration
```

- Time is in seconds. For a **10-minute** break, replace `15` with `600`.

---

### Recommendations

- Keep **only one Teams meeting window** open for optimal script execution.
- After joining a meeting, **close extra Teams windows** before running the script.
- While the **Break Automation Script** runs, you can use your Mac normally. It will automatically return to the meeting when the break ends.
- **Avoid interfering** with the script when it switches back to Teams.

---

### Troubleshooting

#### `cliclick` Not Opening or Blocked by macOS

If you see this warning:

> "Apple could not verify 'cliclick' is free of malware."

Follow these steps:

1. Go to **System Preferences > Security & Privacy > Privacy**.
2. Scroll down and find **Allow Anyway**.
3. Run the script again. If prompted again, a **"Run Anyway"** button will appear.
4. Click **Run Anyway**, enter your **admin password**, and the script should now work.


---

Once setup is complete, you can use your assigned shortcuts to automate meeting tasks efficiently. 🚀

