# 🎬 Market Basket Analysis Project

## 📌 Project Overview
This project implements a highly optimized, two-pass distributed data mining pipeline from scratch using **Apache Spark RDDs**. The system uncovers significant casting collaborations across global film history, scaling effortlessly over an authentic dataset of nearly 100,000 titles.

## 🛠️ Algorithmic Framework (SON Algorithm)
The pipeline utilizes a two-pass distributed MapReduce strategy to prevent cluster memory bottlenecks:
1. **Pass 1 (Local Nominees):** Segments data into independent RDD partitions and runs localized Apriori loops to extract candidate pairs using a dynamically scaled support threshold.
2. **Pass 2 (Global Counting):** Broadcasts a unified candidate list to all workers to compute exact absolute frequencies in a single parallel reduction step.

## 📊 Core Performance Metrics
| Performance Metric | Dataset 1 (Sandbox Sample) | Dataset 2 (Full Production) |
| :--- | :--- | :--- |
| **Total Transactional Baskets** | 10,100 | 98,835 |
| **Pass 1 Filtered Candidate Pairs** | 5,835 | 567,037 |
| **Global Execution Runtime** | 5.68 seconds | 9.29 seconds |

## 📜 Full Academic Report
The complete, publication-ready LaTeX compiled PDF report containing comprehensive data-cleaning details, structural organization breakdown, and cinematic analysis is included in this repository.
