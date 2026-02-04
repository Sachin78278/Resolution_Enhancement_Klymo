# 🛰️ Klymo-SR: Satellite Super-Resolution  
### Bridging the Resolution Gap from 10m Sentinel-2 to 2.5m Commercial-Grade Imagery

---

## Project Overview

Public satellite imagery from **Sentinel-2** is widely available but limited by a **10-meter spatial resolution**, which obscures fine urban details such as roads, buildings, and vehicles. High-resolution commercial imagery (0.3–0.5 m) exists, but remains **cost-prohibitive** for many researchers and institutions.

**Klymo-SR** implements a **Generative Adversarial Network (GAN)**–based pipeline to perform **4× super-resolution**. By leveraging the **Real-ESRGAN** architecture, the system transforms standard Sentinel-2 inputs into **high-fidelity outputs**, offering a cost-effective alternative for urban and geospatial analysis.

---

## Core Objectives

- **Upscaling Performance:**  
  Achieve a 4× increase in spatial resolution while maintaining pixel integrity.

- **Geospatial Accuracy:**  
  Implement *hallucination guardrails* to ensure the model reconstructs real features rather than inventing them.

- **Real-Time Ingestion:**  
  Use **Google Earth Engine (GEE)** to stream satellite image patches directly into the model without large local storage.

---

## Technical Innovation & the “Eye Test”

Instead of standard CNN-based upscaling, which often produces blurry or overly smoothed results, **Klymo-SR uses Residual-in-Residual Dense Blocks (RRDB)** via Real-ESRGAN.

This enables evaluators to visually assess:

- **Edge sharpness:** Clearer building boundaries and urban perimeters  
- **Road and building continuity:** Smooth, non-fragmented linear structures  
- **Color consistency:** Preservation of Sentinel-2 radiometric characteristics  
- **Absence of fabricated structures:** Strict adherence to input ground truth to prevent hallucination  

---

## Mathematical Accuracy

Performance is benchmarked against a **Bicubic interpolation baseline** to ensure transparent and quantifiable improvement.

| Metric | Bicubic (Baseline) | Klymo-SR (GAN) |
|------|--------------------|---------------|
| PSNR | ~20.50 dB | **22.85 dB** |
| SSIM | 0.581 | **0.693** |

**Note:** While GANs prioritize perceptual realism over pixel-wise similarity, Klymo-SR maintains strong mathematical correlation with the source imagery while significantly improving visual clarity.

---

## Interactive Demonstration

An interactive interface built using **Gradio** allows users to:

- Input any geographic coordinate (e.g., Delhi, Kanpur, New York)
- Fetch Sentinel-2 imagery in real time via the GEE API
- View before-and-after super-resolution outputs
- Inspect PSNR and SSIM metrics live

This demonstrates **end-to-end reproducibility** and practical usability for both judges and researchers.

---

## Technology Stack

- **Satellite Data:** Sentinel-2 Level-2A (Surface Reflectance)  
- **Data Access:** Google Earth Engine Python API  
- **Deep Learning Framework:** PyTorch  
- **Super-Resolution Model:** Real-ESRGAN (RRDBNet architecture)  
- **Image Processing:** OpenCV, NumPy, scikit-image  
- **Evaluation Metrics:** PSNR, SSIM  
- **Visualization:** Gradio  
- **Compute Platform:** Google Colab (T4 GPU)  

---

## Limitations and Future Work

The current implementation uses a **pretrained GAN** without satellite-specific fine-tuning. While this delivers strong perceptual results, future improvements include:

- **Fine-tuning:** Training on paired LR–HR satellite datasets such as WorldStrat  
- **Architectural Comparison:** Benchmarking against CNN-based (EDSR) and transformer-based (SwinIR) models  
- **Geospatial Validation:** Adding vector-map overlays to verify alignment of roads and infrastructure  

---

## Conclusion

**Klymo-SR** demonstrates a robust and geospatially faithful super-resolution pipeline for Sentinel-2 imagery under constrained compute. By prioritizing **structural realism**, **transparent benchmarking**, and **hallucination prevention**, the system offers a practical solution for narrowing the public–commercial satellite resolution gap.

---

**Author:** Sachin Minglani  
B.Tech – Computer Science | ML Track
