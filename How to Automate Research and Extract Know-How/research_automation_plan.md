# Research Automation Plan for PMS Know-How Extraction

This document outlines a comprehensive plan to automate the research and extraction of know-how from various Property Management System (PMS) companies. The goal is to gather the necessary information to define a robust set of skills for an AI-powered "Harvey for finance" in the property management sector.

## 1. Companies for Analysis

The following companies have been identified for this research, based on the provided content and the project's shared files. This list combines companies mentioned in the initial document and those for which Product Requirement Documents (PRDs) are available.

| Company Name |
| --- |
| AppFolio |
| Amenitiz |
| AvidXchange |
| BetsyAI |
| BILT Rewards |
| BoomAI |
| Buildium |
| CINC Systems |
| ClickPay |
| Cloudbeds |
| Enumerate |
| Entrata |
| Guesty |
| Hemlane |
| Hostaway |
| Hostfully |
| InnteloAIPMS |
| Landlord_Finance_OS |
| Lodgify |
| Mews |
| MRI |
| OwnerRez |
| PayLease |
| Project Citadel |
| RealPage |
| Stessa |
| Stripe |
| Vantaca |
| VisitoAIPMS |
| Yardi |
| Zego |

## 2. Automated Research and Knowledge Extraction

To efficiently gather the required know-how from each company, we will employ a parallel research process. This will be achieved using a `map` operation that spawns a separate research agent for each company.

### 2.1. Research Prompt

Each research agent will be guided by a standardized prompt, adapted from the "Universal Vendor Research Prompt" provided in the initial documentation. This ensures that the extracted information is consistent and covers all the required areas.

The prompt will instruct the agent to analyze the provided PRD documents and public online resources (help centers, documentation, forums) to extract workflows, data models, and operational patterns.

### 2.2. Output Structure

The research output for each company will be a detailed markdown file, as specified in the research prompt. These files will be organized in a structured directory:

```
knowledge/
└── vendors/
    ├── AppFolio/
    │   └── KD-AppFolio-property-finance.md
    ├── Guesty/
    │   └── KD-Guesty-property-finance.md
    └── ... (one for each company)
```

This structured approach will create a comprehensive knowledge base that can be used to define and build the required AI skills.

## 3. Next Steps

Upon approval of this plan, the automated research process will be initiated. The collected knowledge will then be synthesized to create the final "Skill Library" and associated artifacts.
