# 09 - Research Workspace

## Part 3

Version: 1.0

Status: Planning

---

# Citation Manager

## Purpose

The Citation Manager provides complete reference management with BibTeX support, Zotero integration, multiple citation styles, and automatic citation generation.

---

# Citation Manager Architecture

Citation Manager
- Reference Database
- BibTeX Editor
- Zotero Sync
- Style Engine
- Citation Generator
- Reference Scanner

---

# Reference Database

Central storage for all references.

Reference Types

Article (journal, conference)

Book

Book Chapter

Thesis

Technical Report

Dataset

Software

Web Page

Patent

Standard

Each type has appropriate fields.

---

# Entity: references

Purpose

Stores reference metadata.

Fields

reference_id

cite_key (unique citation key)

reference_type

title

authors (JSON array)

year

journal

volume

issue

pages

doi

url

arxiv_id

isbn

publisher

school (for theses)

how_published

note

keywords

tags

collections

attachments (PDF path)

created_at

---

# BibTeX Management

Full BibTeX support.

BibTeX Features

Import .bib file

Export .bib file

Edit BibTeX entries

Validate BibTeX syntax

Auto-generate cite keys

Search entries

BibTeX entries sync with the reference database.

---

# Zotero Integration

Sync with Zotero reference manager.

Sync Features

One-way sync (Zotero -> PAIOS)

Two-way sync (keep both updated)

Import Zotero collections

Sync attachments (PDFs)

Sync notes and tags

Conflict resolution

Zotero sync is optional and configurable.

---

# Citation Style Support

Multiple citation and bibliography styles.

Supported Styles

APA (6th, 7th)

MLA (8th, 9th)

IEEE

Chicago (Author-Date, Notes-Bibliography)

Harvard

Vancouver

Nature

Science

Custom CSL (Citation Style Language) files

---

# Citation Generator

Generate citations and bibliographies.

Generation Features

Select Style

Select References

Generate In-Text Citation

Generate Bibliography

Copy to Clipboard

Export to Document

Citations are generated in the selected style.

---

# Reference Scanning

Scan documents for citations.

Scanning Features

Detect Citation Markers (e.g., [@smith2024])

Extract Cited References

Match to Database Entries

Add Missing References

Update Bibliography

Reference scanning works with PAIOS documents and external files.

---

# Reference Collections

Organize references into collections.

Collection Features

Create Collections (by project, topic, paper)

Drag and Drop References

Shared Collections (across projects)

Collection Statistics (count, recent additions)

---

# Auto-Complete Citation

Cite references while writing.

Writing Integration

Type @ to search references

Select from dropdown

Insert formatted citation

Auto-add to bibliography

Works in PAIOS Notebook and external editors via plugin.

---

# Duplicate Detection

Detect and merge duplicate references.

Detection Criteria

DOI Match

Title Similarity

Author + Year + Title

Duplicate suggestions are reviewed before merging.

---

# Events

Events published to Event Store

research.citation.added

research.citation.updated

research.citation.merged

research.citation.exported

research.collection.created

research.zotero.synced

---

# Summary

The Citation Manager provides comprehensive reference management with BibTeX, Zotero integration, multiple citation styles, and automatic citation generation.

---

# End of Part 3

Next

Part 4

- Experiment Manager
- Research Experiment Lifecycle
- Hypothesis Testing
- Data Collection
- Results Analysis
- Reproducibility
