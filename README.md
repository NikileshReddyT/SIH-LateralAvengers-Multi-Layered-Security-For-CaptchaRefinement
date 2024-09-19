# CAPTCHA Refinement Using Multi-Layered Machine Learning

## Overview

This project aims to develop a passive CAPTCHA replacement for UIDAI's portals to mitigate denial-of-service (DoS) attacks while maintaining a smooth user experience. The solution relies on a multi-layered machine learning model to differentiate between bots and humans by analyzing environmental parameters collected from the browser.

## Project Structure

The solution consists of three layers:
1. **Rule-Based System**: This layer filters out known bots based on predefined rules using parameters such as IP address validity, browser type, and version.
2. **Logistic Regression Classifier**: A second layer classifies users as either bot or human based on logistic regression, outputting a value between 0 and 1.
3. **Meta Learning with GAN (Generative Adversarial Networks)**: If the logistic regression output is ambiguous (between 0 and 1), the user is passed to this final layer, where a GAN system refines the classification for complex bot behaviors.

## Model Description

### 1. **Rule-Based System**
   The first line of defense employs a rule-based approach to immediately block or allow users based on:
   - **IP Address**: Validity and trustworthiness are checked.
   - **Browser Information**: Type and version of the browser are analyzed for suspicious activity.
   
   Users passing this layer are considered safe, while suspicious ones are blocked or sent to the next layer for further analysis.

### 2. **Logistic Regression Classifier**
   If the rule-based system is unable to make a definitive decision, a logistic regression model is used to classify the user as either:
   - **Human (1)**: Determined by the model when parameters strongly align with human behavior.
   - **Bot (0)**: Determined when the behavior matches that of known bots.
   
   Logistic regression is chosen for its efficiency and ability to classify binary outcomes. However, if the model outputs a value between 0 and 1 (ambiguous), the user is passed to the next layer for further classification.

### 3. **Meta Learning with GAN (Generative Adversarial Networks)**
   In cases where logistic regression provides uncertain results, we use a Generative Adversarial Network (GAN) to classify complex bot behavior that mimics human characteristics. The GAN system ensures:
   - Accurate differentiation between sophisticated bots and humans.
   - Enhanced ability to catch complex bots that may bypass simpler detection methods.

## Technology Stack

- **Frontend Framework**: Next.js/Flutter (used to collect environmental data such as IP address, browser type, and user interactions).
- **Backend**: The machine learning models are developed using Python (Scikit-learn for Logistic Regression, PyTorch for GAN) and integrated into the backend to provide a scalable API for UIDAI's application stack.
  
## Key Features
1. **Seamless User Experience**: No active CAPTCHA required for users, reducing friction and improving usability.
2. **Multi-Layered Security**: Rule-based filters, followed by ML-based classification, and finally meta-learning for advanced bot detection.
3. **Privacy Adherence**: The system follows UIDAI's core privacy policies, ensuring all user data is handled securely.
   
## Deployment

The backend ML models are designed to be easily integrated into existing API infrastructure. Once the model classifies the user, the decision (human or bot) is sent back to the portal to either allow or block the interaction.

---
