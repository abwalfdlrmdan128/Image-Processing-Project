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
 % im=rgb2gray(app.Image);
            % imshow(im);

               img=double(app.Image);
               [m, n, ~] = size(img);     
               gray = zeros(m, n);        
               for row = 1:m
                for col = 1:n
                    R = img(row, col, 1);
                    G = img(row, col, 2);
                    B = img(row, col, 3);
                    gray(row, col) = 0.2989*R + 0.5870*G + 0.1140*B;
                end
               end
                    app.ProcessedImage=gray;
                    imshow(gray, 'Parent', app.UIAxes_2);
                    axis(app.UIAxes_2, 'image');
                    axis(app.UIAxes_2, 'off');
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
        % K=20;
        %  if isfloat(app.Image)
        %     img = im2uint8(app.Image);   % convert to uint8
        % else
        %     img = app.Image;
        % end
        %     [m, n, c] = size(app.Image);
        %     zoomed = zeros(m*K, n*K, c,'uint8');
        % 
        % for i = 1:m
        %     for j = 1:n
        %         for x= 1:c
        %             zoomed((i-1)*K+1:i*K, (j-1)*K+1:j*K, x) =img(i,j,x);
        %         end
        %     end
        % end
        %     app.ProcessedImage=zoomed;
        %     imshow(zoomed, 'Parent', app.UIAxes_2);
        %     axis(app.UIAxes_2, 'image');
        %     axis(app.UIAxes_2, 'off');
        img=app.Image;
        [n,m,t]=size(img);
        k=str2double(app.EditField_5.Value);
        f=zeros(k*n,k*m,t);
        c = 1; 
        r = 1; 
       for o=1:t
        for x = 1:size(img, 1) 
           for y = 1:size(img, 2) 
               f(r:r+k-1, c:c+k-1,o) = img(x, y,o); 
               c = c + k; 
           end 
           c = 1; 
           r = r + k; 
        end 
        r=1;
       end
        app.ProcessedImage = f;
        imshow(f, 'Parent', app.UIAxes_2); 
        axis(app.UIAxes_2, 'image');        
        axis(app.UIAxes_2, 'off');       
        zoom(app.UIAxes_2, 'on');             
        pan(app.UIAxes_2, 'on');



        % K=20;
        %  if isfloat(app.Image)
        %     img = im2uint8(app.Image);   % convert to uint8
        % else
        %     img = app.Image;
        % end
        %     [m, n, c] = size(app.Image);
        %     zoomed = zeros(m*K, n*K,'uint8');
        % 
        % for i = 1:m
        %     for j = 1:n
        % 
        %             zoomed((i-1)*K+1:i*K, (j-1)*K+1:j*K) =img(i,j);
        % 
        %     end
        % end
        %     app.ProcessedImage=zoomed;
        %     imshow(zoomed, 'Parent', app.UIAxes_2);
        %     axis(app.UIAxes_2, 'image');
        %     axis(app.UIAxes_2, 'off');
        img=app.Image;
        [n,m]=size(img);
        k=str2double(app.EditField_6.Value);
        f=zeros(k*n,k*m);
        c = 1; 
        r = 1; 
        for x = 1:size(img, 1) 
           for y = 1:size(img, 2) 
               f(r:r+k-1, c:c+k-1) = img(x, y); 
               c = c + k; 
           end 
           c = 1; 
           r = r + k; 
        end 
        app.ProcessedImage = f;
        imshow(f, 'Parent', app.UIAxes_2); 
        axis(app.UIAxes_2, 'image');        
        axis(app.UIAxes_2, 'off');       
        zoom(app.UIAxes_2, 'on');  
```
3️⃣ Zero Order Zooming (Interpolation)

Enlarges image by inserting average values between pixels.

📌 Purpose:

Reduce blocky appearance

Improve visual smoothness

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
4️⃣ Brightness Enhancement (Log Transformation)

Applies logarithmic intensity transformation:

📌 Purpose:

Enhance low-intensity (dark) regions

Compress high-intensity values

```matlab
c = app.BrightnessButtonSlider.Value;
            img =double(app.Image);                       
            Transform = c * log(1 + img);
            Transform = uint8(Transform);
            app.ProcessedImage = Transform;
            imshow(Transform, 'Parent', app.UIAxes_2);
            axis(app.UIAxes_2, 'image');
            axis(app.UIAxes_2, 'off');
```

5️⃣ Average Filter (Smoothing Filter)

Applies a 3×3 mean filter to reduce noise. 

📌 Purpose:

Noise reduction

Image smoothing

✔️ Supports:

Grayscale images

Color images (channel-wise processing)
```matlab
if(app.ColorCheckBox.Value)
            img = app.Image;
            [n,m,~] = size(img);
            k = (1/9);
            f = zeros(n,m,3);
            for c = 1:3      
                for i = 1:n-2
                    for j =1:m-2
                        f(i,j,c) =k*sum(sum(img(i:i+2, j:j+2, c)));
                    end
                end
            end
            imshow(f, 'Parent', app.UIAxes_2);
            app.ProcessedImage = f;
           else

            img=app.Image;
            [n,m]=size(img);
            f=zeros(n,m);
            k=(1/9);
            for i=1:n-2
                for j=1:m-2
                    f(i,j)=k*sum(sum(img(i:i+2,j:j+2)));
                end
            end
            imshow(f, 'Parent', app.UIAxes_2);
            app.ProcessedImage=f;
            axis(app.UIAxes_2, 'image');
            axis(app.UIAxes_2, 'off');
          end                     
