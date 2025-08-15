# Object-Detection-and-Tracking
# 🎯 Object Detection & Tracking with YOLOv8 (VisDrone Dataset)

This project uses **YOLOv8** to perform object detection on image sequences from the **VisDrone2019-VID** dataset.  
It overlays **predicted bounding boxes** from YOLO along with **ground truth annotations**, displays results in real time, and exports the processed video.

---

## 📖 Overview
The script:
1. Loads a YOLOv8 model (nano by default).
2. Reads a sequence of images from the VisDrone dataset.
3. Performs object detection on each frame.
4. Draws:
   - **Predictions** (Green for persons, Red for vehicles)
   - **Ground Truth Annotations** (Blue)
5. Saves the annotated frames into `output_detection.mp4`.
6. Shows the processed frames live in an OpenCV window.

---

## 🛠 Features
- **YOLOv8 Inference** using the [Ultralytics](https://github.com/ultralytics/ultralytics) library.
- **Ground Truth Overlay** from VisDrone annotation files.
- **Custom Label Mapping**:
  - Class `0` → "person" (Green box)
  - Any other class → "vehicle" (Red box)
- **Real-Time Display** with OpenCV.
- **Video Export** as `output_detection.mp4`.
- **Error Handling** for missing files or malformed annotation lines.

---

## 📂 Dataset Structure
This script is designed for the **VisDrone2019-VID** dataset.  
It expects the following folder structure:

```

base\_path/
├── sequences/
│    ├── video\_sequence\_folder/
│    │     ├── 0000001.jpg
│    │     ├── 0000002.jpg
│    │     └── ...
├── annotations/
│    ├── video\_sequence\_folder.txt
│    └── ...

```

- **sequences/** → Contains subfolders for each video sequence (each containing sequential image frames).
- **annotations/** → Contains `.txt` annotation files for each sequence, named identically to the sequence folder.

---

## 🖼 Annotation Format
VisDrone annotation `.txt` files contain rows in the format:
```

frame\_id, object\_id, x, y, width, height, score, class\_id, visibility

````
This script uses:
- **frame_id** → To match annotations to frames.
- **object_id** → For labeling ground truth boxes.
- **x, y, width, height** → Bounding box coordinates.
- **class_id** → To identify object category.

---

## ⌨️ Controls
- **Press `q`** → Quit early while processing.

---

## 📦 Requirements
- Python 3.x
- OpenCV
- Ultralytics YOLOv8

Install dependencies:
```bash
pip install ultralytics opencv-python
````

---

## 🚀 How to Run

### 1️⃣ Clone the repository

```bash
git clone https://github.com/your-username/visdrone-yolov8-tracking.git
cd visdrone-yolov8-tracking
```

### 2️⃣ Place the dataset

Ensure your `VisDrone2019-VID-train` folder (or equivalent) is structured as shown in **Dataset Structure** above.

### 3️⃣ Run the script

```bash
python detect_and_track.py
```

You can modify the model or sequence index in the script:

```python
model = YOLO("yolov8n.pt")  # Change to 'yolov8s.pt' or 'yolov8m.pt' for higher accuracy
first_sequence_folder = sequence_folders[20]  # Change the index to pick another sequence
```

---

## 📸 Output Example

* **Green Box** → YOLO prediction: person
* **Red Box** → YOLO prediction: vehicle
* **Blue Box** → Ground truth annotation

The processed video is saved as:

```
output_detection.mp4
```

---

## 🔍 Tracking Note

Currently, this script:

* Processes frames sequentially.
* Displays ground truth **object IDs**.
* Does **not** implement an ID persistence algorithm like **SORT** or **DeepSORT** for predicted tracks.

This means YOLO detects objects per frame independently. For continuous tracking (same object ID across frames), you can extend this script by integrating SORT/DeepSORT.

---

```

If you want, I can also **include an ASCII art camera 🎥** at the top of this README so it looks visually catchy, just like a gaming project README.  
That would make your detection project look more polished and unique.
```
