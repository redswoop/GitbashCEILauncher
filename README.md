# GitBash ComfyUI Easy Install Starter with Custom Paths

A bash script for **ComfyUI Easy Install** users that provides flexible path management and launches ComfyUI with SageAttention optimization.

## Requirements

- **Git Bash on Windows** (or any bash shell on Linux/macOS)
- **ComfyUI Easy Install** setup
- Optional: [gum](https://github.com/charmbracelet/gum) for enhanced visual output

## Overview

This script implements a hierarchical path resolution system for ComfyUI's three main directories, allowing you to customize where ComfyUI reads inputs, stores outputs, and manages user data. It's specifically designed for ComfyUI Easy Install users who want more control over their directory structure.

## Path Resolution System

The script manages three key directories with intelligent fallback behavior:

### 1. Output Directory
- **Environment Variable**: `COMFY_OUTPUT_DIR`
- **Fallback**: `${COMFY_DIR}/output`
- **Purpose**: Generated images and workflow outputs

### 2. User Directory  
- **Environment Variable**: `COMFY_USER_DIR`
- **Fallback**: `${COMFY_DIR}/user`
- **Purpose**: User-specific settings, custom workflows, and preferences

### 3. Input Directory
- **Environment Variable**: `COMFY_INPUT_DIR`
- **Fallback**: `${COMFY_DIR}/input`
- **Purpose**: Source location for input images, videos, and other assets

**Resolution Priority**: Explicit environment variable → `COMFY_DIR`-based default → unset (uses ComfyUI defaults)

## Usage

### Basic Usage
```bash
./csa
```

### With Custom Paths
```bash
# Set environment variables before running
export COMFY_OUTPUT_DIR="/path/to/my/outputs"
export COMFY_USER_DIR="/path/to/my/user/settings"
export COMFY_INPUT_DIR="/path/to/my/inputs"
./csa
```

### With Additional ComfyUI Arguments
```bash
# Pass any ComfyUI command line arguments
./csa --port 8080 --cpu --preview-method auto
```

### One-liner with Custom Paths
```bash
COMFY_OUTPUT_DIR="/my/outputs" COMFY_USER_DIR="/my/user" ./csa --port 8080
```

## Environment Variables

| Variable | Purpose | Default |
|----------|---------|---------|
| `COMFY_DIR` | Base ComfyUI directory | `./ComfyUI` |
| `COMFY_OUTPUT_DIR` | Output directory | `${COMFY_DIR}/output` |
| `COMFY_USER_DIR` | User directory | `${COMFY_DIR}/user` |
| `COMFY_INPUT_DIR` | Input directory | `${COMFY_DIR}/input` |

## Features

- **SageAttention Optimization**: Automatically enables `--use-sage-attention` for improved performance
- **Network Access**: Enables `--listen` for web interface access
- **Manager Legacy Support**: Includes `--enable-manager-legacy` flag
- **Path Validation**: Shows resolved paths before launching
- **Argument Forwarding**: Passes through any additional command line arguments
- **Visual Output**: Uses [gum](https://github.com/charmbracelet/gum) for enhanced formatting when available
- **Graceful Fallback**: Works with plain echo output when gum is not installed

## Installation on Windows

1. **Install Git Bash** if you haven't already (comes with Git for Windows)
2. **Place the script** in your ComfyUI Easy Install root directory (same level as `ComfyUI/` folder)
3. **Make it executable** (optional, but recommended):
   ```bash
   chmod +x csa
   ```
4. **Run from Git Bash**:
   ```bash
   ./csa
   ```

## Example Scenarios

### Separate Outputs by Project
```bash
# For project A
COMFY_OUTPUT_DIR="/projects/project-a/outputs" ./csa

# For project B  
COMFY_OUTPUT_DIR="/projects/project-b/outputs" ./csa
```

### Shared Asset Library
```bash
# Use a centralized input directory
COMFY_INPUT_DIR="/shared/assets" ./csa
```

### Development vs Production
```bash
# Development environment
COMFY_USER_DIR="/dev/comfy-settings" ./csa --port 8080

# Production environment  
COMFY_USER_DIR="/prod/comfy-settings" ./csa --port 80
```

## Output Example

When running, the script displays:

```
# Starting Comfy with SageAttention

## Configuration Paths
----------------------------------------
Output Directory: ./ComfyUI/output
User Directory:   ./ComfyUI/user
Input Directory:  ./ComfyUI/input
----------------------------------------

## Command Line Arguments
----------------------------------------
./python_embeded/python.exe
-I
-W
ignore::FutureWarning
ComfyUI/main.py
--use-sage-attention
--listen
--enable-manager-legacy
--output-directory
./ComfyUI/output
--user-directory
./ComfyUI/user
--input-directory
./ComfyUI/input
----------------------------------------
```

## Troubleshooting

### "command not found: gum"
This is normal - the script will use plain text output. Install gum for better formatting:
```bash
# Windows (with Chocolatey)
choco install gum

# Or download from: https://github.com/charmbracelet/gum/releases
```

### "Permission denied"
Make the script executable:
```bash
chmod +x csa
```

### "No such file or directory: python.exe"
Ensure you're running from the ComfyUI Easy Install root directory where `python_embeded/` exists.

## Compatibility

- **Windows**: Requires Git Bash
- **Linux/macOS**: Works with any bash shell
- **ComfyUI**: Designed for Easy Install setups, should work with manual installations if directory structure matches

## License

This script is provided as-is for ComfyUI Easy Install users. Modify as needed for your setup.
