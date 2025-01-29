# TALMA-on-ALPS

This repository contains the demo code for our research work:  
**"A Physiotherapy Video Matching Method Supporting Arbitrary Camera Placement via Angle-of-Limb-based Posture Structures."**  

TALMA-on-ALPS is a physiotherapy video matching system designed to **align patient rehabilitation movements with mentor demonstrations, even when captured from different camera angles**.  
To overcome the challenges caused by **arbitrary camera placement**, we introduce the **Angle-of-Limb-based Posture Structure (ALPS)** and a **Camera-Angle-Free (CAFE) transformation**, which enable robust matching of physiotherapy exercises regardless of camera positioning.  

Our approach formulates **physiotherapy video matching** as an optimization problem and solves it using a **three-phase ALPS matching algorithm (TALMA)**.  
Real-world experiments demonstrate that TALMA-on-ALPS achieves **high precision**, with time differences **under 0.07 seconds** from expert-annotated ground truths.

![TALMA-on-ALPS Demo](https://github.com/NCKU-CIoTlab/TALMA-on-ALPS/blob/main/images/demo_picture.jpg?raw=true)

🔗 **Demo video:** [Watch on YouTube](https://www.youtube.com/watch?v=vU7GImAmCSI)

## 🚀 How to Run TALMA-on-ALPS

TALMA-on-ALPS provides a ready-to-use **Windows executable** (`PVM_test.exe`) for physiotherapy video matching. Follow these steps to **download, set up the environment, and execute the program**.

### 1️⃣ **Clone Repository with Git LFS**
⚠️ **Warning:** If you download this repository as a ZIP file from GitHub, the large binary files (such as `.exe` files) will not be included.

To correctly download the repository and its large files, you must **install Git LFS** and use `git clone`:
```bash
# 1️⃣ Install Git LFS (Skip if already installed)
git lfs install

# 2️⃣ Clone the repository with LFS support
git clone https://github.com/NCKU-CIoTlab/TALMA-on-ALPS.git
cd TALMA-on-ALPS

# 3️⃣ Pull large files
git lfs pull
```

---

### **2️⃣ Run the Prediction Program**
Run the executable file to start the physiotherapy video matching process:
```bash
./PVM_test.exe
```
This program will:
- Read the **`input.json`** file to load the necessary mentor and convalescent data.
- Perform movement matching using the TALMA-on-ALPS algorithm.
- Generate results in a new folder named with the current execution date and time.
- Save logs and matching outputs in `output.json`.

---

## 📌 Customizing `input.json`
By default, the required input files are already specified in `input.json`.  
If you want to **use your own rehabilitation recordings**, modify `input.json` with the correct file paths.

Example `input.json`:
```json
{
    "mentor": {
        "3DModel": "3D_Model/DPMentor.npy",
        "annotate": "annotate/DPMentor.json",
        "video": "video/DPMentor.mp4"
    },
    "convalescent": [
        {
            "3DModel": "3D_Model/MyConvalescent.npy",
            "video": "video/MyConvalescent.mp4"
        },
        {
            "3DModel": "3D_Model/MyConvalescent.npy",
            "video": "video/MyConvalescent.mp4"
        },
        {
            "3DModel": "3D_Model/MyConvalescent.npy",
            "video": "video/MyConvalescent.mp4"
        }
    ]
}
```
If you only have **one** convalescent video, set all three (front, right, left) paths to the same file.

---

## 📂 Understanding the Output
Once `PVM_test.exe` completes execution, it generates output files in a **timestamped folder**, structured as follows:

```
fig(YYYY-MM-DD_HH_MM_SS)/
│── Front-Front/        # Matching results for front-view convalescent video
│   ├── 1.png
│   ├── 2.png
│   ├── 3.png
│   └── ... (matching pairs)
│── Front-Right/        # Matching results for right-view convalescent video
│── Front-Left/         # Matching results for left-view convalescent video
│── TALMA P3Matching(Front-Front).png    # Visualization of matching behavior
│── TALMA P3Matching(Front-Right).png
│── TALMA P3Matching(Front-Left).png
```

### **🖼️ Explanation of Output Files**
- **`Front-Front/`, `Front-Right/`, `Front-Left/`**  
  These folders contain **matching pairs** (e.g., `1.png`, `2.png`, ...) between **mentor anchor frames** and **convalescent frames**.

- **`TALMA P3Matching(Front-XXX).png`**  
  These images provide a graphical representation of the **matching process**.

- **`output.json`**  
  Stores all text-based logs and execution outputs.

---

## ✅ Quick Summary
| **Step** | **Command** | **Description** |
|----------|------------|----------------|
| **1️⃣ Clone Repository** | `git clone https://github.com/NCKU-CIoTlab/TALMA-on-ALPS.git` | Download project files |
| **2️⃣ Install Dependencies** | `pip install -r requirements.txt` | *(Optional)* Install required libraries |
| **3️⃣ Run the Program** | `./PVM_test.exe` | Execute prediction |
| **4️⃣ Customize Input** | Edit `input.json` | Use your own 3D models and videos |
| **5️⃣ Check Output** | Look in `fig(YYYY-MM-DD_HH_MM_SS)/` | View results |

---

🚀 **Now you're ready to use TALMA-on-ALPS for physiotherapy video matching!** 🎉  
If you have any questions or suggestions for improvements, feel free to open an issue or submit a pull request! 🔥

