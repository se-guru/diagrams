# Proposed Diagrams for the Paper

This document contains three proposed diagrams to visually support the key concepts in our paper. Each diagram is presented in Mermaid syntax for easy integration and editing.

---

### **Diagram 1: The Pedagogical Framework (Educator's Perspective)**

**Purpose:** This high-level flowchart provides an educator-centric view of the entire 13-week course. It illustrates the scaffolding of complexity, showing how students progress from individual tasks to full multi-squad collaboration. This diagram would fit well in **Section 3 (The Pedagogical Framework)** to give readers a map of the student journey.

```mermaid
graph TD
    subgraph "Weeks 1-2: Foundations"
        A[Individual Tutorials: Git & PERN Stack]
    end

    subgraph "Weeks 3-5: Initial Collaboration"
        B(Single-Squad Project: Enhancement Task)
        C{Key Learnings: GitFlow, Basic Teamwork}
    end

    subgraph "Weeks 6-8: Multi-Squad Design Phase"
        D[Analysis: User Stories & Data Models]
        E[Contract Definition: Collaborative OpenAPI Spec]
        F{Key Learnings: API-First Design, Negotiation}
    end

    subgraph "Weeks 9-12: Multi-Squad Implementation Phase"
        G[Automated Scaffolding from Contract]
        H[Implementation within MVC Stubs]
        I[Verification via Automated Quality Gates]
        J{Key Learnings: Architectural Adherence, TDD}
    end

    subgraph "Week 13: Reflection"
        K[Final Retrospective & Course Summary]
    end

    A --> B;
    B --> C;
    C --> D;
    D --> E;
    E --> F;
    F --> G;
    G --> H;
    H --> I;
    I --> J;
    J --> K;
```

---

### **Diagram 2: The Design-First Technical Workflow (Technical Perspective)**

**Purpose:** This diagram provides a detailed, technical view of the core design-first process for the main "Galleria" project. It explicitly shows the artifacts, activities, and tools involved, making the entire workflow tangible for the reader. This is a critical diagram and would be best placed in **Section 4 (Constraining AI)** to illustrate the system of constraints.

```mermaid
graph TD
    A[Project Requirements Document] --> B(1. Requirements Analysis);
    
    subgraph "Phase 1: Design (in Moqups)"
        B --> C{User Stories};
        B --> D{Data Models};
    end

    C --> E[2. Collaborative Contract Definition];
    D --> E;

    subgraph "Phase 2: Contract as Source of Truth"
        E --> F([openapi.yaml]);
    end

    subgraph "Phase 3: Automated Generation"
        F -- feeds --> G(Custom Handlebars Templates);
        G -- generates --> H(Application Scaffold: MVC, Stubs);
    end

    subgraph "Phase 4: Implementation & Verification"
        I(Student Code in Stubs) -- creates --> J(Pull Request);
        H -- is filled by --> I;
        
        subgraph CI/CD Pipeline (GitHub Actions)
            J --> K{Gate 1: Linters 
(ESLint, Hoover)};
            K -- on pass --> L{Gate 2: Contract Tests 
(Postman, Newman)};
            L -- on pass --> M{Gate 3: Architectural Rules 
(dependency-cruiser)};
            M -- on pass --> N[Merge to Develop];
        end

        subgraph Runtime Constraint
             O(Live Application) -- request/response --> P{Gate 4: OpenAPI Validator 
(Middleware)};
        end
    end
```

---

### **Diagram 3 (Suggested): The "Constraint Funnel" Conceptual Model**

**Purpose:** The idea that the framework "constrains AI" is the most novel part of our paper, but it can be abstract. This conceptual diagram visualizes how the layers of the framework act as a funnel, filtering raw or AI-generated code to produce high-quality, compliant output. It makes the core argument of **Section 4** immediately understandable.

```mermaid
graph TD
    A(Input: Student-written or <br> AI-generated code);

    A --> B{Constraint 1: <br> Does it fit the MVC Scaffold?};
    B -- Yes --> C{Constraint 2: <br> Does it pass Static Analysis & Linters?};
    B -- No --> Z(Rejected: <br> Architectural Violation);
    
    C -- Yes --> D{Constraint 3: <br> Does it pass Automated Contract Tests?};
    C -- No --> Z;

    D -- Yes --> E{Constraint 4: <br> Does it pass Runtime Validation?};
    D -- No --> Z;

    E -- Yes --> F([Output: High-Quality, <br> Contract-Compliant Code]);
    E -- No --> Z;

    style Z fill:#f9f,stroke:#333,stroke-width:2px;
    style F fill:#9f9,stroke:#333,stroke-width:2px;
```
