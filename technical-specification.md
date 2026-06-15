# Technical Specification: ALD Protocol

## Overview

The Agentic-Living-Document (ALD) Protocol treats documents as live, stateful services rather than static retrieval objects. This specification explains the technical approach behind the protocol, with emphasis on the state-tree model and its advantages over traditional vector retrieval systems.

## Design goals

The ALD model is built around four practical goals:

- maintain verifiable document state
- preserve provenance across revisions and updates
- support context-aware interpretation by multiple agents
- enable recursive reasoning without losing accountability

## Core mechanism: Merkle-DAG state tree

A Merkle-DAG state tree is a directed graph of state changes where each node carries a cryptographic hash of its contents and references to prior nodes. In simple terms:

- each update to the document creates a new state node
- every node points back to its parent state
- the hash of a node depends on both its data and its linked history

This gives the system a chain of verifiable states. If a document changes, the system can identify exactly what changed, when it changed, and how the new state connects to the previous one.

## How it works in practice

1. A document begins in an initial state.
2. An agent or system action produces a new version of the document.
3. The new version is hashed and linked to the previous version.
4. The resulting structure forms a Merkle-DAG that can be traversed, inspected, and validated.
5. Agents can reason over the current state, the revision path, and the provenance trail.

This means the system does not only store “the latest text”; it stores an evolving record of how meaning and context changed.

## Why this is useful

A Merkle-DAG state tree provides several technical benefits:

- tamper evidence: any change alters the hash chain and becomes detectable
- auditability: the history of edits is preserved in a structured form
- reproducibility: a document state can be reconstructed or verified from the graph
- traceability: agents can explain why a current interpretation emerged from prior states

## Why this is better than a traditional vector database

Traditional vector databases are optimized for semantic similarity search. They are useful for finding nearby embeddings, but they often have limitations in this setting:

- they store semantic similarity, not a full revision history
- they usually do not preserve explicit provenance across changes
- they can lose the causal story behind why a document evolved
- they are weaker for trust-sensitive or long-lived reasoning workflows

A Merkle-DAG state tree improves on this in several important ways:

- state integrity is explicit and hash-linked
- changes are versioned and explainable
- the system supports reasoning over history, not just similarity
- it is more suitable for multi-agent collaboration where trust and traceability matter

In short, vector retrieval is good for finding relevant content. The ALD state-tree model is better for understanding how that content became relevant, what changed, and why it should be trusted.

## Architectural implications

The ALD approach combines:

- semantic retrieval for relevance
- state-tree integrity for trust and revision history
- reasoning hooks for interpretation and recursion

This makes the architecture more suitable for autonomous document services, where documents must behave like evolving agents of context rather than passive data blobs.

## Summary

The Merkle-DAG state-tree mechanism gives ALD a practical foundation for real-world autonomy:

- documents are versioned and verifiable
- reasoning is grounded in explicit state transitions
- agents can collaborate over structured, traceable context

This is the key difference between static RAG and an autonomous, stateful document service.