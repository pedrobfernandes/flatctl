# Flatctl

Flatctl is a graphical Flatpak manager written in Bash using YAD.

It provides a simple interface to perform common Flatpak operations without using the terminal.

I mainly wrote it because I use Slackware Linux and Salix Os as my main distros, and I use loads of Flatpaks, but wanted to perform the operations using a GUI.
I know there are much more complete solutions for this, including one named Warehouse, but i wanted something 'GUI Like' and at the same time simpler and straight to the point.

---

## ✨ Features

- Search and install applications from Flathub (can install in "bulk" selecting several apps)
- List installed applications and runtimes
- Update installed Flatpaks
- Uninstall applications (can uninstall in "bulk" selecting several apps)
- Perform basic maintenance:
  - `flatpak repair`
  - removal of unused runtimes and data
- Real-time output for long-running operations
- Lightweight and minimalistic
- English and Portuguese support

---

## 📦 Requirements

Flatctl does not perform dependency checks during installation.

Make sure the following are installed on your system:

- Bash (modern version)
- Flatpak
- YAD (Yet Another Dialog)
- pkexec (from polkit) — used for the `flatpak repair` operation
- Flathub repository added and configured on the system

---

## 🧪 Tested with

- Bash 5.1.16
- Flatpak 1.14.10
- YAD 13.0

---

## 🧠 Design

Flatctl is not just a simple wrapper around Flatpak commands.

It is designed to behave like a real application, even though it is written entirely in Bash.

### Key design points

- **Single instance control**  
  Prevents multiple instances using file locking (`flock`).

- **Concurrency control**  
  Ensures that only one operation runs at a time.

- **Process isolation**  
  Uses `setsid` to manage background tasks independently.

- **Inter-process communication**  
  Uses FIFO pipes to stream command output in real time.

- **Responsive UI**  
  Long-running operations display live output using YAD.

This approach avoids the typical "dialog chain" behavior seen in simple scripts and provides a more consistent user experience.

---

## ⚙️ Design assumptions

Flatctl is intentionally opinionated and makes the following assumptions:

### System-wide Flatpak installation

All operations are executed using:
`--system`

This follows the default Flatpak setup using system-wide installations and polkit authentication.

---

### Flathub as default repository

Applications are installed from Flathub:
`flatpak install flathub <app>`

Flatctl does not support selecting alternative remotes.

---

### No portability concerns

Flatctl uses modern Bash features and is not designed to be POSIX-compliant.

---

## 🚀 Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/flatctl.git
cd flatctl
```
Run the installer:

```bash
./install-flatctl
```

🗑️ Uninstallation:

Like the main application, the uninstaller is added to `$PATH`, so it will suffice in the terminal to just type in:
```bash
$ uninstall-flatctl
```

And everything related to the program will be removed.

🖥️ Usage

Run:
```bash
$ flatctl
```
Or use the desktop entry in the applications menu.

---

## 🌍 Language

Flatctl automatically detects system language via:
`$LANG`

Supported languages:

- English
- Portuguese

---

## ⚠️ Notes

Flatctl does not aim to replace full-featured Flatpak frontends.
It focuses on common daily operations.
Advanced features are intentionally out of scope.

---

## 👤 Author

Pedro Fernandes

