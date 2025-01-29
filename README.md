# TALMA-on-ALPS

This repository contains the demo code and techincal report for our research work:  
**"A Physiotherapy Video Matching Method Supporting Arbitrary Camera Placement via Angle-of-Limb-based Posture Structures."**  

## 📑 Technical Report  
📄 **`2025_TALMA-on-ALPS--Technical-Report.pdf`**  

This report extends the content of our submitted paper by including an additional **Appendix** section, which provides:  
- **A. Impact of Matching Quality Threshold** (θ_{sim})  
- **B. Impact of Re-Matching Control Parameter** ($\phi$)  
These sections contain **experimental results and analysis** that further illustrate the effectiveness of TALMA-on-ALPS.

---

TALMA-on-ALPS is a physiotherapy video matching system designed to **align patient rehabilitation movements with mentor demonstrations, even when captured from different camera angles**.  
To overcome the challenges caused by **arbitrary camera placement**, we introduce the **Angle-of-Limb-based Posture Structure (ALPS)** and a **Camera-Angle-Free (CAFE) transformation**, which enable robust matching of physiotherapy exercises regardless of camera positioning.  

Our approach formulates **physiotherapy video matching** as an optimization problem and solves it using a **three-phase ALPS matching algorithm (TALMA)**.  
Real-world experiments demonstrate that TALMA-on-ALPS achieves **high precision**, with time differences **under 0.07 seconds** from expert-annotated ground truths.

![TALMA-on-ALPS Demo](https://github.com/NCKU-CIoTlab/TALMA-on-ALPS/blob/main/images/demo_picture.jpg?raw=true)

🔗 **Demo video:** [Watch on YouTube](https://www.youtube.com/watch?v=vU7GImAmCSI)

## 🚀 How to Run TALMA-on-ALPS

TALMA-on-ALPS provides **precompiled executables** for **Windows, macOS, and Linux**.  
Follow the instructions below to **download, set up the environment, and execute the program** based on your operating system.

### 1️⃣ **Clone Repository with Git LFS**
⚠️ **Important:**  
**Do not download the repository as a ZIP file from GitHub!**  
ZIP downloads **do not include large binary files** (e.g., `.exe`, `.mac`, `.linux`).  
Instead, **install Git LFS and use `git clone`** to properly fetch all files.

#### **🔹 Install Git LFS**
##### **For Windows**  
Download and install Git LFS from: [https://git-lfs.github.com](https://git-lfs.github.com)  
Then, initialize Git LFS:
```powershell
git lfs install
```

##### **For macOS (Homebrew)**
```bash
brew install git-lfs
git lfs install
```

##### **For Ubuntu (Linux)**
```bash
sudo apt update
sudo apt install git-lfs
git lfs install
```

#### **🔹 Clone the repository**
Once Git LFS is installed, you can clone the repository:
```bash
git clone https://github.com/NCKU-CIoTlab/TALMA-on-ALPS.git
cd TALMA-on-ALPS
```

#### **🔹 Pull Large Files (if necessary)**
Usually, `git clone` will automatically pull large files if Git LFS is installed.  
If large files are missing, manually pull them with:
```bash
git lfs pull
```

---

### **2️⃣ Run the Prediction Program**
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
| **2️⃣ Install Git LFS** | *(See installation guide above)* | Required for large files |
| **3️⃣ Run the Program** | **Windows:** `./PVM_test.exe` <br> **macOS:** `./PVM_test.mac` <br> **Linux:** `./PVM_test.linux` | Start matching process |
| **4️⃣ Customize Input** | Edit `input.json` | Use your own 3D models and videos |
| **5️⃣ Check Output** | Look in `fig(YYYY-MM-DD_HH_MM_SS)/` | View results |

---

🚀 **Now you're ready to use TALMA-on-ALPS for physiotherapy video matching!** 🎉  
If you have any questions or suggestions for improvements, feel free to open an issue or submit a pull request! 🔥

