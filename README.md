# TripNest — The Traveller Insights Challenge

## 📌 Project Overview

TripNest is a digital travel platform that helps travellers discover and book accommodations, activities, and experiences.

The platform receives information from travellers, property partners, experience providers, and customer support. Different teams use this data to understand traveller preferences, manage partner information, and analyze bookings and customer behaviour.

However, differences in data formats, duplicate traveller records, inconsistent business definitions, and changing booking information make it difficult to maintain reliable and consistent data.

This project proposes a **data curation architecture** to organize, standardize, validate, and connect information from multiple sources into trusted datasets for analytical and business use.

## 🎯 Project Objectives

* Integrate information from multiple source systems.
* Identify duplicate traveller records using entity resolution.
* Standardize data formats and apply transformation rules.
* Establish consistent business metric definitions through a semantic layer.
* Handle booking updates and maintain data freshness.
* Organize curated data for different teams.
* Maintain data lineage to trace information back to its sources.
* Support error investigation, correction, and reprocessing.

## 🏗️ Proposed Architecture

The proposed architecture follows a logical data flow from source systems to downstream reporting and decision-making.

### Architecture Flow

```text
Source Systems
      |
      v
Data Ingestion
(Batch / Incremental / Streaming)
      |
      v
Raw Data Layer
      |
      v
Schema Checks and Data Quality
      |
      v
Standardization and Transformation
      |
      v
Entity Resolution
      |
      v
Curated Data and Quality Checks
      |
      v
Central Data Warehouse
      |
      v
Semantic Layer and Team-Specific Views
      |
      v
Reports and Business Decisions
```

**Cross-cutting capabilities:** Data lineage, metadata, monitoring, testing, quarantine, error recovery, and access control.

### Architecture Components

| Component                          | Purpose                                                                                     |
| ---------------------------------- | ------------------------------------------------------------------------------------------- |
| Source Systems                     | Provide traveller, property partner, experience provider, and customer support information. |
| Data Ingestion                     | Collect data using suitable ingestion methods.                                              |
| Raw Data Layer                     | Preserve incoming data with minimal modification for auditing and reprocessing.             |
| Schema Checks and Data Quality     | Validate data structures, required fields, data types, and values.                          |
| Standardization and Transformation | Normalize formats, apply business rules, and process data updates.                          |
| Entity Resolution                  | Identify records that refer to the same traveller while preserving source references.       |
| Curated Data                       | Store clean, standardized, validated, and connected datasets.                               |
| Central Data Warehouse             | Organize structured, related data for reporting and analysis.                               |
| Semantic Layer                     | Define shared business meanings, metrics, and calculation rules.                            |
| Team-Specific Views                | Provide relevant datasets to authorized teams.                                              |
| Data Lineage                       | Track data origins and transformations throughout the pipeline.                             |
| Error Recovery                     | Support correction, reprocessing, validation, and downstream updates.                       |

## 🔍 Problems and Proposed Solutions

### 1. Duplicate Traveller Records

**Problem:** The same traveller may appear under different names or contact details across multiple sources.

**Solution: Entity Resolution**

* Compare names, email addresses, phone numbers, and other reliable identifiers.
* Match records using appropriate evidence.
* Preserve original source identifiers and relevant history.
* Review uncertain matches rather than merging them automatically.

### 2. Inconsistent Business Definitions

**Problem:** Teams may define a completed booking differently. One team may count successful payments, while another counts bookings where the service was actually used.

**Solution: Semantic Layer and Business Metric Definitions**

* Establish clear definitions for business metrics.
* Distinguish paid bookings from used bookings.
* Apply agreed calculation rules consistently across reports and dashboards.

### 3. Changing Booking Information

**Problem:** A booking may initially be confirmed and later cancelled, leaving reports with outdated information.

**Solution: Change Processing and Data Freshness Management**

* Capture new and changed booking information.
* Apply transformation rules to process status updates.
* Update affected curated datasets and warehouse records.
* Refresh reports according to the required freshness level.

Streaming or incremental ingestion can be used when appropriate for the source and freshness requirements.

### 4. Data from Multiple Sources

**Problem:** Different source systems may use different formats, field names, data types, and value representations.

**Solution: Data Integration and Standardization**

* Bring information into a central data platform.
* Standardize field names, formats, data types, and values.
* Maintain appropriate source identifiers.
* Connect related datasets using suitable keys and relationships.

### 5. Different Team Requirements

**Problem:** The Travel, Partner, and Business teams require different information.

**Solution: Team-Specific Data Organization**

* Create relevant views or datasets for each team.
* Reuse shared curated data and business definitions.
* Apply role-based access control (RBAC).
* Avoid unnecessary duplication of underlying datasets.

### 6. Lack of Data Traceability

**Problem:** TripNest needs to understand where reported information originated and how it was transformed.

**Solution: Data Lineage**

* Track data from source systems through processing and storage to reports.
* Record relevant transformation and processing information.
* Trace incorrect report values to their potential origins.
* Correct the root cause, reprocess affected data, and validate the results.

## 📊 Data Consumers

### Travel Team

Uses traveller profiles, preferences, and behaviour information to understand traveller needs and trends.

### Partner Team

Uses property and experience information to analyze partner performance and relevant operational details.

### Business Team

Uses booking metrics, customer behaviour, and revenue information for business analysis and decision-making.

## 🧠 Key Design Decisions

### Ingestion Strategy

Different ingestion methods can be selected based on source capabilities and freshness requirements:

* **Batch:** Processes data periodically.
* **Incremental:** Captures newly added or modified records.
* **Streaming:** Processes incoming events continuously or as they arrive.

Not every source requires all three methods.

### Data Modeling

The curated layer can use an entity-based relational model to organize travellers, bookings, properties, and experiences.

The central data warehouse can use a dimensional model, such as a star schema, when suitable for reporting and analytical requirements.

These are proposed modeling choices; the exact schema depends on the implementation requirements.

### Semantic Layer

The semantic layer provides shared business definitions and consistent metric calculations. Business rules can be defined during design and implemented in transformations or exposed through a reporting-facing semantic model.

### Data Lineage and Recovery

Lineage supports investigation of data issues, while monitoring, validation, and reprocessing help restore correct results.

## ✅ Expected Outcomes

The proposed architecture aims to provide:

* More reliable and consistent traveller records.
* Standardized information across source systems.
* Consistent business metric definitions.
* Timely processing of booking updates.
* Organized datasets for different teams.
* Improved data traceability and error investigation.
* More trustworthy reporting and decision-making.

## 📁 Project Deliverables

This repository contains the proposed solution for the TripNest Data Curation Challenge.

Planned deliverables:

* `README.md` — Project overview, architecture, and design decisions.
* `TripNest.pdf` — Detailed case study analysis, problems, and proposed solutions.
* `diagrams/TripNest-Data-Curation-Architecture.png` — Proposed data curation architecture.

## ⚠️ Project Scope

This repository presents a proposed data curation design for the TripNest case study. The architecture and solutions describe recommended approaches; they should not be interpreted as proof that a production pipeline has been implemented.

Specific tools, schemas, and implementation details can be selected based on further technical requirements.


