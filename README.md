https://github.com/DipaCaturAsyafa/Road-Lane-Detection-OpenCV/releases

[![Releases](https://img.shields.io/badge/Releases-OpenCV-blue?logo=github&style=for-the-badge)](https://github.com/DipaCaturAsyafa/Road-Lane-Detection-OpenCV/releases)

# Road Lane Detection with OpenCV for Real-Time Driving Lane Tracking

A computer vision project using OpenCV to detect road lane lines in driving videos. It processes video frame-by-frame using edge detection, region masking, Hough transforms, and overlays lane lines to assist self-driving logic.

- Topics: ai-project, autonomous-driving, computer-vision, cv2, deep-learning, github, image-processing, lane-detection, machine-learning, object-detection, opencv-projects, python, road-lane-detection, self-driving-cars, video-processing

Hero image
![Road Lane Detection Hero](https://picsum.photos/1200/400?text=Road+Lane+Detection+Demo)

Introduction to the project
- This project focuses on extracting lane lines from driving videos.
- It uses a frame-by-frame approach to analyze each image from a video feed.
- The core steps include edge detection, masking the region of interest, line detection, and drawing lane overlays.
- The goal is to provide reliable lane information that can feed autonomous driving logic or driver assistance features.

Why this project matters
- Lane detection is a foundational task for autonomous driving and advanced driver assistance systems.
- A simple yet robust pipeline helps researchers prototype ideas quickly.
- OpenCV-based solutions are cross-platform, lightweight, and easy to extend.

Key features
- Real-time frame processing from video input
- Edge detection to highlight boundaries
- Region of interest masking to focus on road area
- Hough transform for lane line detection
- Overlay of lane lines on original frames
- Configurable thresholds and ROI shapes
- Visualization options for debugging and tuning
- Compatibility with common video formats and camera inputs

Tech stack
- Python
- OpenCV (cv2)
- NumPy
- Optional: Matplotlib for plotting and debugging
- Optional: pyvirtualdisplay or similar tools for headless environments

How it works: the pipeline at a glance
- Read a video or image sequence frame by frame
- Convert to grayscale to simplify processing
- Apply Gaussian blur to reduce noise
- Detect edges with the Canny algorithm
- Define a polygon region of interest where lanes usually appear
- Mask the frame using the ROI to ignore irrelevant areas
- Run the Hough transform to find line segments
- Separate line segments into left and right lane candidates
- Fit lines to these candidates to create stable lane lines
- Overlay the lane lines on the original frame
- Optionally compute a curvature estimate and vehicle offset

Code structure overview
- main/
  - drive.py or run.py: entry point to process a video stream
  - pipeline.py: the core image processing steps
  - lanes.py: lane detection and fitting utilities
- tests/
  - test_pipeline.py: basic checks for the pipeline output
  - test_lane_fitting.py: verification of line fitting behavior
- assets/
  - sample_videos/: example driving videos for testing
  - sample_frames/: extracted frames for quick checks
- configs/
  - default.yaml: default parameters for ROI, thresholds, and line fitting
- docs/
  - overview.md: additional explanations and diagrams
- requirements.txt
- README.md (this file)
- setup.py or pyproject.toml (optional, for packaging)

Usage and getting started
- Prerequisites
  - Python 3.8 or higher
  - OpenCV installed (opencv-python or opencv-python-headless)
  - NumPy installed
  - Optional: ffmpeg or avconv for video I/O
- Quick start for local runs
  - Create a virtual environment
    - python -m venv venv
    - source venv/bin/activate (Linux/macOS) or venv\Scripts\activate (Windows)
  - Install dependencies
    - pip install -r requirements.txt
  - Run on a sample video
    - python main/run.py --input sample_videos/test_drive.mp4 --output results/drive_lanes.mp4
  - View results
    - Open results/drive_lanes.mp4 with any video player
- How to customize
  - ROI polygon shape and thresholds live in configs/default.yaml
  - You can switch on/off visualization overlays
  - You can adjust the smoothing factor for lane lines to reduce flicker

Configuration and tuning tips
- Region of Interest (ROI)
  - The ROI is a polygon that covers the road area and excludes the sky and car hood.
  - A tight ROI reduces noise but may miss lanes at the far end. Start broad, then tighten.
- Edge detection thresholds
  - Canny thresholds control sensitivity to edges. Lower thresholds find more edges, but increase noise.
  - Balance edge detection with the ROI to keep a clean lane signal.
- Hough transform parameters
  - The distance and angle resolution affect line detection density.
  - Tuning helps to separate true lane lines from spurious edges.
- Lane fitting
  - Fit lines using linear regression on detected segments.
  - Apply smoothing over frames to reduce jitter.
  - Consider different models for left and right lanes if the camera angle changes.
- Visualization
  - Toggle lane overlay, curvature display, and offset indicator for debugging.
  - Use a transparent overlay to help side-by-side comparisons with the original frame.

How to run tests locally
- Install test dependencies (if separated from main requirements)
  - pip install pytest
- Run tests
  - pytest tests/

Examples and demonstrations
- Simple test with a static frame
  - python main/run.py --input assets/test_frames/frame_001.jpg --output results/frame_001_detected.jpg
- Live camera input (if you have a camera)
  - python main/run.py --input 0 --output results/camera_output.mp4
- Batch processing of a folder
  - python main/run.py --input-dir assets/test_frames/ --output results/batch/

Edge cases and known limitations
- Night scenes may reduce visibility of lane markings.
- Heavy shadows across the road can cause false positives.
- Road markings in construction zones may appear as broken lines; filtering helps but may still misclassify.
- Extremely curved roads require adaptive ROI or alternative lane models.

How to extend this project
- Improve lane detection with Kalman filtering to predict lane positions between frames.
- Add a curvature model to estimate road curvature more robustly.
- Integrate segmentation-based lane priors to handle faded paint.
- Add camera calibration utilities to correct perspective distortion.
- Support different camera mounting angles with adjustable ROI.
- Implement a multi-threaded pipeline to boost throughput on GPUs or multi-core CPUs.
- Create a small GUI to tweak parameters in real time.

Data preparation and synthetic testing
- Use synthetic video sequences to calibrate edge detectors and ROI.
- Generate synthetic frames with painted lines and varying lighting to test resilience.
- Create unit tests for each processing stage: edge detection, ROI masking, and Hough-based line extraction.
- Maintain a small corpus of representative frames for regression tests.

Performance and hardware notes
- OpenCV with Python is light on memory usage and runs well on consumer laptops.
- Real-time performance depends on video resolution and frame rate.
- For higher frame rates, reduce resolution or optimize the ROI and Hough parameters.
- If you need speed, consider using precompiled OpenCV wheels with optimizations or switching to a compiled language for bottlenecks.

Deployment considerations
- In a vehicle or edge device, ensure the processing latency stays within acceptable bounds.
- Implement hardware checks to ensure OpenCV can access the camera or video source.
- Safeguard against processing failures by providing a fallback mode that uses a previous lane estimate.

How to contribute
- Fork the repository and clone locally.
- Create a feature branch for your changes.
- Run the test suite and verify no regressions.
- Document any new configuration options in configs/ and docs/overview.md.
- Submit a pull request with a clear description of the change and testing steps.

Releases and assets
- The primary distribution for this project is hosted in the Releases section.
- The link above points to the official Releases page where you can download prebuilt artifacts or source snapshots.
- From the Releases page, download the main release artifact named RoadLaneOpenCV_V1.0.zip (example) and run the executable or extract and run the Python scripts as described in the Getting Started section.
- The Releases page contains the file you need to download and execute. For details, visit the link again: https://github.com/DipaCaturAsyafa/Road-Lane-Detection-OpenCV/releases
- If you seek a direct download, you will find the asset labeled RoadLaneOpenCV_V1.0.zip (example) on the Releases page, which you should download and run.

Usage notes for the Releases approach
- The release artifact typically contains a bundled environment with dependencies preinstalled.
- Running the provided executable should launch a demo or a sample pipeline with preset videos.
- If you prefer to run the code directly, you can use the source files and install dependencies from requirements.txt as described in Getting Started.
- Always verify the release notes for compatibility with your platform and Python version.

Developer notes
- The codebase emphasizes readability and straightforward logic.
- Functions are modular, with clear responsibilities for edge detection, ROI masking, line extraction, and overlay rendering.
- Unit tests cover the essential parts, ensuring changes do not break core behavior.
- Comments explain the rationale behind parameter choices and algorithm steps.

Common troubleshooting steps
- If no output video is produced, check the input path and ensure the output directory exists.
- If an error mentions OpenCV not finding a video or camera, verify permissions and device availability.
- If frames flicker, adjust smoothing or apply a stronger ROI mask.
- If the process is slow, reduce the input resolution or optimize Hough thresholds.

Licensing
- This project uses open source components from the OpenCV ecosystem.
- See LICENSE for the exact terms and conditions.
- Respect the licenses of any included sample data or third-party assets.

Changelog (high level)
- v1.0: Initial release with frame-by-frame lane detection, ROI masking, Canny edges, Hough lines, and overlay.
- v1.1: Improved smoothing, added curvature and offset visualization, updated defaults for various road types.
- v1.2: Architectural refactor to separate pipeline stages, added tests, and improved documentation.
- v1.3: Enhanced robustness in challenging lighting and weather conditions.

FAQ
- Q: Can I use this on real cars?
  A: Yes, with careful adaptation. Run in a safe testing environment first and ensure your system’s latency is acceptable.
- Q: Do I need a GPU?
  A: Not strictly. CPU-based OpenCV works, but GPUs can speed up processing for higher resolutions.
- Q: How do I extend the ROI?
  A: Update the ROI polygon in the configuration file and test with different camera angles.

Best practices for learners
- Start with a single video and a small ROI. Get stable lanes first.
- Print intermediate images or plots to understand how edges and lines evolve.
- Keep a log of parameter changes to trace improvements.
- Validate results on diverse lighting and road conditions.

Appendix: terminology and concepts
- Edge detection: identifies boundaries where intensity changes sharply.
- ROI: the polygons that focus the analysis on the road area.
- Canny: an edge detector that highlights strong edges with gradient information.
- Hough transform: a method to detect lines by transforming points to parameter space.
- Lane overlay: the colored lines drawn on the video to show detected lanes.
- Curvature: a measure of how sharply the road bends, inferred from the lane geometry.

Roadmap and future plans
- Integrate color-based lane hints to support white and yellow lane markings in varied conditions.
- Add motion models to predict lane positions when frames are lost.
- Explore deep learning hybrids that combine traditional features with lightweight neural networks for better robustness.
- Build a small visualization dashboard to tune parameters live.
- Extend to multi-camera setups with perspective stitching for wider coverage.

Notes
- This README emphasizes clarity and practical guidance.
- It is designed for developers, researchers, and enthusiasts who want to experiment with lane detection using OpenCV.
- The project remains approachable for beginners while offering room to grow into advanced topics.

End of document
- The content above is structured to be informative, actionable, and easy to navigate.
- It reflects the repository’s focus on road lane detection using OpenCV in Python.
- The linked releases page is highlighted for access to downloadable artifacts and related assets.