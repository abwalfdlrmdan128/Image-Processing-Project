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
```

### 2️⃣ K-Time Zooming (Pixel Replication)
🔸 RGB Image Zooming

Replicates each pixel K × K times to enlarge the image.

📌 Method:

Zero-order hold interpolation

Manual pixel replication

🔸 Grayscale Image Zooming

Same concept applied to grayscale images.
```matlab
img = app.Image;  
        [rows, cols] = size(img); 
        intermediate_rows = 2*rows - 1;
        row_interpolated_img = zeros(intermediate_rows, cols); 
        
        for i = 1:rows
            row_interpolated_img(2*i-1,:) = img(i,:);
            if i < rows
                row_interpolated_img(2*i,:) = (img(i,:) + img(i+1,:)) / 2;
            end
        end
        
        intermediate_cols = 2*cols - 1;
        zoomed_img = zeros(intermediate_rows, intermediate_cols); 
        
        for j = 1:cols
            zoomed_img(:,2*j-1) = row_interpolated_img(:,j);
            if j < cols
                zoomed_img(:,2*j) = (row_interpolated_img(:,j) + row_interpolated_img(:,j+1)) / 2;
            end
        end
        
        app.ProcessedImage = zoomed_img;
        imshow(app.ProcessedImage, 'Parent', app.UIAxes_2);
        axis(app.UIAxes_2,'image');
        axis(app.UIAxes_2,'off');
```

