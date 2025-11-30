# 🎨 Automated Art Frame Processing Tool

A powerful Python tool for automatically framing artwork using perspective transformation. Select frame corners once, then process unlimited artwork images with consistent professional results.

## 🚀 Features

- **Interactive Frame Selection**: Click to select frame corners with visual feedback
- **Batch Processing**: Process multiple artwork images simultaneously
- **Smart Perspective Correction**: Automatic geometric transformation for perfect fitting
- **Multiple Format Support**: JPG, PNG, BMP, TIFF, WebP
- **Organized Output**: Clean folder structure with descriptive naming
- **Reusable Coordinates**: Save frame settings for unlimited future use

## 📋 Prerequisites

```bash
# Activate virtual environment
source venv/bin/activate

# Required packages (already installed)
pip install opencv-python numpy
```

## 🎯 Quick Start

### Step 1: Select Frame Coordinates (One-Time Setup)

```bash
python interactive_frame_selector.py frame.jpg
```

**Instructions:**
1. Click on the 4 corners of your frame in order:
   - Top-Left corner
   - Top-Right corner  
   - Bottom-Right corner
   - Bottom-Left corner
2. Press 's' to save coordinates
3. Coordinates are saved to `frame_coordinates.json`

### Step 2: Add Your Artwork

Place all your artwork images in the `art/` folder:
```
art/
├── painting1.jpg
├── digital_art.png
├── sketch.webp
└── masterpiece.jpeg
```

### Step 3: Batch Process

```bash
python batch_process_frames.py
```

Choose option 1 to process all images in the art folder.

### Step 4: Get Results

All framed artwork appears in the `output/` folder:
```
output/
├── framed_painting1.jpg
├── framed_digital_art.png
├── framed_sketch.webp
└── framed_masterpiece.jpeg
```

## 📁 Project Structure

```
art-work/
├── art/                              # Input: Your artwork goes here
├── output/                           # Output: Framed results
├── frame.jpg                         # Frame template image
├── frame_coordinates.json            # Saved coordinates
├── interactive_frame_selector.py     # Frame selection tool
├── batch_process_frames.py          # Main batch processor
└── README.md                        # This file
```

## 🛠️ Advanced Usage

### Preview Single Image
```bash
python batch_process_frames.py
# Choose option 2, then select an image to preview
```

### Re-select Frame Coordinates
```bash
python interactive_frame_selector.py frame.jpg
# Click new corners and save
```

### Process Specific Images
The system automatically processes all supported images in the `art/` folder.

## 🎮 Controls

### Interactive Frame Selector
- **Mouse Click**: Select corner points
- **'s' Key**: Save coordinates
- **'r' Key**: Reset selection
- **'q' Key**: Quit without saving

### Batch Processor Options
1. Process all images in art folder
2. Preview single image
3. Create folders and exit

## ✨ Example Workflow

```bash
# 1. Activate environment
source venv/bin/activate

# 2. Select frame (first time only)
python interactive_frame_selector.py frame.jpg
# Click corners: top-left → top-right → bottom-right → bottom-left
# Press 's' to save

# 3. Add artwork to art/ folder
cp my_paintings/* art/

# 4. Process all artwork
python batch_process_frames.py
# Enter: 1

# 5. Find results in output/ folder
ls output/
```

## 📊 Current Configuration

**Frame Coordinates:**
- Top-left: [194, 144]
- Top-right: [647, 140]
- Bottom-right: [610, 869]
- Bottom-left: [133, 824]

**Supported Formats:**
- Input: .jpg, .jpeg, .png, .bmp, .tiff, .webp
- Output: Same format as input with "framed_" prefix

## 🔧 Technical Details

- **Perspective Transformation**: Uses OpenCV's `getPerspectiveTransform()` for accurate geometric correction
- **Aspect Ratio Preservation**: Maintains original artwork proportions
- **High Quality Output**: No compression artifacts in transformation
- **Memory Efficient**: Processes images individually to handle large batches

## 📈 Performance

- ✅ Successfully processed 4 images in example run
- ✅ Handles various image sizes and formats
- ✅ Consistent frame positioning across all artwork
- ✅ Zero processing failures in testing

## 🎨 Tips for Best Results

1. **High Resolution**: Use high-quality artwork for best output
2. **Clear Frames**: Ensure frame corners are clearly visible in template
3. **Consistent Lighting**: Frame template should have even lighting
4. **Organized Files**: Keep artwork organized in the art/ folder
5. **Backup Originals**: Original files remain untouched in art/ folder

---

**Ready to frame your artwork collection? Start with Step 1! 🖼️**