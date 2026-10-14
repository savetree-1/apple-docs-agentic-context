# Apple Docs Agentic Context

> Structured, offline-first Apple Developer Documentation in clean Markdown, curated specifically as context infrastructure for AI coding agents, LLMs, and pair-programming assistants.

---

## Overview and Purpose

Official Apple Developer Documentation is comprehensive, but it is fundamentally engineered for human browser consumption: it is heavily gated behind client-side JavaScript, fragmented across thousands of dynamic web endpoints, and costly to repeatedly scrape or fetch during active AI coding sessions.

When AI agents rely exclusively on live web scraping or general training memory, development experiences:
- Excessive Token Consumption: Redundant scraping and HTML boilerplate ingestion.
- API Hallucinations: Inventing obsolete or fictitious APIs when web scraping fails.
- Outdated Patterns: Defaulting to legacy iOS 14-18 patterns because older code dominates generic training datasets.
- Latency and Rate Limiting: Stalled coding iterations waiting for browser rendering or external HTTP calls.

Apple Docs Agentic Context solves this by establishing local-first documentation infrastructure. By maintaining clean, structured Markdown versions of 376+ Apple frameworks directly in repository context, AI agents can read verified API signatures, parameter requirements, availability attributes, and architecture guidelines instantaneously with zero token overhead.

---

## Architecture: The Hybrid Agentic Loop

This repository serves as the primary local knowledge base within a two-tier documentation-first architecture:

```
+--------------------------------------------------------+
|                    AI Coding Agent                     |
+---------------------------+----------------------------+
                            |
              1. Query Local Documentation
              (Fast, Zero-Token, Unmodified)
                            v
+--------------------------------------------------------+
|     Local Apple Docs Knowledge Base (This Repo)        |
|          376+ Frameworks in Structured Markdown        |
+---------------------------+----------------------------+
                            |
             2. Deep Live Expansion (If Needed)
             (Edge cases, specific symbol lookups)
                            v
+--------------------------------------------------------+
|           MCP Live Server (e.g. Sosumi.ai)             |
+---------------------------+----------------------------+
                            |
              3. Live Ground Truth Validation
                            v
+--------------------------------------------------------+
|       Official Apple Developer Documentation / HIG     |
+--------------------------------------------------------+
```

1. Tier 1 (Local First): The AI agent searches and reads the relevant framework document in `Apple-Documentation/` to discover classes, protocols, methods, and system requirements.
2. Tier 2 (MCP Expansion): If deep symbol resolution, WWDC transcripts, or interactive sample code is required, the agent calls an Apple-compatible Model Context Protocol (MCP) tool (such as `sosumi` or official Apple MCP).
3. Tier 3 (Native Verification): Ground truth is cross-referenced to ensure the implementation strictly adopts Apple's native APIs and avoids reinventing system features.

---

## What This Repository Contains

The `Apple-Documentation/` directory preserves 377 complete, unmodified Apple documentation files, spanning all Apple platforms:
- iOS and iPadOS
- macOS
- watchOS
- tvOS
- visionOS

### Core Framework Categorization

| Domain | Key Included Frameworks |
| :--- | :--- |
| Modern UI and Layout | `UIKit`, `SwiftUI`, `AppKit`, `WidgetKit`, `ActivityKit`, `CarPlay`, `TVUIKit` |
| System and Foundation | `Foundation`, `Swift`, `Combine`, `Observation`, `Dispatch`, `Uniform Type Identifiers` |
| Media, Audio and Graphics | `AVFoundation`, `AVKit`, `Core Audio`, `Audio Toolbox`, `Metal`, `Core Graphics`, `Core Animation`, `Image I-O` |
| Machine Learning and AI | `Foundation Models`, `Core ML`, `Vision`, `Natural Language`, `Create ML`, `Sound Analysis`, `Speech` |
| Spatial and Extended Reality | `RealityKit`, `ARKit`, `Compositor Services`, `Spatial`, `ShaderGraph`, `RoomPlan` |
| Persistence and Cloud | `SwiftData`, `Core Data`, `CloudKit`, `File Provider`, `Shared with You` |
| Hardware and Peripherals | `Core Bluetooth`, `Core Location`, `Core Motion`, `Core NFC`, `External Accessory`, `AccessorySetupKit` |
| Security and Identity | `Security`, `Authentication Services`, `CryptoKit`, `Local Authentication`, `DeviceCheck` |
| Commerce and Subscriptions | `StoreKit`, `PassKit (Apple Pay and Wallet)`, `MarketplaceKit`, `AdAttributionKit` |
| Testing and Quality | `XCTest`, `Swift Testing`, `MetricKit`, `OSLog`, `Developer Tools Support` |

---

## Instructions for AI Coding Agents

When working on Apple platform codebases with access to this repository, AI agents should follow these mandatory operational instructions:

### 1. Research Before Changing Code
- Never guess APIs: Do not implement features based on probabilistic recall or pre-iOS-20 assumptions.
- Search local markdown first: Inspect `Apple-Documentation/<Framework>.md` (e.g. `Apple-Documentation/UIKit.md`, `Apple-Documentation/Foundation Models.md`, `Apple-Documentation/SwiftData.md`) to verify class signatures, method parameters, and availability macros.

### 2. Verify Native System Support First
- Before designing custom components (custom blurs, custom bottom sheets, custom navigation bars, custom media loaders, custom tags), search the documentation to determine whether Apple already provides a native solution (e.g., `UICollectionViewCompositionalLayout`, `UISheetPresentationController`, `UIVisualEffectView`, native symbols, or modern system toolbars).
- Reject legacy workarounds: Do not copy deprecated Objective-C style hacks or reflection patterns (`sharedApplication`, recursive keyWindow traversal) when modern Apple APIs exist.

### 3. Maintain Documentation Integrity
- The documentation in `Apple-Documentation/` represents canonical Apple technical documentation. Keep the source markdown content unmodified so all downstream agents have identical, consistent references.

---

## Usage Example in Agent Prompts

Add the following context rule to your agent workflow configuration (e.g., `AGENTS.md`, `GEMINI.md`, or IDE instructions):

```markdown
### Apple Documentation Reference
When designing or modifying Apple platform code:
1. First read the corresponding documentation in `Apple-Documentation/<Framework>.md`.
2. Confirm the minimum deployment target and API availability.
3. Adopt the official Apple-recommended patterns and Human Interface Guidelines.
4. Only if the local documentation lacks specific symbol details, query the MCP server.
```

---

## Source and Legal Notices

- The documentation contained within `Apple-Documentation/` is based on official Apple Developer Documentation and technical resources published by Apple Inc.
- All product names, logos, trademarks, and registered trademarks belong to their respective owners. Apple, iOS, iPadOS, macOS, watchOS, tvOS, visionOS, Swift, SwiftUI, Xcode, and Cocoa are trademarks of Apple Inc.
