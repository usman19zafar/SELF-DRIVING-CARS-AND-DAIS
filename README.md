```mermaid
mindmap
  root((Safety Standards Compare))
    ISO_26262
      Focus:::iso[Functional Safety]
      Governs_meaning:::iso[No]
      Governs_drift:::iso[No]
      Semantic_lifecycle:::iso[No]
      Occlusion_meaning:::iso[No]
      Cross_model_contradictions:::iso[No]
      Semantic_scoring:::iso[No]
      Tiering:::iso[No]
      Fading_logic:::iso[No]
      Semantic_diagnostics:::iso[No]
      SSCEs:::iso[No]
      Complements_AV:::iso[Yes]
    SOTIF
      Focus:::sotif[Safety of Intended Functionality]
      Governs_meaning:::sotif[No]
      Governs_drift:::sotif[Partial]
      Semantic_lifecycle:::sotif[No]
      Occlusion_meaning:::sotif[Partial]
      Cross_model_contradictions:::sotif[No]
      Semantic_scoring:::sotif[No]
      Tiering:::sotif[No]
      Fading_logic:::sotif[No]
      Semantic_diagnostics:::sotif[No]
      SSCEs:::sotif[No]
      Complements_AV:::sotif[Yes]
    DAIS_10
      Focus:::dais[Semantic Safety]
      Governs_meaning:::dais[Yes]
      Governs_drift:::dais[Yes]
      Semantic_lifecycle:::dais[Yes]
      Occlusion_meaning:::dais[Yes]
      Cross_model_contradictions:::dais[Yes]
      Semantic_scoring:::dais[Yes]
      Tiering:::dais[Yes]
      Fading_logic:::dais[Yes]
      Semantic_diagnostics:::dais[Yes]
      SSCEs:::dais[Yes]
      Complements_AV:::dais[Yes]
```

```text
+----------------------------------------+-------------+-------------------------------+-------------+
|                Dimension               | ISO 26262   |            SOTIF              |   DAIS‑10   |
+----------------------------------------+-------------+-------------------------------+-------------+
| Focus                                  | Functional  | Safety of Intended            | Semantic    |
|                                        | Safety      | Functionality                 | Safety      |
+----------------------------------------+-------------+-------------------------------+-------------+
| Governs meaning                        | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Governs drift                          | No          | Partial                       | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Governs semantic lifecycle             | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Handles occlusion meaning              | No          | Partial                       | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Handles cross‑model contradictions     | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Provides semantic scoring              | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Provides tiering                       | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Provides fading logic                  | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Provides semantic diagnostics          | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Handles SSCEs                          | No          | No                            | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
| Complements AV stack                   | Yes         | Yes                           | Yes         |
+----------------------------------------+-------------+-------------------------------+-------------+
```

```mermaid
flowchart LR

    A[ISO 26262<br/>Functional Safety] --> D[Complete AV Safety Stack]
    B[SOTIF<br/>Safety of Intended Functionality] --> D
    C[DAIS‑10<br/>Semantic Safety] --> D

    subgraph A1[ISO 26262 Capabilities]
        A2[No meaning governance]
        A3[No drift governance]
        A4[No semantic lifecycle]
        A5[No occlusion meaning]
        A6[No semantic diagnostics]
    end

    subgraph B1[SOTIF Capabilities]
        B2[No meaning governance]
        B3[Partial drift handling]
        B4[No semantic lifecycle]
        B5[Partial occlusion handling]
        B6[No semantic diagnostics]
    end

    subgraph C1[DAIS‑10 Capabilities]
        C2[Governs meaning]
        C3[Governs drift]
        C4[Governs semantic lifecycle]
        C5[Handles occlusion meaning]
        C6[Resolves cross‑model contradictions]
        C7[Semantic scoring]
        C8[Tiering]
        C9[Fading logic]
        C10[Semantic diagnostics]
        C11[Handles SSCEs]
    end
```
