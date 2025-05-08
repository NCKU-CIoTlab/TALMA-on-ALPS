# TALMA-on-ALPS

This repository contains the demo code and techincal report for our research work:
**"A Physiotherapy Video Matching Method Supporting Arbitrary Camera Placement via Angle-of-Limb-based Posture Structures."**

## 📑 Technical Report 
📄 **[2025_TALMA-on-ALPS--Technical-Report.pdf](./2025_TALMA-on-ALPS--Technical-Report.pdf)**

This report extends the content of our submitted paper by including an additional **Appendix** section, which provides:
- **A. Impact of Matching Quality Threshold** (θ_{sim})
- **B. Impact of Re-Matching Control Parameter** ($\phi$)
These sections contain **experimental results and analysis** that further illustrate the effectiveness of TALMA-on-ALPS.

---

TALMA-on-ALPS is a physiotherapy video matching system designed to **align patient rehabilitation movements with mentor demonstrations, even when captured from different camera angles**.
To overcome the challenges caused by **arbitrary camera placement**, we propose the **Angle-of-Limb-based Posture Structure (ALPS)** and a **Camera-Angle-Free (CAFE) transformation**, which enable robust matching of physiotherapy exercises regardless of camera positioning.

![TALMA-on-ALPS pipeline](https://github.com/NCKU-CIoTlab/TALMA-on-ALPS/blob/main/images/pipeline.png?raw=true)

Our pipeline utilizes existing state-of-the-art pose estimation methods for constructing the 3D posture model of each subject. Specifically:

- [AlphaPose](https://github.com/MVIG-SJTU/AlphaPose) for 2D human pose estimation.
- [Dual-stream Spatio-temporal Transformer (DST)](https://github.com/eth-ait/motion-transformer) for lifting 2D keypoints to 3D space.

Our approach formulates **physiotherapy video matching** as an optimization problem and solves it using a **three-phase ALPS matching algorithm (TALMA)**.
Real-world experiments demonstrate that TALMA-on-ALPS achieves **high precision**, with time differences **under 0.07 seconds** from expert-annotated ground truths.

![TALMA-on-ALPS Demo](https://github.com/NCKU-CIoTlab/TALMA-on-ALPS/blob/main/images/demo_picture.jpg?raw=true)

🔗 **Demo video:** Download **`./demo_video.mp4`** or [watch on YouTube](https://www.youtube.com/watch?v=qgAUHp7HgRQ).

## 🚀 How to Run TALMA-on-ALPS

TALMA-on-ALPS provides **precompiled executables** for **Windows, macOS, and Linux**.
Follow the instructions below to **download, set up the environment, and execute the program** based on your operating system.


### **1️⃣ Clone the repository**
```bash
git clone https://github.com/NCKU-CIoTlab/TALMA-on-ALPS.git
cd TALMA-on-ALPS
```
---

### **2️⃣ Download the required files (Executables + Input Videos)**

The following files are **not included** in this repository due to size limitations:

- `PVM_test.exe`, `PVM_test.linux`, `PVM_test.mac` (precompiled executables)
- `input_video/` folder (physiotherapy videos used for prediction)

You can download all of them from the following Google Drive [link](https://drive.google.com/drive/folders/16_H5DXaXWCRT2OMF2ucPRLodk5s9K9nh?usp=sharing):

#### 📁 After Downloading

Please place the downloaded files directly into the **root directory** of the repository, so the folder structure looks like this:
```
your-project-folder/
├── 3D_Model/
├── images/
├── input_video/
   └── DPConvalescent.mp4
   └── DPConvalescentLeft.mp4
   └── DPConvalescentRight.mp4
├── demo_video.mp4
├── fig(2025-01-28_22_25_50)/
├── input.json
├── output.json
├── annotate/
├── README.md
├── 2025_TALMA-on-ALPS--Technical-Report.pdf
├── PVM_test.exe          ← (if you're on Windows)
├── PVM_test.linux        ← (if you're on Linux)
├── PVM_test.mac          ← (if you're on macOS)
```

### **3️⃣ Run the Prediction Program**
Choose the appropriate executable for your **operating system**:

#### **🔹 Windows**
```powershell
./PVM_test.exe
```

#### **🔹 macOS**
```bash
chmod +x PVM_test.mac
./PVM_test.mac
```

#### **🔹 Linux (Ubuntu)**
```bash
chmod +x PVM_test.linux
./PVM_test.linux
```

This program will:
- Read the **`input.json`** file to load the necessary mentor and convalescent data.
- Perform movement matching using the **TALMA-on-ALPS** algorithm.
- Generate results in a **timestamped folder** with **predicted matching outputs**.
- Save logs and execution outputs in **`output.json`**.

---

## 📌 Customizing `input.json`
By default, `input.json` is preconfigured with required files.  
To **use your own physiotherapy recordings**, modify `input.json` with your file paths.

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
**📌 If you only have one convalescent video, set all three (front, right, left) to the same file.**

---

## 📂 Understanding the Output
Once the program finishes execution, it generates **output files** in a **timestamped folder**, structured as follows:

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
| **2️⃣ Download the execution file** | *(See download guide above)* | Download from Google Cloud |
| **3️⃣ Run the Program** | **Windows:** `./PVM_test.exe` <br> **macOS:** `./PVM_test.mac` <br> **Linux:** `./PVM_test.linux` | Start matching process |
| **4️⃣ Customize Input** | Edit `input.json` | Use your own 3D models and videos |
| **5️⃣ Check Output** | Look in `fig(YYYY-MM-DD_HH_MM_SS)/` | View results |

---

🚀 **Now you're ready to use TALMA-on-ALPS for physiotherapy video matching!** 🎉  
If you have any questions or suggestions for improvements, feel free to open an issue or submit a pull request! 🔥