```
6️⃣ Salt & Pepper Noise

Adds impulse noise to the image using:

📌 Purpose:

Simulate noise for filter testing
```matlab
img=app.Image;
             img=imnoise(img,"salt & pepper",0.05);
             imshow(img, 'Parent', app.UIAxes_2);
             app.ProcessedImage=img;
             axis(app.UIAxes_2, 'image');
             axis(app.UIAxes_2, 'off');
```


7️⃣ Median Filter

Removes impulse noise by replacing pixel values with the median of a 3×3 neighborhood.

📌 Purpose:

Effective for salt & pepper noise

Preserves edges better than average filter

```matlab
  img=app.Image;
         [n,m]=size(img);
         f=zeros(n,m);
         if ndims(img) == 3
            img = rgb2gray(img);
         end
         for x = 1 : size(img, 1) - 2 
           for y = 1:size(img, 2) - 2 
               o = sort(img(x:x+2, y:y+2)); 
               f(x,y) = o(5); 
           end 
         end 
             imshow(f, 'Parent', app.UIAxes_2);
             app.ProcessedImage=f;
             axis(app.UIAxes_2, 'image');
             axis(app.UIAxes_2, 'off');

        % % Min Filter (Used for removing Salt noise) 
        % for x = 1 : size(img, 1) - 2 
        %    for y = 1 : size(img, 2) - 2 
        %        o = min(min(img(x:x+2, y:y+2))); 
        %        f(x,y) = o; 
        %    end 
        % end 
        % 
        % 
        % 
        % % Max Filter (Used for removing Pepper noise) 
        % for x = 1 : size(img, 1) - 2 
        %    for y = 1 : size(img, 2) - 2 
        %        o = max(max(img(x:x+2, y:y+2))); 
        %        f(x,y) = o; 
        %    end 
        % end 
```

8️⃣ Intensity Level Slicing

Highlights specific intensity ranges while keeping others unchanged. 

📌 Purpose:

Highlight specific gray-level regions

Feature extraction

```matlab
img =im2uint8(app.Image);
        s =img;
        for x =1:size(img, 1)
            for y = 1:size(img, 2)
                if img(x,y) <50 && img(x,y) >10
                    s(x,y) = 255;
                else
                    s(x,y) = img(x,y);
                end
            end
        end
        
        imshow(s, 'Parent', app.UIAxes_2);
        axis(app.UIAxes_2,'image');
        axis(app.UIAxes_2,'off');
        app.ProcessedImage = s;
```

9️⃣ Contrast Stretching

Enhances image contrast using normalization: 

📌 Purpose:

Improve low-contrast images

Expand dynamic range

```matlab
 img = im2uint8(app.Image); 
        x_min = min(img(:)); 
        x_max = max(img(:)); 
        delta = x_max - x_min; 
        new = ((img - x_min) / delta) * 255;
          app.ProcessedImage = new;
          imshow(new, 'Parent', app.UIAxes_2);
          axis(app.UIAxes_2, 'image');
          axis(app.UIAxes_2, 'off');
```

🔟 Image Flipping

Horizontal flip (Left–Right)

Vertical flip (Up–Down)

📌 Purpose:

Geometric transformation

Image alignment

```matlab
  imm=app.Image;
            if (app.LeftRightCheckBox.Value)
                imm=fliplr(imm);
            end
            if (app.UpDownCheckBox.Value)
                imm = flipud(imm);
            end
          app.ProcessedImage = imm;
          imshow(imm, 'Parent', app.UIAxes_2);
          axis(app.UIAxes_2, 'image');
          axis(app.UIAxes_2, 'off');
```

1️⃣1️⃣ Image Rotation

Rotates image by multiples of 90 degrees using:

📌 Purpose:

Orientation correction
```matlab
    value=app.EditField_4.Value;
            img=app.Image;
            imm=rot90(img,str2double(value));
            app.ProcessedImage = imm;
            imshow(imm, 'Parent', app.UIAxes_2);
            axis(app.UIAxes_2, 'image');
            axis(app.UIAxes_2, 'off');
```

1️⃣2️⃣ Transpose & Negative

Transpose the image matrix

Apply image negative:

📌 Purpose:

Matrix transformation

Intensity inversion

```matlab
 img = app.Image;
        % Transpose
        img_t = img.'; 
        % Negative
        img_t_neg = 1 - img_t;
        app.ProcessedImage = img_t_neg;
        imshow(app.ProcessedImage, 'Parent', app.UIAxes_2);
        axis(app.UIAxes_2, 'image');
        axis(app.UIAxes_2, 'off');
```

Browse Button
```matlab
[file, path] = uigetfile({'*.jpg;*.png;*.bmp','Images'}, 'Select Image');
        
            if isequal(file, 0)
                return;
            end
    
            img = imread(fullfile(path, file));
            img = im2double(img);
            app.Image=img;
            app.PathFill=fullfile(path,file);
            app.FileName=file;
            imshow(img, 'Parent', app.UIAxes_3);
            axis(app.UIAxes_3, 'image');
            axis(app.UIAxes_3, 'off');
            app.EditField_2.Value=path;
            app.EditField.Value=file;
            app.EditField_3.Value=fullfile(path, file);
```

Save Button

```matlab
         
        % Ask user where to save the file
         [file, path] = uiputfile({...
        '*.jpg','JPEG Image (*.jpg)'; 
        '*.png','PNG Image (*.png)'; 
        '*.tif','TIFF Image (*.tif)'; 
        '*.bmp','Bitmap Image (*.bmp)'}, ...
        'Save Image As');

        % User pressed Cancel
        if isequal(file,0)
            return;
        end
    
        % Full file path
        fullpath = fullfile(path, file);
        % Example image to save (replace with your image variable)
        imgToSave = app.ProcessedImage ;   % or app.OriginalImage
        % Save the image
        imwrite(imgToSave, fullpath);
        msgbox('Image saved successfully','Success');
```
