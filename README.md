# 🖼️ MATLAB Image Processing Application

## 📌 Project Overview
This project is a **MATLAB App Designer application** for implementing and visualizing **basic and advanced image processing operations**.

The application allows users to load an image, apply different **spatial and intensity-based filters**, preview the processed image, and save the result.  
All operations are implemented **manually using pixel-level processing**, not relying on MATLAB built-in high-level image processing functions (except basic I/O).

---

## 🎯 Project Objectives
- Understand digital image representation
- Implement image processing algorithms manually
- Apply spatial and intensity transformations
- Practice GUI-based image processing using MATLAB App Designer
- Visualize original and processed images side by side

---

## 🛠️ Technologies Used
- **MATLAB**
- **MATLAB App Designer**
- **Image Processing Concepts**
- **Matrix & Pixel Manipulation**

---

## 📂 Application Features

### 🔹 File Operations
- Browse and load images (`.jpg`, `.png`, `.bmp`)
- Display original image
- Save processed image in different formats

---

## 🧠 Implemented Image Processing Operations

### 1️⃣ RGB to Grayscale Conversion
Converts a color image to grayscale using weighted intensity formula:

```matlab
Gray = 0.2989*R + 0.5870*G + 0.1140*B;
