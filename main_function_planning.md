# SubWatcher Web-Based Application: Main Functionality Technical Design

This document provides a detailed technical overview of the main functionality for the web-based SubWatcher application. The goal is to enable users to upload subscription-related images, extract relevant information via OCR and NLP techniques, and schedule notifications to remind them to utilize their subscription benefits.

---

## 1. Introduction

SubWatcher is designed to help users maximize the value of their subscription services. The application achieves this by:
- Allowing users to upload images (e.g., screenshots of subscription receipts).
- Processing these images to extract text using Optical Character Recognition (OCR).
- Analyzing the extracted text with Natural Language Processing (NLP) to identify key subscription details.
- Storing the data and scheduling timely notifications for users.

---

## 2. Functional Overview

### 2.1 User Workflow
- **Image Upload:** Users select and upload an image containing subscription information.
- **Image Preprocessing:** The system validates and preprocesses the image (e.g., resizing, grayscale conversion) to enhance OCR performance.
- **OCR Processing:** The preprocessed image is processed to extract textual content.
- **Text Parsing & NLP Analysis:** Extracted text is analyzed to identify subscription names, pricing, renewal dates, and benefits.
- **Data Storage & Record Keeping:** The parsed data is stored in a database, including details such as subscription changes over time.
- **Notification Scheduling:** Based on the stored information, the system schedules notifications to alert users before subscription renewals or when benefits are underutilized.

### 2.2 Key Functional Components
- **Image Upload Module:** Manages file selection, initial validation, and client-side image preprocessing.
- **OCR Processing Service:** Converts preprocessed images into raw text, using either in-browser or server-side solutions.
- **NLP & Parsing Engine:** Processes the raw OCR text to extract structured subscription details.
- **Data Management Layer:** Persists subscription data, user preferences, and alert histories.
- **Notification Scheduler:** Monitors subscription data and triggers notifications based on predefined criteria.

---

## 3. System Architecture

### 3.1 High-Level Architecture Overview
The system is structured into multiple modular components that communicate via well-defined APIs. The primary components include:

- **Frontend Client (Web Application):**
  - Built with modern web technologies (e.g., React).
  - Provides an interface for image upload and displays processing results and notifications.
  - Performs preliminary image validation and preprocessing.

- **Backend API Gateway:**
  - Acts as the central hub for all client requests.
  - Routes image processing, OCR, NLP, and data storage requests to the appropriate services.
  - Implements security measures such as authentication and rate limiting.

- **OCR Processing Service:**
  - Extracts text from images.
  - Offers flexibility between client-side (e.g., browser-based inference) and server-side processing.
  - Incorporates image enhancement techniques (e.g., noise reduction) to improve accuracy.

- **NLP & Parsing Engine:**
  - Normalizes and cleans the extracted text.
  - Uses pattern matching, regular expressions, and entity recognition to parse subscription details.
  - Optionally leverages lightweight language models to refine the extraction process.

- **Data Storage:**
  - Maintains a repository of subscription records, user profiles, and alert logs.
  - Supports dynamic updates to reflect changes in subscription offerings and pricing.
  - Can be implemented using either a relational or NoSQL database, based on scalability needs.

- **Notification Scheduler:**
  - Monitors the database for upcoming renewal dates or low benefit usage.
  - Schedules and dispatches notifications via email, in-app alerts, or push notifications.
  - Allows user customization for notification frequency and thresholds.

### 3.2 Component Interaction Flow
1. **User uploads an image** via the web interface.
2. **Frontend validates and preprocesses** the image, then sends it to the backend API.
3. **API Gateway routes the image** to the OCR Processing Service.
4. **OCR Service extracts text** from the image and returns raw text to the API.
5. **The NLP & Parsing Engine** processes the raw text to extract structured subscription details.
6. **Structured data is stored** in the Data Management Layer.
7. **The Notification Scheduler** reviews stored data and schedules alerts based on upcoming renewals or benefit usage.

---

