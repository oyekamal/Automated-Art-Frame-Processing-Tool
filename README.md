# 🎨 Automated Art Frame Processing Tool

A comprehensive art frame processing solution with both command-line tools and REST API. Select frame corners interactively, then process unlimited artwork images with consistent professional results via web interface or API calls.

## 🚀 Features

### 📱 Web API Interface
- **RESTful API**: Complete REST API for frame management and artwork processing
- **Web UI**: Interactive browser-based frame coordinate selection
- **Batch API Processing**: Process multiple artwork images via single API call
- **Real-time Downloads**: Direct download URLs for processed results
- **Multi-file Support**: Upload and process multiple artworks simultaneously

### 🖥️ Command Line Tools
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

# Install required packages
pip install -r requirements.txt
```

**Required packages:**
- `opencv-python` - Image processing and perspective transformation
- `numpy` - Numerical operations
- `fastapi` - REST API framework
- `uvicorn` - ASGI server for FastAPI
- `pillow` - Image handling and metadata
- `python-multipart` - File upload support

## 🎯 Quick Start

## 🌐 Web API Usage (Recommended)

### Start the API Server
```bash
cd art_frame_api
python main.py
```
The server runs at `http://localhost:8000`

### Web Interface
Visit `http://localhost:8000/frames/manage` for the complete web interface:
- Upload frame images
- Interactive coordinate selection (same as command-line tool)
- Visual coordinate confirmation
- Frame management dashboard

### 📡 REST API Endpoints

#### 1. Frame Management

**Upload Frame Image:**
```bash
curl -X POST "http://localhost:8000/frames/upload" \
  -F "frame_name=my_frame" \
  -F "file=@frame.jpg"
```

**List All Frames:**
```bash
curl "http://localhost:8000/frames"
```

**Set Frame Coordinates (Interactive Web UI):**
```bash
# Open in browser
http://localhost:8000/frames/{frame_id}/coordinates
```

#### 2. Artwork Processing

**Process Single Artwork:**
```bash
curl -X POST "http://localhost:8000/frames/{frame_id}/process-artwork" \
  -F "artwork_images=@artwork.jpg"
```

**Process Multiple Artworks:**
```bash
curl -X POST "http://localhost:8000/frames/{frame_id}/process-artwork" \
  -F "artwork_images=@art1.jpg" \
  -F "artwork_images=@art2.jpg" \
  -F "artwork_images=@art3.png"
```

**Example Response:**
```json
{
  "success": true,
  "frame_id": "abc123-def456-ghi789",
  "processed_count": 2,
  "failed_count": 0,
  "results": [
    {
      "original_filename": "art1.jpg",
      "output_filename": "framed_art1.jpg",
      "status": "success"
    }
  ],
  "download_urls": [
    "/results/session123/framed_art1.jpg",
    "/results/session123/framed_art2.jpg"
  ]
}
```

**Download Processed Results:**
```bash
curl -O "http://localhost:8000/results/{session_id}/{filename}"
```

#### 3. Image Access

**View Frame Images:**
```bash
curl "http://localhost:8000/frames/images/{frame_id}.jpg"
```

**View Coordinate Visualizations:**
```bash
curl "http://localhost:8000/frames/{frame_id}/visual"
```

---

## 🖥️ Command Line Usage (Alternative)

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
├── art_frame_api/                    # 🌐 REST API Application
│   ├── main.py                       # FastAPI server with all endpoints
│   ├── core.py                       # Business logic and processing functions
│   ├── static/                       # Web UI files
│   │   ├── frames_manager.html       # Frame management interface
│   │   └── interactive_selector.html # Coordinate selection UI
│   ├── storage/                      # API data storage
│   │   ├── frames/                   # Uploaded frame images and coordinates
│   │   ├── uploads/                  # Temporary upload storage
│   │   └── results/                  # Processed artwork results
│   └── database/                     # API database files
├── art/                              # 🖼️ Input: Your artwork (CLI mode)
├── output/                           # 📤 Output: Framed results (CLI mode)
├── frame.jpg                         # 🖼️ Frame template image
├── frame_coordinates.json            # 📍 Saved coordinates (CLI mode)
├── interactive_frame_selector.py     # 🎯 CLI frame selection tool
├── batch_process_frames.py          # 🔄 CLI batch processor
├── requirements.txt                  # 📦 Python dependencies
└── README.md                        # 📖 This documentation
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

## ✨ Complete API Workflow Example

### 1. Start API Server
```bash
cd art_frame_api
python main.py
# Server running at http://localhost:8000
```

### 2. Upload Frame via API
```bash
curl -X POST "http://localhost:8000/frames/upload" \
  -F "frame_name=vintage_frame" \
  -F "file=@../frame.jpg"

# Response: {"frame_id": "abc123-def456", "message": "Frame uploaded successfully"}
```

