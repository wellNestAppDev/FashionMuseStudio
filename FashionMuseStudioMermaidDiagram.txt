graph TD
    A[User] --> UC0[Visit Application]
    UC0 --> UC1A[Register Account (Email/Pass, Social)]
    UC0 --> UC1B[Login (Email/Pass, Social, Magic Link)]
    
    UC1B --> UC4[Access User Dashboard]
    UC4 --> UCProj1[Create/View Projects]
    UC4 --> UCColl1[Create/View Collections]
    UC4 --> UCAsset1[Manage Personal Asset Libraries]
    UC4 --> G2[View Personal Image Gallery]
    UC4 --> P2[Manage Personal Saved Prompts]
    UC4 --> CF[Browse Community Feed]

    A --> UC2[Manage User Profile & Privacy Settings]
    A --> UC3[Manage App Settings (Defaults, Watermark)]

    subgraph Core App Interaction
        UC1A; UC1B; UC2; UC3; UC4; UCProj1; UCColl1; UCAsset1;
    end

    UC5{Start New Image Creation Project}
    UC4 --> UC5
    UCProj1 --> UC5 %% Start from project

    UC5 --> I1[Define Scene Setup (Tab 1)]
    I1 --> ApplySavedSnippet[Apply Saved Style Snippet]
    I1 --> ApplySavedColorPalette[Apply Saved Color Palette]
    UC5 --> I2[Customize Model (Tab 2)]
    UC5 --> I3[Set Pose & Composition (Tab 3)]
    UC5 --> I4[Select Stylistic Effects (Tab 4)]
    UC5 --> I5[Use Advanced Prompting Tools]
    I5 --> ApplySavedNegatives[Apply Saved Negative Prompt Set]
    
    A --> UC6P{Generate Image (via Secure Proxy)}
    UC6P --> FalAI[(Fal.ai API)]
    UC6P --> UC6Batch[Request Batch Generation/Variations]
    
    A --> UC7[View & Interact with Generated Image]
    UC7 --> G1[Save Image to Gallery/Project (Supabase)]
    G1 --> SPI[Set Image Public/Private & Sharing Options]
    UC7 --> Upscale[Upscale Image]
    Upscale -.-> FalAIUpscaler[(Fal.ai Upscaler via Proxy)]
    UC7 --> G4[Download Image (with Watermark/Format Choice)]
    UC7 --> UC9{Evolve This Image}
    
    subgraph Output & Advanced Tools
      UC6Batch; Upscale; G4; UC9;
    end
    
    subgraph Community Interaction
        CF --> VPI[View Public Item Details]
        CF --> LPI[Like Public Item]
        CF --> RPI[Remix/Evolve Public Item]
        A --> VUP[View Others' Public Profiles]
    end
    
    A --> G2; A --> P2;

    style A fill:#f9f,stroke:#333,stroke-width:2px