## 4. Detailed Workflow

### 4.1 Image Upload and Preprocessing
- **User Interaction:**  
  Users select and upload an image file through a web-based interface.
  
- **Client-Side Validation:**  
  The system checks file type and size to ensure compatibility.

- **Image Enhancement:**  
  Preprocessing steps (e.g., converting to grayscale, adjusting brightness/contrast, and noise reduction) are applied to optimize the image for OCR.

### 4.2 OCR Processing
- **Processing Options:**  
  - **Client-Side Processing:** Utilizing in-browser machine learning frameworks to perform OCR directly on the user’s device.
  - **Server-Side Processing:** Sending the preprocessed image to a backend service equipped with an OCR engine (such as Tesseract) for text extraction.

- **Output:**  
  The OCR process produces a block of raw text containing various subscription details.

### 4.3 Text Parsing and NLP Analysis
- **Text Normalization:**  
  Clean and standardize the extracted text to remove artifacts and format inconsistencies.

- **Data Extraction:**  
  Use pattern matching and entity recognition to extract key information, including:
  - **Subscription Name:** Identifying the service provider.
  - **Pricing Information:** Detecting cost details (e.g., "$20/month").
  - **Renewal Date:** Extracting dates indicating when the subscription renews.
  - **Benefits:** Parsing any additional details such as the number of credits, videos, or other benefits.

- **Accuracy Considerations:**  
  Implement mechanisms to handle ambiguous or low-confidence extractions, potentially flagging them for manual review or further processing.

### 4.4 Data Storage and Record Keeping
- **Database Design:**  
  Create a structured schema to capture subscription data, including:
  - User identifiers and subscription metadata.
  - Detailed records of subscription features and historical changes.
  - Timestamps for record updates and notifications.

- **Data Integrity:**  
  Ensure that the system supports dynamic updates, reflecting any changes in subscription offerings or pricing.

### 4.5 Notification Scheduling
- **Monitoring and Analysis:**  
  A background service periodically scans the stored subscription records to identify upcoming renewals or underutilized benefits.

- **Alert Criteria:**  
  Configure thresholds and rules (e.g., notifying users one week before renewal or when certain benefits remain unused).

- **User Notifications:**  
  Alerts are delivered via configured channels (email, in-app messages, or push notifications), allowing users to take timely action.

---

## 5. Technical Considerations

### 5.1 Performance and Scalability
- **Client vs. Server Processing:**  
  Balance between client-side and server-side processing to optimize performance and minimize costs.
  
- **Load Distribution:**  
  Utilize API gateways and load balancers to ensure efficient handling of concurrent requests.
  
- **Caching and Rate Limiting:**  
  Implement caching strategies and enforce rate limiting to manage resource usage and prevent system overload.

### 5.2 Security and Data Privacy
- **Input Validation:**  
  Rigorously validate all image and text inputs to mitigate potential security risks.
  
- **Authentication and Authorization:**  
  Secure API endpoints to restrict access and protect user data.
  
- **Data Encryption:**  
  Encrypt sensitive data both in transit and at rest, ensuring compliance with privacy standards.

### 5.3 Cost Management
- **Leveraging Open-Source Tools:**  
  Use free and open-source OCR and NLP solutions to reduce operational costs.
  
- **Optimized Resource Usage:**  
  Maximize on-device processing to decrease server load and associated expenses.
  
- **Scalable Infrastructure:**  
  Design the system to scale dynamically with user demand, using containerization and orchestration as needed.

---

## 6. Summary

This technical design document outlines the core functionality of the SubWatcher web-based application. It details the end-to-end process—from image upload and preprocessing, through OCR and NLP-based text extraction, to data storage and notification scheduling. By utilizing a modular architecture and balancing client-side and server-side processing, the system aims to provide a robust, cost-effective, and scalable solution for helping users maximize the benefits of their subscriptions.

*This document serves as a technical blueprint for the development team. It may be adjusted based on further testing, evolving project requirements, and technology considerations.*
