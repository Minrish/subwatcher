# Technical Roadmap for SubWatcher

This document outlines the comprehensive plan for implementing SubWatcher’s core functionalities. It details the approaches and strategies for vision recognition (OCR), subscription benefit extraction, dynamic record keeping, and the overall system architecture, ensuring a cost-effective, secure, and scalable solution.

---

## 1. Overview

### 1.1 Project Goals
- **Maximize Subscription Value:** Remind users to leverage all benefits of their subscriptions before renewal.
- **Automated Benefit Detection:** Use OCR and NLP to extract and analyze subscription details from images.
- **Dynamic Updates:** Maintain an up-to-date repository of subscription plans, pricing, and benefits.

### 1.2 Scope and Platforms
- **Primary Platform:** Web application using modern technologies (e.g., React).
- **Secondary Platform:** iOS application (under active development using Swift/SwiftUI).
- **Core Components:** 
  - Image processing (OCR)
  - Natural Language Processing (NLP) for benefit extraction
  - Subscription data management and notification system

---

## 2. System Architecture

### 2.1 Component Breakdown
- **Frontend:**
  - Web interface (React)
  - Future mobile (iOS) interface
- **Backend API:**
  - RESTful endpoints for data management, OCR, and NLP services
- **OCR & Vision Module:**
  - Extract text from user-provided images
- **NLP Module:**
  - Process extracted text to identify key subscription details and benefits
- **Database:**
  - Stores user configurations and subscription data (choice between NoSQL and SQL)
- **Notification Service:**
  - Schedules and delivers alerts based on usage and upcoming renewals

### 2.2 Deployment Strategies
- **Modular Architecture:** Decouple each component for independent development and scaling.
- **Microservices Approach:** Consider deploying OCR, NLP, and data services as separate services behind an API gateway.
- **Hybrid Processing:** Leverage both on-device and server-side processing to optimize cost and performance.

---

## 3. Vision Recognition & OCR Module

### 3.1 Processing Options

#### Local (On-Device) Processing
- **Advantages:**
  - Reduced latency and dependency on network connectivity
  - No recurring server costs; minimizes risk of abuse-induced cost spikes
- **Challenges:**
  - Device performance variability may require model optimization (e.g., quantization, pruning)
- **Implementation:**
  - Use frameworks like **TensorFlow Lite** or **ONNX Runtime**
  - For web, explore **TensorFlow.js** for browser-based inference

#### Cloud-Based Processing
- **Advantages:**
  - Consistent processing power regardless of client device capability
  - Easier updates and centralized model management
- **Challenges:**
  - Potential high operational costs if not strictly rate-limited
  - Increased latency due to network dependency
- **Mitigation:**
  - Implement caching, rate limiting, and a hybrid fallback mechanism

### 3.2 Model Selection and Optimization
- **Traditional OCR:** Utilize tools such as **Tesseract OCR** for clear, formatted text.
- **Deep-Learning Models:**
  - Investigate distilled deep-learning models (e.g., a variant similar to DeepSeek 1.59B) or CRNN architectures for enhanced accuracy on noisy images.
- **Optimization Techniques:**
  - Model distillation, quantization, and pruning to balance accuracy and performance
  - Continuous benchmarking across target devices

### 3.3 Integration Strategy
- **Client-Side:**
  - Embed OCR models in the web application using in-browser ML libraries
  - Provide a fallback to server-side processing if local inference is insufficient
- **Server-Side:**
  - Create dedicated RESTful endpoints to handle image uploads and OCR processing
  - Deploy containerized services (e.g., Docker/Kubernetes) for scalability

---

## 4. Subscription Benefit Extraction and Analysis

### 4.1 Text Parsing and NLP
- **Post-OCR Processing:**
  - Normalize text and remove artifacts introduced during OCR
  - Employ Named Entity Recognition (NER) to extract dates, prices, and benefit descriptions
- **Pattern Matching:**
  - Use regular expressions and heuristic rules to detect subscription-specific details (e.g., “$20/month”, “50 priority videos”)
