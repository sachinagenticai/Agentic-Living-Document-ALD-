# Truth-Anchor Layer

## Overview

The Truth-Anchor Layer is the provenance and state foundation of the ALD Protocol. Its responsibility is to preserve the canonical meaning of each document or semantic block while keeping the document system verifiable, auditable, and efficient to update.

This layer treats content as a sequence of evolving semantic units, not just plain text. Each unit can be versioned, hashed, and recomputed independently when changes occur.

## Core Concept

A Merkle-DAG state-tree maps each semantic block to a version hash. In practice, this means:

- a document is split into meaningful units such as claims, paragraphs, sections, or structured fields
- each unit receives a deterministic hash that represents its current content
- the hashes are linked into a directed acyclic graph (DAG)
- parent-child relationships preserve the history of revisions and dependencies

This structure allows the system to answer two important questions:

1. What is the current version of this block?
2. What changed from the previous version?

## How the Merkle-DAG Works

### 1. Semantic Block Identification

Before hashing, the system identifies semantic blocks. These are the units that matter for reasoning or update propagation.

Examples include:

- a claim statement
- a table row
- a summary section
- a policy statement
- a code snippet with metadata

### 2. Hash Generation

Each block is converted into a stable representation and hashed using a deterministic algorithm. The resulting hash becomes the block’s version fingerprint.

The hash should include:

- block content
- block type or schema
- relevant metadata
- references to prior state where applicable

### 3. DAG Linking

Each new version of a block points to its parent version. The resulting graph forms a Merkle-DAG:

- each node is a state snapshot of a semantic block
- each edge represents a revision lineage
- the root or latest state can be verified through the hash chain

This makes the history of the block explicit and inspectable.

## Incremental Refreshes

The main advantage of this design is incremental refresh. Instead of recomputing every block in a document, the system can:

- detect which semantic blocks changed
- recompute only the affected hashes
- update only the impacted parent nodes in the DAG
- propagate new state references without rebuilding the entire document graph

This is especially useful for large knowledge documents, long-lived reports, and multi-agent systems where only a small portion of content changes at a time.

## Why This Is Better Than Flat Versioning

A traditional document version system often stores only the latest blob of text. That approach has several limitations:

- it does not identify which parts changed
- it makes large refreshes expensive
- it lacks an explicit audit trail for each semantic unit
- it does not scale well in multi-agent reasoning workflows

The Merkle-DAG state-tree improves this by:

- isolating changes at the semantic-block level
- enabling efficient partial refreshes
- preserving a verifiable revision history
- supporting trust and explainability in downstream reasoning

## Operational Benefits

The Truth-Anchor Layer helps the ALD Protocol achieve:

- faster incremental updates
- precise provenance tracking
- better cacheability for stateful documents
- clearer auditability for automated systems

## Summary

The Merkle-DAG state-tree is the core mechanism that turns semantic blocks into verifiable, versioned units of truth. By mapping each block to a version hash and linking those hashes into a DAG, the ALD Protocol provides a scalable and trustworthy foundation for incremental refreshes and long-lived document intelligence.
