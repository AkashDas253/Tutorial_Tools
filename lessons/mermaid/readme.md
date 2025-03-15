## Mermaid

### **1. Basics**  

#### **What is Mermaid?**  
Mermaid is a JavaScript-based diagramming tool that allows creating various types of charts using text-based syntax.  

#### **Syntax Overview**  
- Every diagram starts with `%%{init}` (optional) for configuration.  
- The first line specifies the diagram type.  
- Nodes and relationships are defined with simple text-based syntax.  

**Example:**  
```mermaid
graph TD;  
    A[Start] --> B{Decision};  
    B -->|Yes| C[End];  
    B -->|No| D[Continue];  
```

---

### **2. Flowcharts**  

#### **Nodes and Links**  
- Nodes represent elements in the flowchart.  
- Links connect nodes using arrows (`-->`, `--x`, `-.->`).  

**Example:**  
```mermaid
graph TD;  
    A[Start] --> B{Decision};  
    B -->|Yes| C[Success];  
    B -->|No| D[Failure];  
```

#### **Direction & Layout**  
- `TD` → Top to Bottom  
- `LR` → Left to Right  
- `BT` → Bottom to Top  
- `RL` → Right to Left  

**Example:**  
```mermaid
graph LR;  
    A --> B;  
    B --> C;  
```

#### **Styling Nodes and Edges**  
- Nodes can have styles (`fill`, `stroke`, `font-size`).  
- Edges can have text and styles.  

**Example:**  
```mermaid
graph TD;  
    A[Start] -->|Proceed| B{Decision};  
    B -->|Yes| C[Approved];  
    B -->|No| D[Rejected];  
    style A fill:#ffcc00,stroke:#333,stroke-width:2px;  
    style C fill:#00ff00,stroke:#000;  
```

#### **Subgraphs**  
- Group nodes into clusters using `subgraph`.  

**Example:**  
```mermaid
graph TD;  
    subgraph Group 1  
        A --> B;  
        B --> C;  
    end  
    C --> D;  
```

---

### **3. Sequence Diagrams**  

#### **Participants**  
- Define entities in a sequence diagram using `participant`.  

**Example:**  
```mermaid
sequenceDiagram  
    participant A as User  
    participant B as Server  
    A->>B: Request Data  
    B-->>A: Response  
```

#### **Messages**  
- `->>` → Solid arrow (synchronous)  
- `-->>` → Dashed arrow (asynchronous)  
- `->>` with `+` → Activation  

**Example:**  
```mermaid
sequenceDiagram  
    A->>+B: Process Start  
    B-->>-A: Acknowledgment  
```

#### **Activation & Deactivation**  
- `+` → Activate a participant  
- `-` → Deactivate a participant  

**Example:**  
```mermaid
sequenceDiagram  
    participant A  
    participant B  
    A->>+B: Start  
    B-->>-A: Done  
```

#### **Loops, Alternatives, and Conditions**  
- `loop` → Repeats actions  
- `alt` → Alternatives (if-else)  
- `opt` → Optional block  

**Example:**  
```mermaid
sequenceDiagram  
    participant User  
    participant System  
    User->>System: Login Attempt  
    alt Successful  
        System-->>User: Welcome  
    else Failed  
        System-->>User: Retry  
    end  
```

---

### **4. Gantt Charts**  

#### **Tasks and Dependencies**  
- Gantt charts define project tasks with dependencies and timelines.  
- Format:  
  - `title` → Sets the chart title.  
  - `dateFormat` → Defines the date format.  
  - `section` → Groups tasks.  

**Example:**  
```mermaid
gantt  
    title Project Timeline  
    dateFormat YYYY-MM-DD  
    section Planning  
    Task A :a1, 2025-03-01, 5d  
    Task B :after a1, 3d  
    section Development  
    Task C :a2, 2025-03-10, 7d  
    Task D :after a2, 4d  
```

#### **Styling and Customization**  
- `color` → Change task colors.  
- `done` → Mark task completion.  

