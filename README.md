````markdown
# Reading Pane Stripe Removal

A **Windhawk mod** that provides a temporary workaround for a Windows 11 Insider bug in File Explorer's Reading/Preview Pane.
[Windhawk](https://windhawk.net/)

## The problem

On some Windows 11 Insider builds, selecting an image or video in File Explorer can produce a horizontal ~47 px stripe across the Reading/Preview Pane.
The stripe is painted with the same color as the pane background and visually cuts the preview into two parts.

**This bug is not present on all Windows builds.**

The issue was observed and tested on:

- **Windows 11 26H2 Insider — build 26300.9032**
- An independent Reddit report was made on **Windows 11 25H2 Insider — build 26220.9022**

Microsoft has acknowledged the issue in the Experimental channel and stated that they are working on it.

### Before

![Reading Pane stripe - before](before.png)

### After

![Reading Pane stripe - after](after.png)

## The workaround

This Windhawk mod suppresses the specific background fill responsible for the stripe.
It does not rely on the stripe's size, position, or color. The affected DUI element is identified through its internal `DUI70.dll` implementation.
This is a **temporary workaround**, not a permanent fix. The internal implementation may change in future Windows builds, and the mod may stop working after a Windows update.
Once Microsoft fixes the underlying bug, the mod should be disabled or removed.

## Installation

This is a **Windhawk mod**.

1. Install [Windhawk](https://windhawk.net/).
2. Open Windhawk and install the mod from the source code in `readingpane-stripe-removal.cpp`.
3. Compile and enable the mod.
4. **Completely restart `explorer.exe` before opening File Explorer again.**

### PowerShell

Run:

```powershell
Stop-Process -Name explorer -Force
Start-Process explorer.exe
````

### Task Manager

1. Open **Task Manager**.
2. Find **Windows Explorer**.
3. Right-click it → **End task**.
4. Select **Run new task**.
5. Enter:

```text
explorer.exe
```

6. Press **Enter**.

The Explorer restart is important because the affected DirectUI/Preview Pane state may already be cached before the mod is loaded.

## Compatibility

The workaround is intended for Windows 11 Insider builds affected by this bug.
The implementation uses internal `DUI70.dll` addresses and structure offsets, so compatibility with other Windows builds is not guaranteed.

```
