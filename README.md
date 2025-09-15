# 📈 FinSight AI: AI-Powered Financial Turbulence & Market Regime Monitor

![Python Version](https://img.shields.io/badge/python-3.9+-blue.svg)
![Frameworks](https://img.shields.io/badge/Frameworks-Airflow%20%7C%20Streamlit%20%7C%20scikit--learn-orange)
![License](https://img.shields.io/badge/License-MIT-green.svg)

**FinSight AI is an intelligent platform designed to analyze real-time market conditions by synthesizing structured financial data and unstructured news sentiment. The system identifies distinct market 'regimes' or 'states' to provide a clear, high-level view of current financial turbulence.**

This project moves beyond simple indicators by using unsupervised machine learning to discover hidden patterns in the market, helping users understand the prevailing risk environment at a glance.

***

## 📋 Table of Contents

1.  [The Problem](#-the-problem)
2.  [Our Solution](#-our-solution)
3.  [Key Features](#-key-features)
4.  [System Architecture & Workflow](#-system-architecture--workflow)


***

## 🎯 The Problem

In today's volatile financial markets, investors are inundated with a constant stream of disconnected data points—stock prices, economic reports, breaking news, and social media chatter. It's challenging to consolidate this information into a single, coherent understanding of the market's risk level. Traditional methods often lag and fail to capture the impact of public sentiment.

## 🤖 Our Solution

FinSight AI addresses this challenge by creating a unified view of the market. It leverages an automated data pipeline to:
1.  **Aggregate Key Data:** Ingests critical market indicators (like the S&P 500 and VIX) and real-time news from around the web.
2.  **Analyze Sentiment:** Applies Natural Language Processing (NLP) to quantify the sentiment (positive, negative, neutral) of financial news.
3.  **Identify Market Regimes:** Uses a K-Means clustering algorithm to group days with similar financial and sentiment characteristics. Each cluster represents a distinct **market regime**, such as "Low Volatility & Bullish Sentiment" or "High-Risk-Off Environment".
4.  **Visualize:** Presents the current market regime and supporting data on an intuitive, interactive web dashboard.

***

## ✨ Key Features

* **Automated ETL Pipelines:** Built with **Apache Airflow** to reliably fetch and process data from various sources without manual intervention.
* **Multi-Source Data Aggregation:**
    * **Unstructured Data:** Real-time news sentiment analysis from the News API.
    * **Structured Data:** Key market indices from Yahoo Finance (`'SP500', 'VIXCLS', 'T10Y2Y'`, etc.).
* **Unsupervised Market Regime Clustering:** Employs a **K-Means** model to classify the current market environment into predefined risk-based clusters.
* **Scalable Object Storage:** Uses **Minio** as a robust and scalable storage backend for raw data, processed features, and model artifacts.
* **Interactive Dashboard:** A clean and user-friendly interface built with **Streamlit** to visualize the current market regime, sentiment trends, and key financial indicators.

***

## 🏗️ System Architecture & Workflow

The entire process is orchestrated by Airflow, ensuring a seamless flow of data from ingestion to visualization. Data is stored centrally in Minio, decoupling storage from compute and allowing for greater scalability.

```mermaid
graph TD
    subgraph "Data Ingestion (Orchestrated by Airflow)"
        A[News API] --> B{Airflow DAG 1};
        B --> C[Minio Bucket: Raw News];

        D[Yahoo Finance API] --> E{Airflow DAG 2};
        E --> F[Minio Bucket: Market Data];
    end

    subgraph "Data Processing & Modeling"
        C --> G[Sentiment Analysis Service];
        G --> H[Minio Bucket: Sentiment Scores];

        F & H --> I{Feature Engineering};
        I --> J[Combined Dataset];
        J --> K[K-Means Clustering Model];
        K --> L[Minio Bucket: Cluster Results & Model];
    end

    subgraph "Presentation Layer"
        L --> M[Streamlit Web App];
        M --> N[👨‍💻 User];
    end

    style A fill:#FF9900,stroke:#333,stroke-width:2px
    style D fill:#7C00A1,stroke:#333,stroke-width:2px
    style M fill:#FF4B4B,stroke:#333,stroke-width:2px
    style C fill:#1A73E8,stroke:#333,stroke-width:2px
    style F fill:#1A73E8,stroke:#333,stroke-width:2px
    style H fill:#1A73E8,stroke:#333,stroke-width:2px
    style L fill:#1A73E8,stroke:#333,stroke-width:2px




