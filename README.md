# MyFuncs
Linux flavored BASH functions for casual CLI

A practical Bash utility pack for Ubuntu 24.04 that replaces macOS specific behavior with Linux ready commands. It includes fast JSON inspectors, note and TODO search, clipboard and text shaping helpers, date and time converters, simple networking math, file dumpers for reviews, and small quality of life wrappers for Git and Terraform. Sensible auto detection picks Wayland or X11 clipboards, with clear fallbacks. Drop the script in your home directory, source it from .bashrc, and use the grouped functions as focused, composable tools in everyday workflows.

# README, ubuntu-myfuncs

## Overview

A compact Bash function and alias library tuned for Ubuntu 24.04. It replaces macOS specific bits with Linux friendly commands and adds sensible fallbacks. Utilities cover JSON viewing, note searching, clipboard text shaping, time and date helpers, simple networking math, project file dumping, and small quality of life wrappers for Git and Terraform.

## Function Naming Convention

Functions with leading underscores (e.g., `_function_name`) are internal helper functions called by other functions and should not be invoked directly by users. Functions without leading underscores are safe for direct user invocation.

## Requirements

Core: `bash`, `curl`, `grep`, `sed`, `awk`, `find`, `ls`, `date`, `printf`
Recommended: `jq`, `uuidgen` (util-linux), `wl-clipboard` or `xclip` or `xsel`, `ccrypt`, `coreutils`, `neofetch`
Optional: `terraform`, `git`, `base32`

## Automatic Dependency Installation

MyFuncs includes an automatic dependency installer that detects your Linux distribution and package manager:

```bash
myfuncs_install_deps
```

This will:
- Detect your package manager (apt, dnf, yum, pacman, brew, etc.)
- Check for required dependencies
- Install missing packages automatically
- Provide clear feedback on installation status

Run this after initial setup to ensure all features work properly.

Install suggestions:

```bash
sudo apt update
sudo apt install -y jq uuid-runtime xclip ccrypt coreutils git curl
# yq v4:
sudo wget -O /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 && sudo chmod +x /usr/local/bin/yq
# Wayland clipboard (if on Wayland):
sudo apt install -y wl-clipboard
```

## Setup

Place the script in your home directory and source it from your shell config.

```bash
# clone or copy ubuntu-myfuncs.sh somewhere, for example:
cp ubuntu-myfuncs.sh ~/.ubuntu-myfuncs.sh
echo 'source ~/.ubuntu-myfuncs.sh' >> ~/.bashrc
source ~/.bashrc
```

## Quick start

```bash
# JSON
jcat file.json             # pretty print JSON
jqkeys < file.json         # show JSON keys
jqcheck file.json          # validate JSON
jqpaths < file.json        # show JSON paths
jqjoke                     # fetch sample JSON

# Notes
busca "kafka"              # search notes
whattodo                   # TODO density by file
cleartodo 2024-10-01 30    # mark TODO to SKIP in date range

# Clipboard and shaping
clip 72                    # wrap clipboard text at 72
ones                       # collapse multiple spaces
moos '_' ' '               # replace char in clipboard content

# Time, date, conversions
epochnow
e2h 1732646400
h2e "Jan 1 2025"
utc2local 2025-01-01T00:00:00

# Networking
netcalc 192.168.1.0 255.255.255.0
pubip
whereip 8.8.8.8

# Files and git
splat "*.md"               # print files with headers
splooge .                  # recursive print with extension filter file
gitdiff README.md
look4this "*.tf" module    # search text in matching files

# Terraform (if installed)
tfchk

# Help system
funchelp                # Show all available functions
funchelp json           # Show JSON function help
funchelp jqcheck        # Show help for specific function

# Dependency management
myfunc_install_deps     # Check and install all required dependencies
```

## Function groups

### JSON

* `jcat`, `jqkeys`, `jqcheck`, `jqpaths`, `jqjoke`
  Pretty print JSON, explore JSON structures, validate JSON files, show JSON paths, and fetch a simple sample JSON payload for testing.

### Notes search

* `busca`, `whattodo`, `cleartodo`, `bang`, `findbang`
  Search personal notes, summarize TODO density, bulk mark TODO as SKIP in a time window, and generate quick anchors.

### Networking

* `pubip`, `whereip <ip>`, `whoip`, `netcalc <ip> <mask>`
  Show your public IP, basic IP geolocation, reference list lookups, and mask math.

### File dumping and diffs

* `splat`, `splooge`, `gitdiff <file>`
  Print files with headers for review, recursively print while honoring `~/.splooge.filter`, and diff a file against HEAD.

### Clipboard and text shaping

* `clip`, `clop`, `clpcry`, `nocry`, `ones`, `moos`, `txtcln`, `mkhead`, `mkbody`, `mkgrid`, `lineup`, `spaceout`, `numcat`, `coldwar`, `letonly`, `fold64`, `colx`
  Work well on Wayland or X11. `clpcry` and `nocry` depend on `ccrypt`. `mkhead` and `mkbody` help build Markdown tables fast.

### Time and date

* `epochnow`, `e2h`, `h2e`, `utc2local`, `inthepast`, `inthefuture`
  Thin wrappers over `date` for quick conversions.

### Shell helpers and prompts

* `hl`, `hg`, `tnb`, `dropone`, `uc`, `lc`, `getwin`, `tabname`
* Prompts: `normalprompt`, `gitprompt`, `exitprompt`, plus `githelp`, `prompthelp`
* Help: `funchelp [topic]` - Comprehensive help system

### Terraform

* `_tffun` auto-loads aliases if `terraform` exists: `tfini`, `tfval`, `tffmt`, `tfpln`, `tfapl`, `tfdes`, `tfshw`, `tflst`, `tfout`, `tfref`, `tfimp`

## Configuration and environment

* `~/.splooge.filter` defines filename patterns to exclude per line, for example:

  ```
  .json
  .log
  .tmp
  node_modules
  ```

## Tips

* Wayland desktops: install `wl-clipboard` and you get instant clipboard support.
* X11 sessions: install `xclip` or `xsel`.
* Set your timezone in the environment if needed: `export TZ=America/New_York`.
* Keep `jq` and `yq` up to date for predictable parsing.

## License

Use under your preferred internal policy. Review third party tool licenses you install.

---

## GitLab description paragraph

A practical Bash utility pack for Ubuntu 24.04 that replaces macOS specific behavior with Linux ready commands. It includes fast YAML and JSON inspectors, note and TODO search, clipboard and text shaping helpers, date and time converters, simple networking math, file dumpers for reviews, and small quality of life wrappers for Git, Terraform, and Terragrunt. Sensible auto detection picks Wayland or X11 clipboards, with clear fallbacks. Drop the script in your home directory, source it from `.bashrc`, and use the grouped functions as focused, composable tools in everyday workflows.
