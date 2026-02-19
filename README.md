# 🛠 Data Preprocessing & Embedding Strategy
> **Role:** Data Scientist (Data Collection, Cleaning & Structural Embedding)
> **Project:** RAG-based Global Airline Baggage Verification System

수하물 규정의 복잡한 계층 구조와 수치 데이터를 LLM이 정확하게 인지할 수 있도록 설계한 **데이터 전처리 및 임베딩 전략**을 다룬다. 

##🎯 0. 전체 구조 (map)
1. ICAO,IATA에서 전세계 공통적으로 규정하고 있는 STANDARD 규정
2. 각 국가별 특색 (10개국) 에 맞춘 추가 규정
3. 국가별 FSC, LCC의 규정 

을 살펴봄으로써, 지속적으로 파일확장에 대한 가능성을 제시한다. 
  

---

## 🎯 1. 전처리 핵심 원칙 (Core Principles)



1. **Lossless Table Parsing:** 표(Table) 데이터의 행/열 관계가 깨지지 않도록 Markdown 포맷으로 변환
2. **Contextual Metadata Tagging:** 각 규정 조항에 항공사, 국가, 수하물 유형(기내/위탁) 등의 메타데이터를 강결.
3. **Hierarchical Layering:** 전 세계 공통 규정(IATA)과 개별 항공사 규정을 분리하여 지식 충돌을 방지한다. 

---

## 🏗 2. 데이터 파이프라인 (Data Pipeline)



```mermaid
graph TD
    A[Raw Data: Web/PDF] --> B{Cleaning}
    B -->|Noise Removal| C[Markdown Structuralization]
    C -->|Metadata Tagging| D[Semantic Chunking]
    D --> E[Vector Embedding]
    E --> F[(Vector Database)]


## 📂3. Global Fundamental Aviation Rules

## 3-1 . Safety & Security (IATA DGR)
- **Lithium Batteries:** - < 100Wh: Carry-on Only (Up to 20pcs)
  - 100Wh ~ 160Wh: Approval Required
  - > 160Wh: Forbidden
- **Liquids (LAGs):** 100ml per container, 1L total in a clear bag.

## 3-2. Liability & Compensation (Montreal Convention)
- **Liability Limit:** Max 1,288 SDR per passenger for destruction, loss, damage, or delay.
- **Claim Deadlines:**
  - Damage: Within 7 days
  - Delay/Loss: Within 21 days

## 3-3. Regional Overrides (US/Canada)
- **US DOT 399.87:** For itineraries to/from the US, the baggage rules of the **First Marketing Carrier** apply to the entire journey.
- **Conflict Note:** This rule overrides IATA Resolution 302.
