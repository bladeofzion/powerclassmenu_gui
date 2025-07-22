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

- A Zenity menu will appear with options.
- Select modes or toggles; the script handles sudo prompts graphically.
- Use "Show Current Settings" to view CPU status.

**Example**: To set "Top Mode" for maximum performance, select it from the menu—all changes are applied immediately.

## Warnings
- **Root Access**: Modifies system files (e.g., `/sys/devices/system/cpu/`), so run as a user with sudo rights.
- **Hardware-Specific**: Tuned for CPUs with ~14-28 cores/threads (e.g., i9-13900H). Adjust variables like enabled cores in modes if your hardware differs. **Developed on LMDE 6; test thoroughly on other systems to avoid compatibility issues.**
- **Risks**: Disabling cores or Turbo can cause instability; overclocking equivalents may increase heat/power draw. Monitor with tools like `htop` or `sensors`.
- **Backup**: Test in a safe environment. No warranty for hardware damage.
- **Compatibility**: Assumes `intel_pstate` driver; may not work on AMD or non-Intel systems without modifications.

## Customization
- Edit mode settings (e.g., `ENABLED_CORES` in `lux()`, `trv()`, `eco()`) to match your CPU's processor count (e.g., 14 physical cores on i9-13900H; check with `nproc --all` for logical cores).
- Frequency calculations are based on a base of 2.6 GHz + increments; adjust in `scaling_max_freq()` for your hardware's max frequency (up to 5.4 GHz on i9-13900H).
- For non-LMDE systems, modify dependency checks, sudo handling, or sysfs paths as needed.

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details. (Add a LICENSE file to your repo if desired.)

## Contributing
Feel free to fork and submit pull requests for improvements, such as AMD support or additional modes.

## Credits
Developed for personal use on high-performance laptops. Inspired by sysfs CPU tuning guides.

*Last Updated: Monday, 21 July 2025, 09:40 PM*

   sudo apt update
   sudo apt install linux-cpupower zenity gksu
   ```

## Usage
Run the script from the terminal:
