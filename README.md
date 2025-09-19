# 🖼️ Image Segmentation using Graph-Based Algorithm

![C#](https://img.shields.io/badge/C%23-9.0-blue?logo=c-sharp)
![.NET](https://img.shields.io/badge/.NET-WinForms-purple?logo=dotnet)
![Algorithm](https://img.shields.io/badge/Algorithm-Graph--Based-brightgreen)
![Union-Find](https://img.shields.io/badge/DataStructure-UnionFind-orange)
![Gaussian](https://img.shields.io/badge/Filter-Gaussian-yellow)

---

## 🚀 Overview  
This project implements **Graph-Based Image Segmentation** in **C# (WinForms)**.  
The algorithm follows **Felzenszwalb and Huttenlocher's method (2004)** by:  
1. Applying **Gaussian smoothing** to reduce noise.  
2. Constructing a **graph of pixels** with weighted edges based on intensity differences.  
3. Using **Union-Find (Disjoint Set Union)** to merge regions adaptively.  
4. Generating a **segmented image** where each region is colored randomly.  

---

## 🧠 Core Concepts in Code  

### 📌 Main Components
- **`MainForm.cs`** → GUI (Open, Process, Save, Display images).  
- **`ImageOperations.cs`** → Image loading, displaying, Gaussian filter.  
- **`RGBPixel` struct** → Stores pixel (R, G, B) values.  
- **`Edge` class** → Represents graph edge with weight.  
- **`Peixel` class** → Pixel coordinates (X, Y).  
- **`unionfind` class** → DSU with path compression, union by size, and `diff` tracking.  

### 📌 Algorithm Pipeline
1. **Load Image**  
   - Using `ImageOperations.OpenImage(path)`.  
2. **Apply Gaussian Filter**  
   - `GaussianFilter1D(ImageMatrix, maskSize, sigma)`.  
   - Smooths the image before segmentation.  
3. **Graph Construction**  
   - `graph(ImageMatrix, channel)` → builds edges between neighboring pixels.  
   - Edge weight = intensity difference.  
4. **Edge Sorting**  
   - Counting sort for efficiency (`maxWeight = 255`).  
5. **Segmentation with Union-Find**  
   - `segment(ImageMatrix, channel, k)` → merges regions using threshold function:  
     ```
     merge_threshold = diff + (k / size)
     ```
   - Ensures adaptive merging.  
6. **Combine Channels**  
   - `extractcomp(Rcomponent, Gcomponent, Bcomponent)` merges R/G/B segmentations.  
7. **Generate Output Image**  
   - `imggenerate(validComponents)` → assigns random colors to regions.  
8. **Save Results**  
   - Segmented image (`.bmp`)  
   - Report file (`seg.txt`) with processing time + region sizes.  

---

## 📂 Test Cases  

🔗 [Download All Test Cases](https://drive.google.com/file/d/1h4ClRkOzEjnF2nooMk0A4SPGINQAtwci/view?usp=sharing)  

We provide four levels of test cases to validate segmentation quality and performance:  

| Level   | Description |
|---------|-------------|
| 🟢 Simple | Very basic images for quick testing and debugging |
| 🟢 Easy   | Clean images with low details |
| 🟡 Medium | Real-world images with moderate complexity |
| 🔴 Hard   | Complex images with high variations and noise |

Each test case set includes:
- Original images  
- Segmented output images  
- Segmentation reports (`seg.txt`)  

