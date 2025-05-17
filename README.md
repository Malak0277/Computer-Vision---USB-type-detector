# USB Connector Type Identifier

This project is a computer vision-based system that can automatically identify and classify different types of USB connectors from images.

## Overview

The USB Connector Type Identifier uses image processing and machine learning techniques to analyze images of USB connectors and determine their type (USB-A, USB-B, USB-C, Micro-USB, or Mini-USB). The system extracts various features from the input image and uses a rule-based classification approach to identify the connector type.

## Features

- **Automatic USB connector type identification** from images
- **Support for 5 common USB types**:
  - USB-A
  - USB-B
  - USB-C
  - Micro-USB
  - Mini-USB
- **Visual debug mode** showing intermediate processing steps
- **Confidence scoring** for classification results
- **Detailed explanation** of classification reasoning

## Requirements

- Python 3.6+
- OpenCV (cv2)
- NumPy
- Matplotlib
- Enum (from the standard library)

## Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/Malak0277/Computer-Vision---USB-type-detector.git
   cd usb-connector-identifier
   ```

2. Install required dependencies:
   ```bash
   pip install opencv-python numpy matplotlib
   ```

## Usage

### Basic Usage

```python
import cv2 as cv
from usb_identifier import process_image

# Load an image and identify the USB connector type
image_path = "path/to/your/usb/image.jpg"
image = cv.imread(image_path)
usb_type, confidence, reason, result_img = process_image(image)

# Print results
print(f"USB Type: {usb_type.value}")
print(f"Confidence: {confidence:.2f}")
print(f"Reason: {reason}")

# Save result image
cv.imwrite('result.jpg', result_img)
```

### Debug Mode

To enable visual debugging that shows intermediate processing steps:

```python
# Set debug_mode to True at the beginning of your script
debug_mode = True
```

This will display visualizations of:
- Preprocessing steps
- Feature extraction
- Classification results

## How It Works

The system follows these main steps:

1. **Preprocessing**
   - Convert image to grayscale
   - Apply Gaussian blur for noise reduction
   - Perform Canny edge detection
   - Find contours in the image
   - Extract the region containing the USB connector

2. **Feature Extraction**
   - Calculate geometric features (aspect ratio, area, perimeter, compactness)
   - Detect corners using Harris corner detection
   - Analyze symmetry and rectangularity
   - Identify internal structures like pins and central lines
   - Measure end roundedness

3. **Classification**
   - Score each USB type based on extracted features
   - Apply rule-based classification logic
   - Calculate confidence scores
   - Determine the most likely USB type

4. **Visualization**
   - Display the original image with overlaid classification results
   - Show confidence score and reasoning

## Feature Importance

The system uses these key features to distinguish between USB types:

- **USB-A**: Typically has aspect ratio 2.0-3.1, high rectangularity, and horizontal pins
- **USB-B**: Nearly square aspect ratio (0.9-1.4), high rectangularity, larger size
- **USB-C**: Aspect ratio 2.7-3.7 with a strong central line and good symmetry
- **Micro-USB**: Aspect ratio 2.6-5.0, smaller size, and specific compactness profile
- **Mini-USB**: Aspect ratio 2.2-2.5 with distinct edge profile and corner count

## Examples

Example classification result for a USB-C connector:

```
USB Type: USB-C
Confidence: 1.00
Reason: Aspect ratio 3.04 fits USB-C range, Good symmetry (score: 0.0173), 
        Strong central line (0.99 of width), Size (area: 1661.0) fits USB-C range, 
        Rectangularity 0.90 fits USB-C profile, Strong central line with ideal USB-C aspect ratio, 
        Size and aspect ratio combination ideal for USB-C
```

## Future Improvements

- Add support for more USB types (Lightning, Thunderbolt, etc.)
- Implement machine learning approach for more robust classification
- Improve preprocessing for handling poor lighting conditions
- Add batch processing capabilities for multiple images
- Create a simple GUI for easier usage


## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
