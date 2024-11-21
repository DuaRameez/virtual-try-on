# Virtual Try-On README

## Virtual Try-On

This project is a **Virtual Try-On application** that allows users to see how different shirts look on them in real-time using a webcam. It leverages **computer vision** techniques for pose detection and overlays images of shirts onto the user’s body.

---

## Features

- **Real-time Pose Detection**: Tracks the position of key body landmarks.
- **Shirt Overlay**: Dynamically adjusts shirt size and position to fit the user's body.
- **Interactive Navigation**: Switch between shirts using hand gestures.
- **Customizable**: Add your own shirt designs to the resource folder.

---

## Requirements

- Python 3.7+
- OpenCV
- cvzone
- A webcam

---

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/DuaRameez/virtual-try-on.git
   cd virtual-try-on
   ```

2. **Install Dependencies**:
   Use `pip` to install the required packages:
   ```bash
   pip install opencv-python cvzone mediapipe
   ```

3. **Add Shirt Designs**:
   Place PNG images of shirts (with transparent backgrounds) in the `Resources/Shirts` folder.

---

## Usage

1. Run the application:
   ```bash
   python virtual_try_on.py
   ```

2. The application will open a webcam feed:
   - Use **hand gestures** to navigate between shirts:
     - **Right hand**: Swipe to switch to the next shirt.
     - **Left hand**: Swipe to switch to the previous shirt.

---

## File Structure

```
virtual-try-on/
│
├── Resources/
│   ├── Shirts/             # Folder containing shirt images
│   └── button.png          # Button image for navigation
│
├── virtual_try_on.py       # Main Python script
└── README.md               # Project documentation
```

---

## Customization

- Add more shirt designs by placing PNG files in the `Resources/Shirts` folder.
- Adjust **fixedRatio** and **shirtRatioHeightWidth** values in the code to fine-tune the shirt scaling.

---

## Contributing

Contributions are welcome! Feel free to:
- Add new features.
- Improve gesture control.
- Optimize performance.

Fork the repository, create a new branch for your feature, and submit a pull request.

---

## Acknowledgments

- Inspired by the **cvzone** library for simplifying computer vision tasks.
- Thanks to the **OpenCV** community for their resources and support.
