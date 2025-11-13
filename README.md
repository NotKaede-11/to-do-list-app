# To-Do List Application (x86 Assembly)

[![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)](https://www.microsoft.com/windows)
[![Assembly](https://img.shields.io/badge/language-x86%20Assembly-orange.svg)](https://www.nasm.us/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

A feature-rich, console-based task management application written in 32-bit x86 assembly language using NASM for Windows. This project demonstrates low-level programming concepts including Windows API integration, file I/O, memory management, and user-friendly console interfaces—all without using high-level languages.

---

## 📑 Table of Contents

- [Quick Start](#-quick-start)
- [Features](#-features)
- [Usage Guide](#-usage-guide)
- [For Developers (Build from Source)](#️-for-developers-build-from-source)
- [What's Included](#-whats-included)
- [Architecture & Implementation](#️-architecture--implementation)
- [Development Phases](#-development-phases)
- [Use Cases](#-use-cases)
- [Customization](#-customization)
- [Troubleshooting](#-troubleshooting)
- [Project Stats](#-project-stats)
- [Contributing](#-contributing)
- [Authors](#-authors)
- [Version History](#-version-history)

---

## 🚀 Quick Start

### For End Users (Just Run It)

1. Download **only** `todo32.exe` (standalone - no other files needed!)
2. Double-click or run from command prompt:
   ```powershell
   .\todo32.exe
   ```
3. Start managing your tasks!

**Optional:** Download `Sample Input – 30 Task List.txt` to see example tasks you can paste into the app.

**Note:** Requires Windows (32-bit or 64-bit). The exe is completely standalone - no installation, no dependencies, no other files required.

---

## 📋 Features

### Core Task Management

- ✅ **Add Tasks** - Single or multiple tasks at once (separated by `;`)
- ✅ **View All Tasks** - Display tasks in a clean, bordered table format
- ✅ **Update Task** - Modify task descriptions
- ✅ **Delete Task** - Remove all tasks or select specific ones
- ✅ **Toggle Complete** - Mark tasks as done/undone with checkbox indicators `[ ]` / `[+]`
- ✅ **Save/Load** - Persist tasks to disk in binary format
- ✅ **Modify Slots** - Adjust task limit (10, 15, 20, or 30 tasks)
- ✅ **Search Tasks** - Find tasks by keyword (case-sensitive substring search)
- ✅ **Sort Tasks** - Alphabetically sort your task list (A-Z)

### User Experience Enhancements

- 🎯 **ESC to Cancel** - Press `0` to cancel any operation
- 👀 **Task Preview** - See all tasks before Update/Delete/Toggle operations
- ⏸️ **Press Enter to Continue** - Read output before returning to menu
- 🧹 **Input Validation** - Automatic whitespace trimming, empty task rejection
- 📊 **Task Counters** - Shows completed vs. remaining tasks in real-time
- 🎨 **Bordered UI** - Clean ASCII art borders and formatted displays
- 💡 **Helpful Hints** - Contextual tips for complex operations

---

## 🛠️ For Developers (Build from Source)

### Prerequisites

- **NASM** (Netwide Assembler) - Version 2.x or higher
- **GoLink** (Linker) - v1.0.4.6 or higher (included in repo)
- **Windows** - Any modern version with kernel32.dll

### Option 1: Easy Build (Recommended)

Use the included GoLink linker (no Visual Studio needed):

```powershell
# Run the build script
.\build-golink.bat
```

### Option 2: Manual Build

```powershell
# Assemble
nasm -f win32 todo32.asm -o todo32.obj

# Link (using GoLink)
.\Golink\GoLink.exe /console /entry main todo32.obj kernel32.dll
```

### Option 3: Visual Studio Linker

If you have Visual Studio 2022 installed:

```powershell
.\build32.bat
```

---

## 📦 What's Included

### Essential Files (Required)

- `todo32.asm` - Main application source code (3,063 lines)
- `todo32.exe` - Compiled executable (ready to run)
- `build-golink.bat` - Build script using GoLink
- `Golink/GoLink.exe` - Lightweight linker (no VS required)
- `README.md` - This file

### Optional Files

- `build32.bat` - Alternative build script (requires Visual Studio)
- `tasks.dat` - Task data file (auto-created on first save)

---

## 💻 Usage Guide

### Basic Operations

```
===== TO-DO LIST APPLICATION =====
Status: 0 completed, 0 remaining
Total: 0/10 tasks

  1. Add Task
  2. View All Tasks
  3. Update Task
  4. Delete Task
  5. Toggle Complete
  6. Save Tasks
  7. Load Tasks
  8. Modify Task Slots
  9. Search Tasks
  10. Sort Tasks
  11. Exit

  Choose option: _
```

### Quick Tips

- **Add multiple tasks:** Type `task1;task2;task3` to add three tasks at once
- **Cancel any operation:** Press `0` then Enter
- **Delete specific tasks:** Enter task numbers separated by spaces: `1 3 5`
- **Toggle multiple tasks:** Enter task numbers separated by spaces: `2 4 6`
- **Search for tasks:** Use option 9 to find tasks by keyword
- **Sort alphabetically:** Use option 10 to organize your task list
- **Save your work:** Always save (option 6) before exiting!

---

## 🏗️ Architecture & Implementation

### Technical Highlights

- **Language:** Pure x86 assembly (NASM syntax)
- **Architecture:** 32-bit Windows PE executable
- **API:** Windows kernel32.dll (stdcall convention)
- **File Format:** Binary task storage in `tasks.dat`
- **Code Size:** 3,063 lines of assembly
- **Executable Size:** ~13 KB

### Key Functions

- `main` - Application entry point and menu loop
- `add_task` - Multi-task input with semicolon parsing
- `view_tasks` - Bordered table display with status icons
- `update_task` - Task modification with preview
- `delete_task` - Single/multi/all deletion modes
- `toggle_complete` - Status toggling with checkbox updates
- `save_tasks` / `load_tasks` - Binary file persistence
- `modify_slots` - Dynamic task limit adjustment
- `search_tasks` - Keyword-based task search
- `sort_tasks` - Alphabetical task sorting
- `display_tasks_preview` - Preview table for operations
- `wait_for_enter` - User-friendly pause mechanism
- `cancel_operation` - ESC/cancel handling

### Memory Layout

```
section .data    - Constant strings, messages, UI elements
section .bss     - Runtime buffers, counters, task storage
section .text    - Program code and logic
```

---

## 📚 Development Phases

This project was developed in phases with comprehensive testing:

### ✅ Phase 1: ESC Cancel Functionality

- Added ability to cancel operations with `0` key
- Implemented across all input prompts
- Prevents accidental operations

### ✅ Phase 2: Task Preview

- Shows task list before Update/Delete/Toggle
- Reduces "guessing" task numbers
- Improves user decision-making

### ✅ Phase 3: Press Enter to Continue

- Pauses after successful operations
- Prevents menu from appearing too quickly
- Gives time to read output messages

### ✅ Phase 4: Documentation & Organization

- Comprehensive README
- File organization and cleanup
- Complete project documentation

### ✅ Phase 5: Search & Sort Features

- **Search Tasks** - Case-sensitive substring search across all tasks
- **Sort Tasks** - Alphabetical sorting (A-Z) of task list
- Extended menu to 11 options for new features
- Enhanced user workflow with advanced task management

---

## 🎯 Use Cases

### Educational

- Learn x86 assembly programming
- Understand Windows API calls
- Practice low-level file I/O
- Study memory management
- Explore console application development

### Practical

- Lightweight task management
- No bloat, no dependencies
- Instant startup (< 10 KB executable)
- Works on any Windows machine
- Complete offline functionality

---

## 🔧 Customization

### Modify Task Limit

Change `MAX_TASKS` constant in `todo32.asm`:

```nasm
MAX_TASKS equ 50    ; Default is 30
```

### Change Task Size

Adjust `TASK_SIZE` constant:

```nasm
TASK_SIZE equ 100   ; Default is 64 (63 chars + status byte)
```

### Rebuild After Changes

```powershell
nasm -f win32 todo32.asm -o todo32.obj
.\Golink\GoLink.exe /console /entry main todo32.obj kernel32.dll
```

---

## 🐛 Troubleshooting

| Issue                      | Solution                                               |
| -------------------------- | ------------------------------------------------------ |
| `'nasm' is not recognized` | Add NASM to system PATH or use full path to nasm.exe   |
| `GoLink.exe not found`     | Ensure `Golink/GoLink.exe` exists in project folder    |
| `tasks.dat` won't load     | File may be corrupted; delete and recreate by saving   |
| Garbled text display       | Ensure console uses Code Page 437 or compatible        |
| Program crashes            | Check that you're running on Windows with kernel32.dll |

---

## 📊 Project Stats

- **Total Code:** 3,063 lines of assembly
- **Development Time:** Multiple phases over several iterations
- **Test Coverage:** 30+ test cases across 5 test suites
- **Functions:** 20+ major functions
- **API Calls:** 8 Windows API functions utilized
- **File Size:** ~13 KB (executable)

---

## 🤝 Contributing

This is an educational project, but contributions are welcome:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

### Ideas for Contributions

- Add color support (ANSI codes)
- Implement task priorities
- Add due dates
- Create task categories
- Export to text/CSV
- Add task filtering options
- Implement undo/redo functionality

---

## 📄 License

This project is open source and available under the MIT License.

---

## 👥 Authors

**Group 3:**

- CARTONEROS, BEOMARC ANDREW D.
- CARVAJAL, CHRISTIAN EZEKIEL L.
- CASTILLO, CHARLES
- GO, MARCO ENRICO S.
- HANGINON, MARIA FATIMA T.
- SILVESTRE, DASHIELL B.

---

## 🙏 Acknowledgments

- **NASM** - The Netwide Assembler team
- **GoLink** - Jeremy Gordon for the lightweight linker
- **Windows API** - Microsoft for comprehensive documentation
- **Assembly Community** - For tutorials and support resources

---

## 📞 Support

Having issues? Check the troubleshooting section above or review the build instructions.

For bug reports or feature requests, please open an issue on the repository.

---

**Made with ❤️ and Assembly** - Because sometimes you need to get close to the metal! 🔧

---

## 📜 Version History

- **v2.1** (2025) - Added Search and Sort features, extended to 11 menu options
- **v2.0** (2025) - Enhanced version with ESC cancel, task preview, and press-enter pauses
- **v1.0** (2025) - Initial release with core task management features