- **Advanced NLP Models:**
  - Fine-tune lightweight language models (e.g., a distilled BERT variant) tailored for subscription data
  - Leverage semantic search tools (e.g., Elasticsearch) for matching extracted text to known benefit templates

### 4.2 Dynamic Record Keeping
- **Database Design:**
  - Structure records to include subscription names, pricing, benefit details, and update timestamps
  - Choose between a flexible NoSQL database (e.g., MongoDB) or a relational SQL database (e.g., SQLite) based on requirements
- **Update Mechanisms:**
  - Implement web scraping or API integrations to retrieve real-time updates from subscription providers
  - Utilize change detection algorithms to trigger notifications for significant modifications (e.g., pricing changes, updated TOS)

### 4.3 Notification and Alert System
- **Matching Logic:**
  - Compare benefits extracted via OCR/NLP with subscription records using fuzzy matching techniques
- **Scheduling:**
  - Create a scheduling system to alert users ahead of subscription renewals or when significant changes are detected
  - Allow users to set custom thresholds and preferences for notification frequency

---

## 5. Cost, Security, and Scalability Considerations

### 5.1 Cost-Free Operation Strategies
- **Open-Source Tools:** 
  - Prioritize free, community-supported libraries and models (e.g., TensorFlow Lite, Tesseract)
- **On-Device Processing:**
  - Maximize client-side computation to reduce server load and associated costs
- **Resource Management:**
  - Enforce robust rate limiting, caching, and request throttling to mitigate potential abuse

### 5.2 Security Measures
- **Input Validation & Authentication:**
  - Secure API endpoints with strict validation, authentication, and authorization mechanisms
- **Rate Limiting and Monitoring:**
  - Implement server- and client-side rate limiting to prevent misuse
  - Deploy logging and monitoring tools to detect anomalies and security breaches

### 5.3 Scalability and Deployment
- **Modular Design:**
  - Separate services (frontend, OCR, NLP, database) allow for independent scaling and easier maintenance
- **Microservices Deployment:**
  - Use container orchestration (e.g., Kubernetes) to manage load distribution and scaling efficiently
- **API Gateways:**
  - Ensure efficient inter-service communication with API gateways and load balancers

---

## 6. Implementation Roadmap

### Phase 1: Prototype Development
- **Objective:** Develop a Minimal Viable Product (MVP) focusing on core OCR functionality.
- **Tasks:**
  - Implement basic OCR using an open-source tool (e.g., Tesseract or TensorFlow.js model)
  - Develop rudimentary text parsing for key subscription data extraction
  - Set up a static subscription database with sample entries

### Phase 2: Model Optimization and NLP Integration
- **Objective:** Enhance OCR performance and integrate advanced NLP for benefit extraction.
- **Tasks:**
  - Optimize OCR models (considering distillation, quantization, and pruning)
  - Integrate fine-tuned NLP models to refine subscription benefit extraction
  - Establish mechanisms (web scraping/APIs) for dynamic database updates

### Phase 3: Scalability and Security Enhancements
- **Objective:** Transition to a scalable microservices architecture with robust security.
- **Tasks:**
  - Decompose the application into modular, containerized services
  - Enhance security through authentication, logging, and rate limiting
  - Optimize caching and load balancing to handle varying traffic loads

### Phase 4: Final Testing and Deployment
- **Objective:** Prepare for production deployment across web and iOS platforms.
- **Tasks:**
  - Conduct extensive testing using real-world data and user scenarios
  - Fine-tune the balance between local and cloud processing based on device capabilities
  - Finalize deployment pipelines and monitor performance post-deployment

---

## 7. Final Overview

SubWatcher aims to deliver a cost-effective, secure, and scalable solution to help users maximize their subscription benefits. By leveraging open-source tools, on-device processing where feasible, and a modular microservices architecture, the project ensures:
- **Accurate Vision Recognition:** Through optimized OCR and deep-learning models.
- **Effective Benefit Extraction:** Via advanced NLP techniques.
- **Dynamic Subscription Management:** With real-time data updates and alert systems.
- **Cost Control & Security:** Using resource management, rate limiting, and robust security practices.