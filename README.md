graph TD
    subgraph Camera Troubleshooting Flowchart
        direction TB

        %% ------ 1. DEFINE ALL NODES ------
        subgraph "Technician / L1 Support"
            A[Start: Symptom - Camera is Offline];
            B{Is camera feed accessible<br>in the viewing application?};
            C[END: Escalate to<br>Application/Backend Team];
            D{Check camera power at<br>Junction Box (JB)};
            E{Check Cat6 data cable<br>from JB to Camera};
            F{Check port status/lights<br>on JB Switch for the camera};
            G{Check fiber link status<br>from JB to Core Switch (CS)};
            H{Is the Core Switch (CS)<br>powered and online?};
            I{Check main Power/Fiber<br>infrastructure feeding the area (UF)};
            J[END: Issue is complex.<br>Engage Senior Network/Infra Teams];
        end

        subgraph "Application / Backend Team"
            C1[Investigate application,<br>server, or database issue];
        end

        subgraph "NEC (Power & Copper)"
            D1[END: Fix power issue at JB<br>(e.g., UPS, Battery, Breaker)];
            E1[END: Replace Cat6 Cable];
            F1[END: Check/Replace<br>JB Switch];
            H1[END: Check Power Line to CS];
            I1[END: Check Power Feed (UF)];
        end

        subgraph "Rafftel (Fiber & Core HW)"
            G1[END: Repair Fiber Link<br>from JB to CS];
            H2[END: Check/Replace<br>Core Switch (CS)];
            I2[END: Check Fiber Feed (UF)];
        end

        %% ------ 2. DEFINE ALL CONNECTIONS ------
        A --> B;
        B -- YES --> C;
        B -- NO --> D;
        C --> C1;
        D -- Power OK --> E;
        D -- Power NOT OK --> D1;
        E -- Cable OK --> F;
        E -- Cable FAULTY --> E1;
        F -- Port OK/Active --> G;
        F -- "Port Dead / Switch Offline" --> F1;
        G -- Link OK --> H;
        G -- Link DOWN --> G1;
        H -- YES --> I;
        H -- "NO (Power Issue)" --> H1;
        H -- "NO (Hardware Issue)" --> H2;
        I -- INFRA OK --> J;
        I -- "INFRA NOT OK" --> I1;
        I -- "INFRA NOT OK" --> I2;

    end

    %% --- 3. STYLING ---
    style C fill:#ffcccb,stroke:#333,stroke-width:2px
    style J fill:#ffcccb,stroke:#333,stroke-width:2px
    style C1 fill:#ffcccb,stroke:#333,stroke-width:2px
    style D1 fill:#ffcccb,stroke:#333,stroke-width:2px
    style E1 fill:#ffcccb,stroke:#333,stroke-width:2px
    style F1 fill:#ffcccb,stroke:#333,stroke-width:2px
    style G1 fill:#ffcccb,stroke:#333,stroke-width:2px
    style H1 fill:#ffcccb,stroke:#333,stroke-width:2px
    style H2 fill:#ffcccb,stroke:#333,stroke-width:2px
    style I1 fill:#ffcccb,stroke:#333,stroke-width:2px
    style I2 fill:#ffcccb,stroke:#333,stroke-width:2px
    style A fill:#d4edda,stroke:#333,stroke-width:2px