**Example:**  
```mermaid
gantt  
    title Development Schedule  
    dateFormat YYYY-MM-DD  
    section Phase 1  
    Task 1 :done, 2025-03-01, 4d  
    Task 2 :active, 2025-03-05, 6d  
```

---

### **5. Pie Charts**  

#### **Defining Pie Charts**  
- Format:  
  - `pie` → Defines a pie chart.  
  - Data values are written as `label: value`.  

**Example:**  
```mermaid
pie  
    title Market Share  
    "Company A" : 40  
    "Company B" : 25  
    "Company C" : 35  
```

#### **Customization**  
- Titles can be added using `title`.  
- Values should be numerical, representing proportions.  

---

### **6. Class Diagrams**  

#### **Defining Classes and Relationships**  
- Classes are defined using `classDiagram`.  
- Syntax:  
  - `ClassName` → Defines a class.  
  - `+` (public), `-` (private), `#` (protected).  
  - `ClassA --|> ClassB` → Inheritance.  
  - `ClassA -- ClassB` → Association.  
  - `ClassA o-- ClassB` → Composition.  
  - `ClassA *-- ClassB` → Aggregation.  

**Example:**  
```mermaid
classDiagram  
    class Animal {  
        +String name  
        +eat()  
    }  
    class Dog {  
        +bark()  
    }  
    Animal <|-- Dog  
```

#### **Inheritance and Composition**  
- `--|>` → Inheritance  
- `*--` → Composition  
- `o--` → Aggregation  

**Example:**  
```mermaid
classDiagram  
    class Car {  
        +engine: Engine  
    }  
    class Engine {  
        +start()  
    }  
    Car *-- Engine  
```


---

### **7. Entity Relationship Diagrams (ERD)**  

#### **Entities and Relationships**  
- `erDiagram` → Defines an ER diagram.  
- Entities are written as `ENTITY_NAME {}`.  
- Relationships:  
  - `||--||` → One-to-One  
  - `||--o{` → One-to-Many  
  - `}o--o{` → Many-to-Many  

**Example:**  
```mermaid
erDiagram  
    CUSTOMER ||--o{ ORDER : places  
    ORDER ||--|{ ITEM : contains  
    CUSTOMER {  
        string name  
        int id  
    }  
    ORDER {  
        int id  
        date orderDate  
    }  
    ITEM {  
        int id  
        string name  
        float price  
    }  
```

---

### **8. State Diagrams**  

#### **States and Transitions**  
- `stateDiagram` → Defines a state diagram.  
- States are written as `StateName`.  
- Transitions use `-->`.  

**Example:**  
```mermaid
stateDiagram  
    [*] --> Idle  
    Idle --> Running : Start  
    Running --> Stopped : Stop  
    Stopped --> Idle : Reset  
```

#### **Styling and Customization**  
- Use `[ ]` for the start and end states.  
- Arrows represent transitions.  
- Labels describe transitions.  

**Example:**  
```mermaid
stateDiagram  
    [*] --> Locked  
    Locked --> Unlocked : Enter Code  
    Unlocked --> Locked : Close  
    Unlocked --> [*] : Exit  
```

---

### **9. User Journey Diagrams**  

#### **Defining Steps**  
- `journey` → Defines a user journey diagram.  
- `section` → Groups steps.  
- Format:  
  - `User: Task, State`  

**Example:**  
```mermaid
journey  
    title User Signup Journey  
    section Signup  
      User: Visit Website, 5  
      User: Create Account, 4  
    section Onboarding  
      User: Verify Email, 3  
      User: Complete Profile, 4  
```

#### **Customization**  
- Numbers represent user experience ratings (1-5).  
- Sections categorize different phases.  

---

### **10. Mind Maps**  

#### **Structure and Formatting**  
- `mindmap` → Defines a mind map.  
- Indentation represents hierarchy.  
- Nodes are written as `Root --> Child`.  

**Example:**  
```mermaid
mindmap  
    root((Main Topic))  
        subtopic1(Subtopic 1)  
            subsub1(Detail 1)  
            subsub2(Detail 2)  
        subtopic2(Subtopic 2)  
```

