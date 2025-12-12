Internet-Draft                                             T. Hanamaruki
Intended status: Informational                                     2025
Expires: TBD

TPS-Based Horizontal API Layering Model
A Structural Safety and Stability Framework for Modern Agent-Based APIs
Abstract

This document proposes a standardized architectural model that introduces
a horizontally isolated API execution layer (Layer4-H) to prevent
unbounded recursion, cross-layer propagation, and cost instability
in modern agent-based API systems.

This model derives from Toyota Production System (TPS) principles and
is compatible with existing three-layer legacy API designs.

Status of This Memo

This memo is submitted to the IETF for consideration as an Informational
Internet-Draft. It does not specify an Internet standard of any kind.
Discussion and feedback are encouraged.

1. Introduction

Traditional API architectures were originally designed for offline,
local-execution environments. These systems relied on a three-layer model:

Layer1: Execution / Hardware

Layer2: System Services

Layer3: Developer Sandbox (black-box logic)

With the rapid expansion of cloud APIs and autonomous agent systems,
two additional layers were added:

Layer4: Public API Surface

Layer5: Agent Runtime / Tool Orchestration

However, these were vertically stacked on top of the legacy model, producing:

A single unbounded execution chain

High coupling across layers

Error propagation without isolation

Recursion leading to uncontrolled API usage ("runaway billing")

Instability in multi-agent and large-context systems

This document defines a structural solution.

2. Terminology

Vertical Layer Coupling (VLC)
A condition where control flow passes directly through all layers
without isolation, enabling error cascades.

Cross-Layer Vibration (CLV)
Unbounded propagation of retries or agent actions across layers.

Layer4-H (Horizontal Safety Gateway)
A new deterministic layer inserted horizontally between Layer5
and the legacy Layer3–1 stack.

Agent Originated Operation (AOO)
Any API-triggered behavior initiated by an autonomous agent.

3. Problem Statement

The legacy vertical architecture enables:

uncontrolled recursion (Layer5 repeatedly calling into Layer3–1)

unpredictable API cost exposure

mixed behavior due to legacy/modern path overlap

silent truncation under high complexity workloads

failure modes that are non-local and hard to trace

These issues are systemic, not implementation-specific.

4. Proposed Architecture: Horizontal Layer4-H Isolation
4.1 Overview

A new horizontal safety layer (Layer4-H) is introduced between
Layer5 and Layer3.

This layer:

terminates all agent-originated operations

enforces execution rules and retry ceilings

isolates legacy logic entirely

defines a deterministic, testable API boundary

4.2 Architecture Diagram
                +-----------------------------+
                | Layer5: Agent Runtime       |
                +-----------------------------+
                           |
                +-----------------------------+
                | Layer4-H: Safety Gateway    |
                +-----------------------------+
                           |
-------------------------------------------------------------
|                      Legacy Core                           |
|  Layer3: Developer Sandbox (Blackbox, Non-Normative Space) |
|  Layer2: System Services                                    |
|  Layer1: Execution / Hardware                               |
-------------------------------------------------------------

5. Requirements for Layer4-H

The Layer4-H gateway MUST:

5.1 Isolation Requirements

MUST prevent direct invocation of Layer1–Layer3 by Layer5

MUST define a deterministic finite execution boundary

MUST localize errors within Layer4-H

5.2 Retry and Recursion Control

MUST enforce maximum retry counts

MUST detect cyclic invocation patterns

MUST terminate unbounded recursion deterministically

5.3 Input/Output Regulation

MUST validate request sizes

MUST block malformed or ambiguous agent actions

SHOULD perform context normalization

5.4 Backward Compatibility

MUST NOT modify the behavior of the legacy Layer1–3 stack

SHOULD operate as a transparent intermediary

6. Security Considerations

The architecture reduces:

propagation-based faults

runaway execution loops

ambiguous behavior arising from legacy/modern path overlap

unpredictable resource consumption

It does not introduce additional risks beyond those present in
existing API boundary layers.

7. IANA Considerations

This document makes no request of IANA.

8. Conclusion

Introducing a horizontally isolated safety layer between modern agent
runtimes and legacy core API structures provides:

predictable system behavior

bounded recursion paths

safer agent execution

improved cost stability

interoperability across diverse implementations

This model is intended as a foundation for future API standardization
for agent-based systems.

Author's Address:
   T. Hanamaruki
   GitHub: Hanamaruki-ai
   Email: (optional)