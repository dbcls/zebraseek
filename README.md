# zebraseek

## フロー図（Mermaid記法）

```mermaid
flowchart TD
    START["begginig of flow"]
    Q["Query<br>Set of HPO"] --> KS["Knowledge Searcher"]
    KS --> WS["web research"]
    KS --> DBS["DB research"]
    WS --> S["Summmarize<br><span style='font-size:10px'>Prompt10,11</span>"]
    DBS --> S
    Q --> CS["Case Searcher<br>Case DB"]
    Q --> PA["Phenotype Analyzer"]
    PA --> ZD["Zero-shot Diagnosis<br><span style='font-size:10px'>Prompt4</span>"]
    PA --> PC["PubcaseFinder"]
    PC --> CD
    CT --> CS
    ZD --> CD["Candidate Disease"]
    CS --> RR["reranking"]
    RR --> R["Result"]
    S --> PD["Pre Diagnosis<br><span style='font-size:10px'>Prompt12</span>"]
    R --> PD
    CD --> PD
    PD --> DN["Disease Normalizer"]
    DN --> KSR["Knowledge Searcher"]
    KSR --> J["Judge<br><span style='font-size:10px'>Prompt6</span>"]
    PD --> J
    CT -->|" "| KS
    J --> FD["Final Diagnosis"]
    J -. "Depth+1 (if Predicted disease = ∅ )" ..->  START

    CT["Clinical Text"]
    FI["Facial Image"]
    START --> CT
    START --> FI
    START -->  Q
    Q -. "PhenopacketStore data" .-> CT
    FI --> GM["GestaltMatcher"]
    GM --> PD
    KS -- " " --> WS
    KS -- " " --> DBS
    WS -- " " --> S
    DBS -- " " --> S
    CS -- " " --> RR
    RR -- " " --> R
    S -- " " --> PD
    R -- " " --> PD
    %% style for blue arrow
    linkStyle 10,21,24,27,30,31,32,33,34,35,36,37 stroke:#0074D9,stroke-width:2px;
    %% style for red arrow
    
    linkStyle 25,29,28 stroke:#FF4136,stroke-width:2px;
    %% 矢印の色や深さの表現はMermaidでは省略
    %% 青色のループや赤色はコメントで補足
    
```


# Research Question

1. Which is more effective for identifying similar patient cases and relevant medical information: free-form clinical narratives or standardized HPO annotations?

2. Are facial photographs effective for diagnosing rare diseases?


# Rare Disease Diagnosis Agent(Now developping)

## Purpose
This project implements an AI agent for assisting in the diagnosis of rare diseases.

---

## Features (Implemented)
- **PCF Integration:** Calls the PubCaseFinder (PCF) API for case-based retrieval.
- **Zero-Shot Diagnosis:** Utilizes zero-shot learning for disease suggestion.
- **Tentative Diagnosis:** Generates a preliminary diagnosis based on input data.
- **Reflection Step:** Performs a reflection process to refine diagnostic suggestions.
- **Final Diagnosis:** Outputs a final diagnosis after all reasoning steps.

---

## Features (Not Yet Implemented)
- **MCP Server Integration:** Support for MCP server communication.
- **External Knowledge Search Logic:** Mechanism for searching and integrating external knowledge sources.
- **Memory:** Persistent memory for accumulating and utilizing information across sessions.
- **Information Definition & Prompt Integration:** Clear definition of information types and mechanisms for embedding them into prompts.

---

## Notes
- Further development is needed for memory management and external knowledge integration.
- Contributions and suggestions are welcome!