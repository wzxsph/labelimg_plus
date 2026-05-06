# labelimg_plus

A customized version of [labelImg](https://github.com/tzutalin/labelImg) optimized for **video/object tracking annotation workflows**. Built with enhanced features for frame-by-frame label editing.

## Features

### Core Improvements
- **Auto-Zoom Preservation** - Automatically maintains the same zoom level when switching frames
- **Scroll Position Memory** - Preserves scroll position between frames
- **Box Labels Auto-Sorting** - Labels sorted by number (1, 2, 10 not 1, 10, 2)
- **Frame Label Change Detection** - Shows +/– indicators for label changes between frames

### Quick Label Operations (Per-frame)
- **Quick Copy** - Copy a labeled bounding box from previous frame to current frame
- **Quick Delete** - Automatically delete specified label when switching to next frame
- **Quick Replace** - Replace all instances of a label number with another number

### Other Features
- **Duplicate Label Prevention** - Prevents creating duplicate labels in the same frame
- **Default No Selection** - Label list defaults to nothing selected for clear visibility
- **Selected Label Display** - Shows currently selected label number in the info panel

## Environment Setup

### Requirements
- Python 3.8+
- PyQt5
- lxml

### Installation

1. **Clone or download this project**

2. **Create a virtual environment (recommended)**
```bash
cd C:\Users\ihao8\Desktop\maybe\rxdata_process
python -m venv .venv
.venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install PyQt5 lxml
```

4. **Run the application**
```bash
python labelImg_src/labelImg.py
```

Or use the virtual environment:
```bash
.venv\Scripts\activate
python labelImg_src/labelImg.py
```

## Default Configuration

On first launch, the application defaults to:
- **Open Dir**: `C:\Users\ihao8\Desktop\maybe\rxdata_process\工作区\image`
- **Save Dir**: `C:\Users\ihao8\Desktop\maybe\rxdata_process\工作区\xml`

To change defaults, modify these constants in `labelImg.py`:
```python
DEFAULT_IMG_DIR = r"your\image\directory"
DEFAULT_XML_DIR = r"your\xml\directory"
```

## Usage Guide

### Basic Navigation
- Press **A** - Previous frame
- Press **D** - Next frame
- Press **W** - Create bounding box
- Press **Ctrl+S** - Save annotations

### Quick Copy Label
Copies a labeled box from the previous frame to the current frame.

1. Enter label number in "Copy:" input (e.g., `3`)
2. Click **Set**
3. Press **D** to go to next frame - the label will be auto-copied
4. To cancel, click the **×** button

### Quick Delete Label
Automatically deletes a specified label when entering a new frame.

1. Enter label number in "Delete:" input (e.g., `5`)
2. Click **Set**
3. Press **D** to go to next frame - the label will be auto-deleted
4. To cancel, click the **×** button

### Quick Replace Label
Replaces all instances of one label number with another.

1. Enter source label in first box (e.g., `3`)
2. Enter target label in second box (e.g., `5`)
3. Click **Set**
4. Press **D** to go to next frame - all `3` labels become `5`
5. To cancel, click the **×** button

### Info Panel
The bottom info panel shows:
- Current selected label number (when a box is selected)
- Last operation result (Copied/Deleted/Replaced)
- Frame-to-frame label changes (+new labels / -removed labels)

## Interface Layout

```
┌─────────────────────────────────────────────────┐
│ File List (Left)  │  Canvas (Center) │  Box Labels (Right) │
│                   │                 │                    │
│                   │                 │  [Edit] [Difficult] │
│                   │                 │  [Combo Box]       │
│                   │                 │  [Label List]      │
│                   │                 │  [Frame Changes]    │
│                   │                 │  ┌──────────────┐ │
│                   │                 │  │ Copy: [ ] Set ×│ │
│                   │                 │  │ Delete:[ ] Set ×│ │
│                   │                 │  │ Replace:[]→[]Set×│ │
│                   │                 │  │ Info: ...     │ │
│                   │                 │  └──────────────┘ │
└─────────────────────────────────────────────────┘
```

## Data Format

- **XML files**: Pascal VOC format
- **Image files**: JPEG with matching names
- **Naming convention**: 6-digit zero-padded (e.g., `000001.xml`, `000001.jpg`)

## Dependencies

- Python 3.8+
- PyQt5
- lxml
- labelImg libs (included in `.venv\Lib\site-packages\libs\`)

## Issues Fixed

- `shape_selection_changed` KeyError
- Empty directory crash
- Label sorting object deletion error
- Remove label KeyError for shapes not in dictionary