#### **Styling and Customization**  
- Use `(( ))` for rounded nodes.  
- Nodes can have multiple branches.  

**Example:**  
```mermaid
mindmap  
    root((Learning Path))  
        Frontend  
            HTML  
            CSS  
            JavaScript  
        Backend  
            Node.js  
            Python  
```

---



---
---


## Mermaid Syntax

Mermaid provides a simple, text-based way to generate diagrams. Below is a detailed syntax guide covering all its features, with examples for each diagram type.

---

### **1. Basic Syntax**
- **Diagram Declaration**: Use a keyword to define the diagram type.
  ```mermaid
  diagram_type;
  ```
  ```txt
  diagram_type;
  ```
- **Comment**: Add comments using `%%`.
  ```mermaid
  %% This is a comment
  ```
  ```txt
  %% This is a comment
  ```

---

### **2. Diagram Types**

#### **a. Flowcharts**
- **Used for**: Process flows and decision trees.
- **Syntax**:
  ```mermaid
  graph [Direction];
  A[Start] --> B[Process];
  B --> C{Decision};
  C -->|Yes| D[Result 1];
  C -->|No| E[Result 2];
  ```
  ```txt
  graph [Direction];
  A[Start] --> B[Process];
  B --> C{Decision};
  C -->|Yes| D[Result 1];
  C -->|No| E[Result 2];
  ```
- **Direction Options**:
  - `TD` (Top-Down)
  - `LR` (Left-Right)
  - `BT` (Bottom-Top)
  - `RL` (Right-Left)
- **Arrow Styles**:
  - `-->` (Standard arrow)
  - `-.->` (Dashed arrow)
  - `==>` (Thick arrow)
  - `---` (No arrow)

---

#### **b. Sequence Diagrams**
- **Used for**: Interaction flows between participants over time.
- **Syntax**:
  ```mermaid
  sequenceDiagram;
  participant A as User;
  participant B as System;
  A->>B: Request Data;
  B-->>A: Response Data;
  A->>B: Another Request;
  ```
  ```txt
  sequenceDiagram;
  participant A as User;
  participant B as System;
  A->>B: Request Data;
  B-->>A: Response Data;
  A->>B: Another Request;
  ```
- **Key Components**:
  - `participant`: Defines entities.
  - `->>`: Solid arrow for messages.
  - `-->>`: Dashed arrow for responses.
  - `Note`:
    ```mermaid
    Note over A: User sends a request;
    ```
    ```txt
    Note over A: User sends a request;
    ```

---

#### **c. Class Diagrams**
- **Used for**: Object-oriented design and relationships.
- **Syntax**:
  ```mermaid
  classDiagram;
  class Person {
      +String name;
      +int age;
      +void display();
  }
  Person <|-- Student: Inherits;
  Person *-- Address: Aggregates;
  ```
  ```txt
  classDiagram;
  class Person {
      +String name;
      +int age;
      +void display();
  }
  Person <|-- Student: Inherits;
  Person *-- Address: Aggregates;
  ```
- **Relationship Types**:
  - `<|--`: Inheritance
  - `*--`: Composition
  - `o--`: Aggregation
  - `..`: Dependency

---

#### **d. Gantt Charts**
- **Used for**: Timelines and task scheduling.
- **Syntax**:
  ```mermaid
  gantt;
  title Project Timeline;
  section Development;
  Task 1 :a1, 2024-01-01, 10d;
  Task 2 :after a1, 5d;
  ```
  ```txt
  gantt;
  title Project Timeline;
  section Development;
  Task 1 :a1, 2024-01-01, 10d;
  Task 2 :after a1, 5d;
  ```
- **Key Components**:
  - `section`: Groups tasks.
  - Task format: `[Name] :[ID], [Start Date], [Duration]`.

---

#### **e. Pie Charts**
- **Used for**: Data distribution.
- **Syntax**:
  ```mermaid
  pie;
  title Browser Market Share;
  "Chrome" : 65;
  "Firefox" : 20;
  "Edge" : 10;
  ```
  ```txt
  pie;
  title Browser Market Share;
  "Chrome" : 65;
  "Firefox" : 20;
  "Edge" : 10;
  ```