### 3. Set Coordinates via Web UI
```bash
# Open in browser for interactive selection
http://localhost:8000/frames/abc123-def456/coordinates
# Click corners and save (same as CLI tool)
```

### 4. Process Artwork via API
```bash
curl -X POST "http://localhost:8000/frames/abc123-def456/process-artwork" \
  -F "artwork_images=@../art/painting1.jpg" \
  -F "artwork_images=@../art/sketch.png" \
  -F "artwork_images=@../art/photo.jpeg"
```

### 5. Download Results
```bash
# Get session_id from step 4 response
curl -O "http://localhost:8000/results/session123/framed_painting1.jpg"
curl -O "http://localhost:8000/results/session123/framed_sketch.png"
curl -O "http://localhost:8000/results/session123/framed_photo.jpeg"
```

## 🖥️ Command Line Workflow Example

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

## 📚 API Reference

### Frame Management Endpoints

| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| `GET` | `/` | Root page with navigation | - |
| `GET` | `/frames/manage` | Web UI for frame management | - |
| `POST` | `/frames/upload` | Upload new frame image | `frame_name`, `file` |
| `GET` | `/frames` | List all frames with coordinates | - |
| `GET` | `/frames/{frame_id}/coordinates` | Interactive coordinate selector | `frame_id` |
| `POST` | `/frames/{frame_id}/coordinates` | Save frame coordinates | `frame_id`, coordinates |

### Artwork Processing Endpoints

| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| `POST` | `/frames/{frame_id}/process-artwork` | Process artwork with frame | `frame_id`, `artwork_images[]` |
| `GET` | `/results/{session_id}/{filename}` | Download processed result | `session_id`, `filename` |

### Image Access Endpoints

| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| `GET` | `/frames/images/{frame_id}.jpg` | View frame image | `frame_id` |
| `GET` | `/frames/{frame_id}/visual` | View coordinate visualization | `frame_id` |

## 🔧 Technical Details

### API Architecture
- **FastAPI Framework**: High-performance async API with automatic documentation
- **Uvicorn Server**: ASGI server for production-ready deployment
- **File Upload**: Multipart form data support for multiple file uploads
- **Session Management**: Unique session IDs for result tracking
- **Error Handling**: Comprehensive error responses with status codes

### Image Processing
- **Perspective Transformation**: Uses OpenCV's `getPerspectiveTransform()` for accurate geometric correction
- **Aspect Ratio Preservation**: Maintains original artwork proportions
- **High Quality Output**: No compression artifacts in transformation
- **Memory Efficient**: Processes images individually to handle large batches
- **Format Support**: Automatic format detection and preservation

## 📈 Performance & Capabilities

### API Performance
- ✅ Concurrent request handling via FastAPI async
- ✅ Multi-file upload support (tested with 3+ files simultaneously)
- ✅ Real-time processing with immediate download URLs
- ✅ Persistent storage with session-based result retrieval
- ✅ Web UI with same functionality as CLI tools

### Processing Quality
- ✅ Successfully processed various image formats and sizes
- ✅ Handles high-resolution artwork (tested up to 4K)
- ✅ Consistent frame positioning across all artwork
- ✅ Zero processing failures in comprehensive testing
- ✅ Maintains original image quality and color profiles

## 🚀 Deployment Options

### Development Server
```bash
cd art_frame_api
python main.py
# Runs on http://localhost:8000
```

### Production Deployment
```bash
pip install uvicorn[standard]
uvicorn main:app --host 0.0.0.0 --port 8000 --workers 4
```

### Docker Deployment
```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY art_frame_api/ .
EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

## 🎨 Tips for Best Results

### Frame Selection
1. **High Resolution**: Use high-quality frame images for best coordinate precision
2. **Clear Corners**: Ensure frame corners are clearly visible and well-lit
3. **Consistent Lighting**: Even lighting helps with accurate corner detection
4. **Sharp Focus**: Avoid blurry frame images for precise coordinate selection

### Artwork Processing
1. **Quality Input**: Use high-resolution artwork for professional results
2. **Proper Format**: JPG/PNG recommended for best compatibility
3. **Batch Processing**: Use API for efficient multi-image processing
4. **Result Management**: Download results promptly (sessions may expire)

### API Usage
1. **Error Handling**: Always check response status codes
2. **File Limits**: Monitor file sizes for upload limits
3. **Session Tracking**: Save session IDs for result retrieval
4. **Concurrent Requests**: API handles multiple simultaneous uploads

---

## 🎯 Choose Your Workflow

**🌐 For Web/API Integration**: Use the REST API at `http://localhost:8000`
- Web interface for frame management
- Programmatic processing via curl/HTTP clients
- Multi-file batch processing
- Real-time results with download URLs

**🖥️ For Desktop/CLI Usage**: Use the command-line tools
- Direct file system processing
- Interactive frame selection
- Batch processing from folders
- Traditional workflow for local use

**Ready to start framing your artwork? Choose your preferred method above! 🖼️**