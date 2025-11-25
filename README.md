# 📚 Product Recognition of Books

This repository contains the solution for **Assignment Module 1: Image Processing and Computer Vision**. The goal of this project is to develop a computer vision system capable of recognizing specific books on shelves and estimating their pose using **traditional computer vision techniques**.

## 👥 Authors
* **Omid Nejati**
* **Alireza Shahidiani**

## 🎯 Project Objective
Given a set of reference images (models of books) and a set of scene images (shelves containing various books), the system must:
1.  **Identify** if the target books are present in the scene.
2.  **Localize** them by computing a bounding box.
3.  **Handle** multiple instances of the same book, clutter, and occlusions.

## 🛠️ Methodology
The project implements a robust object detection pipeline using **local feature matching**. The workflow involves the following steps:

1.  **Preprocessing:** Loading dataset images and converting them to grayscale for intensity-based feature extraction.
2.  **Feature Extraction (SIFT):** We utilize the **Scale-Invariant Feature Transform (SIFT)** to detect distinctive keypoints and compute descriptors invariant to image scaling and rotation.
3.  **Feature Matching (FLANN):** Descriptors are matched using the **Fast Library for Approximate Nearest Neighbors (FLANN)**, which is more efficient than brute-force matchers for high-dimensional data.
4.  **Outlier Rejection (Lowe's Ratio Test):** False matches are filtered out by comparing the distance of the closest neighbor to the second-closest neighbor.
5.  **Geometric Verification (Homography & RANSAC):** We estimate the transformation matrix between the model and the scene using **RANSAC** to robustly handle outliers.
6.  **Multi-Instance Detection:** The algorithm iteratively detects objects, removing the keypoints of identified instances from the scene to find subsequent copies of the same book.
7.  **Post-Processing (NMS):** **Non-Maximum Suppression** is applied to merge or remove overlapping bounding boxes, ensuring each book corresponds to a unique detection.

## 💻 Technologies Used
* **Python 3**
* **OpenCV (cv2):** For all image processing, SIFT implementation, and homography estimation.
* **NumPy:** For efficient matrix operations and geometric calculations.
* **Matplotlib:** For visualizing the matching results and bounding boxes.

## 📂 Dataset Structure
The system expects the data to be organized as follows:
* `dataset/models/`: Contains reference images of the books.
* `dataset/scenes/`: Contains images of the shelves to test detection.

## 📊 Results
The pipeline outputs visual results with bounding boxes drawn around detected books. For each detection, it calculates:
* **Coordinates:** The (x, y) positions of the four corners.
* **Area:** The dimension of the book in pixels.
* **Instance Count:** The total number of times a specific book appears in the scene.

---
*This project demonstrates mastery of fundamental Computer Vision concepts including feature invariance, geometric transformations, and robust estimation techniques.*