---

#### **f. Entity-Relationship (ER) Diagrams**
- **Used for**: Database schemas.
- **Syntax**:
  ```mermaid
  erDiagram;
  CUSTOMER {
      string name;
      string email;
  }
  ORDER {
      int id;
      date order_date;
  }
  CUSTOMER ||--o{ ORDER: places;
  ```
  ```txt
  erDiagram;
  CUSTOMER {
      string name;
      string email;
  }
  ORDER {
      int id;
      date order_date;
  }
  CUSTOMER ||--o{ ORDER: places;
  ```
- **Key Components**:
  - Entity definition: `[EntityName] { [Type] [Attribute] }`
  - Relationships:
    - `||--o{`: One-to-Many
    - `|o--o|`: One-to-One
    - `}o--o{`: Many-to-Many

---

#### **g. State Diagrams**
- **Used for**: Finite-state machines.
- **Syntax**:
  ```mermaid
  stateDiagram-v2;
  [*] --> Start;
  Start --> Processing;
  Processing --> [*];
  Processing --> Error: Validation Failed;
  ```
  ```txt
  stateDiagram-v2;
  [*] --> Start;
  Start --> Processing;
  Processing --> [*];
  Processing --> Error: Validation Failed;
  ```
- **Transitions**:
  - `[Label] --> [Target]`.
  - Add labels for conditions.

---

#### **h. Mindmaps**
- **Used for**: Hierarchical structures and brainstorming.
- **Syntax**:
  ```mermaid
  mindmap;
  root
      child1
          grandchild1
          grandchild2
      child2
          grandchild3
  ```
  ```txt
  mindmap;
  root
      child1
          grandchild1
          grandchild2
      child2
          grandchild3
  ```

---

### **3. Styling and Customization**
- **CSS Classes**: Apply styles to nodes.
  ```txt
  graph TD;
  A[Start]:::customStyle;
  classDef customStyle fill:#f9f,stroke:#333,stroke-width:4px;
  ```

  ```mermaid
  graph TD;
  A[Start]:::customStyle;
  classDef customStyle fill:#f9f,stroke:#333,stroke-width:4px;
  ```
- **Themes**: Change diagram appearance using themes.
  ```txt
  %%{ init: { "theme": "dark" } }%%
  ```

  ```mermaid
  %%{ init: { "theme": "dark" } }%%
  ```

---

### **4. Advanced Features**
- **Subgraphs**: Group nodes into clusters.
  ```txt
  graph TD;
  subgraph Cluster;
      A --> B;
  end;
  ```

  ```mermaid
  graph TD;
  subgraph Cluster;
      A --> B;
  end;
  ```

- **Hyperlinks**: Add links to nodes.
  ```txt
  A[Node] --> B[Linked Node];
  click B "https://example.com" "Tooltip";
  ```

  ```mermaid
  A[Node] --> B[Linked Node];
  click B "https://example.com" "Tooltip";
  ```

- **Directional Labels**:
  ```txt
  graph LR;
  A -->|Label| B;
  ```

  ```mermaid
  graph LR;
  A -->|Label| B;
  ```

---

### **5. Additional Diagram Types**

#### **a. User Journey Diagrams**
- **Used for**: Visualizing customer experiences.
- **Syntax**:
  ```txt
  journey;
  title User Journey for Signup;
  section Discovery;
    User: 5: Finds Website;
  section Signup;
    User: 4: Enters Details;
    System: 3: Sends Confirmation Email;
  section Onboarding;
    User: 5: Completes Profile;
    System: 4: Shows Dashboard;
  ```

  ```mermaid
  journey;
  title User Journey for Signup;
  section Discovery;
    User: 5: Finds Website;
  section Signup;
    User: 4: Enters Details;
    System: 3: Sends Confirmation Email;
  section Onboarding;
    User: 5: Completes Profile;
    System: 4: Shows Dashboard;
  ```

- **Components**:
  - `section`: Define stages.
  - `[Role]: [Emotion Score]: [Action]`.

---

