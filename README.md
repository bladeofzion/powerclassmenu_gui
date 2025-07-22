# powerclassmenu_gui
Zenity GUI Bash script for CPU power management (modes, governors, Turbo) on LMDE 6 with Intel CPUs. Customizable for core counts.

# CPU Power Management GUI Script

## Overview
This is a Bash script (`powerclassmenu_gui`) that provides a graphical user interface (using Zenity) for managing CPU power settings on Linux systems, particularly those with Intel CPUs (e.g., i9-13900H). It allows users to toggle Turbo Boost, switch CPU governors, enable/disable cores, set frequency limits, and apply predefined power modes (e.g., Top, Luxury, Traveller, Eco).

The script is designed for systems like LMDE 6 (Debian-based) and interacts with sysfs and tools like `cpupower` to adjust CPU behavior for performance, power saving, or balanced modes. **Developed on LMDE 6 with Kernel 6.1.0-28-amd64. It may require modifications for other distributions (e.g., non-Debian-based systems) or hardware configurations, such as adjusting the number of enabled cores based on your CPU's physical/logical processor count (use `nproc --all` to check).**

**Note**: This script requires root privileges to modify system settings. Use with caution, as improper changes can affect system stability or hardware. Tested on Intel-based laptops with multicore CPUs.

## Features
- **GUI Menu**: Zenity-based interface for easy selection of options.
- **Predefined Modes**:
  - **Top Mode**: All cores online, performance governor, max frequency, Turbo enabled.
  - **Luxury Mode**: 15 cores online, performance governor, high frequency, Turbo disabled.
  - **Traveller Mode**: 10 cores online, powersave governor, low frequency, Turbo disabled.
  - **Economy Mode**: 5 cores online, powersave governor, min frequency, Turbo disabled.
- **Manual Controls**:
  - Toggle Turbo Boost.
  - Toggle between performance and powersave governors.
  - Set scaling max/min frequencies (max, high, mid, low, min).
  - View current CPU settings (cores, governors, frequencies, power limits).
- **Power Limits**: Adjusts Intel RAPL power caps based on enabled cores.
- **Dependency Checks**: Automatically verifies required tools and prompts for installation.

## Requirements
- **Operating System**: Linux (developed and tested on LMDE 6 / Debian-based distros). May need adaptations for other systems (e.g., Fedora, Arch) due to differences in package management, sysfs paths, or kernel modules.
- **Hardware**: Intel CPU with support for `intel_pstate` driver (e.g., 13th Gen Intel Core i9-13900H with 14 physical cores and 20 threads). **Adjust script for your processor count (e.g., via `nproc --all`); predefined modes assume a high-core setup and may not suit lower-core systems without changes.**
- **Dependencies**:
  - `nproc` (from coreutils, usually pre-installed).
  - `cpupower` (install via `sudo apt install linux-cpupower` on Debian-based systems).
  - `zenity` (install via `sudo apt install zenity`).
  - Graphical sudo tool: `gksudo` (preferred) or `pkexec` (install via `sudo apt install gksu` if needed).
- **Kernel**: 6.1+ with sysfs support for CPU controls. Non-Intel systems (e.g., AMD) will require significant modifications.

## Installation
1. Clone or download the repository:
   ```
   git clone https://github.com/yourusername/your-repo-name.git
   cd your-repo-name
   ```
2. Make the script executable:
   ```
   chmod +x powerclassmenu_gui
   ```
3. Install dependencies if missing (script will prompt via Zenity; adapt commands for non-Debian systems):
   ```
   sudo apt update
   sudo apt install linux-cpupower zenity gksu
   ```

## Usage
Run the script from the terminal:
