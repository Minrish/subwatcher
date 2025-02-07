# SubWatcher: Subscription Benefits Reminder 🚀

_SubWatcher_ is an AI-powered application designed to help you maximize the value of **all** your subscription services. Whether you subscribe to streaming platforms, productivity tools, cloud storage, or even specialized services like ChatGPT (Plus, Pro, etc.), SubWatcher monitors your subscription details and sends you timely reminders to use your benefits before your next billing cycle begins.

> **Note:** We are launching the **web-based version** first. The **iOS version** is under active development and will be available soon!

---

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
  - [Web Installation](#web-installation)
  - [iOS Installation (Coming Soon)](#ios-installation-coming-soon)
- [Configuration](#configuration)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Overview 📢

SubWatcher was created to address a common challenge: many users pay for subscriptions that include valuable features or benefits, yet they rarely take full advantage of them. Whether it's a streaming service, a cloud storage plan, or even niche subscriptions like ChatGPT's Sora video generation feature, SubWatcher keeps track of your usage and sends you a reminder at the end of your subscription period. This ensures you can enjoy every benefit before your subscription renews for the next month.

For example: Many ChatGPT subscribers pay $20/month for a service packed with features—such as Sora’s AI video generation—yet they rarely tap into its full potential.  
- **ChatGPT Plus:** Offers credits to create up to 50 priority 5-second videos at 720p  
- **ChatGPT Pro:** Provides up to 500 priority 20-second videos at 1080p (with unlimited "slow" generations)  

---

## Features ✨

- **Universal Subscription Monitoring:**  
  Works with **any subscription service**—from entertainment and productivity apps to specialized digital services—by letting you input or capture your subscription details.
- **Identifier:**  
  For the web platform, simply select a screenshot (from your local drive or cloud services like Google Drive/Dropbox) that shows your subscription purchase or renewal information. Our AI-powered **Identifier** extracts the relevant text (such as renewal dates and available benefits) automatically.
- **AI-Driven Notifications:**  
  Uses intelligent analytics to detect underutilization and sends you a reminder just before your subscription renews.
- **Customizable Alerts:**  
  Set your preferred notification thresholds and frequency to suit your usage habits.
- **Usage Analytics Dashboard:**  
  View historical usage data, track your benefit consumption, and receive personalized suggestions to optimize your subscriptions.

---

## Architecture 🔧

The project is built with a modular architecture to support multiple platforms:

- **Frontend:**  
  - **Web Platform:** Developed with modern web technologies (e.g., React) to ensure a responsive, intuitive user experience.  
  - **iOS:** *(Coming Soon)* Will be developed using Swift and SwiftUI for a native mobile experience.
- **Backend:**  
  - A RESTful API (using Python or Node.js) that manages user data, subscription details, and AI analytics.
- **AI Module:**  
  - Implements machine learning (e.g., TensorFlow or PyTorch) to analyze usage patterns and extract text from screenshots (the **Identifier**).
- **Database:**  
  - A lightweight relational (e.g., SQLite) or NoSQL database to store user configurations and usage statistics.

---

## Prerequisites 💻

### General
- Git (to clone the repository)
- A stable internet connection

### For Web Platform
- Node.js v14+ (for the frontend)
- Python 3.8+ (for the backend)

### For iOS (Coming Soon)
- Xcode 12 or later
- Swift 5+
- CocoaPods (for dependency management)

---

## Installation

### Web Installation 🌐

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/Minrish/subwatcher.git
   cd subwatcher