#### **b. Git Graphs**
- **Used for**: Representing Git commit history.
- **Syntax**:
  ```txt
  gitGraph;
  commit id: "Initial Commit";
  branch feature;
  checkout feature;
  commit id: "Feature Added";
  checkout main;
  merge feature;
  ```

  ```mermaid
  gitGraph;
  commit id: "Initial Commit";
  branch feature;
  checkout feature;
  commit id: "Feature Added";
  checkout main;
  merge feature;
  ```

---

#### **c. Timeline Diagrams**
- **Used for**: Representing events chronologically.
- **Syntax**:
  ```txt
  timeline;
  title Project Timeline;
  section Phase 1;
    Task 1: 2023-01-01: 2023-01-10;
    Task 2: 2023-01-11: 2023-01-15;
  section Phase 2;
    Task 3: 2023-02-01: 2023-02-20;
  ```

  ```mermaid
  timeline;
  title Project Timeline;
  section Phase 1;
    Task 1: 2023-01-01: 2023-01-10;
    Task 2: 2023-01-11: 2023-01-15;
  section Phase 2;
    Task 3: 2023-02-01: 2023-02-20;
  ```

---
### **6. Advanced Features**

#### **a. Dynamic Data Integration**
Mermaid allows injecting data dynamically for diagrams. This is particularly useful in applications or dashboards.

---

#### **b. Loop and Conditions in Sequence Diagrams**
- Add loops and conditions to make sequence diagrams dynamic.
  ```txt
  sequenceDiagram;
  participant A;
  participant B;
  loop Process Multiple Items;
      A->>B: Process Item;
      B-->>A: Item Processed;
  end;
  alt Success;
      A->>B: Acknowledgment;
  else Failure;
      A->>B: Retry;
  end;
  ```

  ```mermaid
  sequenceDiagram;
  participant A;
  participant B;
  loop Process Multiple Items;
      A->>B: Process Item;
      B-->>A: Item Processed;
  end;
  alt Success;
      A->>B: Acknowledgment;
  else Failure;
      A->>B: Retry;
  end;
  ```

---

#### **c. Pseudo-Styling for Better Presentation**
- Use labels, shapes, or icons for better readability. For example:
  ```txt
  graph TD;
  A([Round Node]) --> B((Circle Node));
  B --> C{{Diamond Node}};
  ```

  ```mermaid
  graph TD;
  A([Round Node]) --> B((Circle Node));
  B --> C{{Diamond Node}};
  ```

---

#### **d. Global Configurations**
- Customize globally:
  ```txt
  %%{ init: { "theme": "default", "themeVariables": { "primaryColor": "#ffcc00" } } }%%;
  graph TD;
  ```

  ```mermaid
  %%{ init: { "theme": "default", "themeVariables": { "primaryColor": "#ffcc00" } } }%%;
  graph TD;
  ```

---

### **7. Useful Tools and Features**

#### **a. Debugging Mode**
- Use `%%{debug}%%` to enable debugging and identify issues in diagram generation.

#### **b. External Links in ER Diagrams**
- Enhance ER diagrams with external references:
  ```txt
  erDiagram;
  CUSTOMER {
      string name;
      string email;
  }
  link CUSTOMER "https://example.com";
  ```

  ```mermaid
  erDiagram;
  CUSTOMER {
      string name;
      string email;
  }
  link CUSTOMER "https://example.com";
  ```

---

### **8. Plugin Support**
Mermaid integrates well with tools like:
- Markdown renderers (e.g., GitHub, Obsidian)
- Presentation tools (e.g., Reveal.js)
- Static site generators (e.g., Docusaurus)

---

### **9. Examples of Nested Relationships**
For complex diagrams, Mermaid allows combining features:
```txt
graph TD;
  subgraph Backend;
      DB[(Database)] --> API;
  end;
  subgraph Frontend;
      User --> UI[User Interface];
      UI --> API;
  end;
```

```mermaid
graph TD;
  subgraph Backend;
      DB[(Database)] --> API;
  end;
  subgraph Frontend;
      User --> UI[User Interface];
      UI --> API;
  end;
```

---