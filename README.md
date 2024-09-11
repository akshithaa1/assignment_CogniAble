# assignment_CogniAble

# Therapist and Child Detection and Tracking

## Introduction

This project aims to address a specific challenge in the context of Autism Spectrum Disorder (ASD) therapy sessions: tracking the interactions between therapists and children over the duration of a video. Using object detection and tracking algorithms, the goal is to automatically detect, assign unique IDs, and track individuals (therapists and children) in the video. This tracking system helps monitor their behaviors, emotions, and engagement levels, allowing for the generation of valuable insights to guide therapy sessions and treatment plans.

This system is based on state-of-the-art object detection and tracking models—YOLOv8 and DeepSORT, respectively. It leverages the power of YOLOv8 to detect the presence of persons in video frames and DeepSORT to maintain consistent tracking of individuals throughout the video, even if they temporarily leave or re-enter the frame.

## Problem Statement

The problem entails building a real-time person detection and tracking system with the following specific requirements:

1. **Assign Unique IDs**: Detect therapists and children in the video and assign them unique IDs for tracking throughout the video.
2. **Track Re-entries**: Ensure that if a person leaves and re-enters the frame, they are assigned the same ID.
3. **Assign New IDs**: Detect new individuals entering the frame and assign them new unique IDs.
4. **Post-Occlusion Tracking**: Handle scenarios where a person is partially or completely occluded from the frame and reappears, ensuring they retain the same ID.
5. **Person Differentiation**: Differentiate between therapists and children based on the size of their bounding boxes, using heuristic rules.
6. **Multiple Person Tracking**: Track multiple persons (therapists and children) simultaneously, maintaining accurate IDs for all individuals across the video.

## Solution Approach

We adopted a two-stage approach for this project:

1. **Object Detection with YOLOv8**: YOLO (You Only Look Once) is a fast and efficient object detection algorithm. In this project, we use YOLOv8, the latest and most advanced version, which offers improved accuracy and speed. YOLOv8 is pre-trained on the COCO dataset, which includes the "person" class (class ID `0`).

2. **Person Tracking with DeepSORT**: DeepSORT (Simple Online and Realtime Tracking with a Deep Association Metric) is a highly accurate multi-object tracking algorithm. It assigns unique IDs to detected objects and maintains these IDs across frames. DeepSORT uses Kalman Filters and a deep learning-based appearance descriptor to ensure re-identification of objects (i.e., maintaining the same ID even if the object temporarily disappears from the frame).

### Differentiation Heuristic

Since we are only interested in tracking therapists and children, we differentiate between the two by using the size of their bounding boxes. The assumption is that therapists will have a larger bounding box than children due to their physical size. A bounding box area threshold is used to determine whether the detected "person" is a therapist or a child.

- **Therapists**: Larger bounding boxes (area > 10% of the frame).
- **Children**: Smaller bounding boxes (area < 10% of the frame).

## Installation

### Prerequisites

Ensure that you have Python 3.8 or higher installed on your machine.

### Steps to Set Up the Environment

1. **Clone the Repository** (or download the source code files):

   ```bash
   git clone <your-repository-url>
   cd <repository-directory>
