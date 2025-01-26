# Image Classification with Milvus Vector Store and Face Detection

## Overview

This project implements a retrieval-augmented generation (RAG) system for image data using face detection and embeddings. It utilizes the Google Gemini embedding model for creating embeddings of images and stores them in a Milvus vector database for efficient retrieval. The goal is to enable efficient searching and classification of images based on facial recognition.

## Table of Contents

- [Requirements](#requirements)
- [Setup](#setup)
- [Code Explanation](#code-explanation)
  - [Importing Libraries](#importing-libraries)
  - [Preprocessing Function](#preprocessing-function)
  - [Creating Image Embeddings](#creating-image-embeddings)
  - [Generating Embeddings for Multiple Images](#generating-embeddings-for-multiple-images)
  - [Setting Up Milvus Database](#setting-up-milvus-database)
  - [Inserting Data into Milvus](#inserting-data-into-milvus)
  - [Searching for Images](#searching-for-images)
- [Usage Example](#usage-example)
- [Conclusion](#conclusion)

## Requirements

This project requires the following Python packages:

- `facenet-pytorch`: For face detection and embedding generation.
- `pillow`: For image processing.
- `milvus-lite`: For the Milvus vector database.
- `pymilvus`: For interacting with the Milvus database.
- `torch`: For PyTorch functionalities.
- `torchvision`: For image transformations.

You can install these packages using the following command:

```bash
!pip install -qU facenet-pytorch pillow milvus-lite pymilvus torch torchvision
