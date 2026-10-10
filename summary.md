# Project Summary

## Repository: AI_assessment_7

This repository is a research replication package for the paper "Database Report: Twin-2K-500: A Data Set for Building Digital Twins of over 2,000 People Based on Their Answers to over 500 Questions". The goal is to computationally reproduce the original findings using the authors' published replication assets and evaluation scripts.

## What this project contains

- `README.md`: high-level project overview and replication instructions
- `INSTRUCTIONS.md`: step-by-step workflow for an AI agent operating under strict human review checkpoints
- `notes/`: generated research and validation documents, including:
  - `paper_summary.md`
  - `literature_verification.md`
  - `replication_scope.md`
  - `data_inventory.md`
  - `environment_setup.md`
  - `codebase_review.md`
- `MktS_2025_Database Report Twin-2K-500 A Data Set for Building Digital Twins of over 2,000 People.pdf`: the main paper used as reference

## Main objective

The project is designed to replicate the study's findings on whether large language model (LLM)-based digital twins can approximate human behavior and recover known behavioral economics effects. The replication work focuses on:

1. Individual-level accuracy comparisons using Mean Absolute Deviation (MAD)
2. Aggregate-level behavior comparisons across within-subject and between-subject experiments
3. Comparison against a non-LLM baseline, including the XGBoost pipeline described in the replication materials

## Research workflow

The repository is organized around a staged, human-in-the-loop process:

- Phase 0: environment setup and data verification
- Phase 1: paper understanding and literature verification
- Phase 2: data validation and replication execution
- Phase 3: final report writing and reproducibility documentation

This structure is intentional: the instructions explicitly require stop-and-check review points before advancing to the next phase.

## Intended execution model

The project expects a local Python environment managed with Poetry and a working copy of the original replication materials under `orig/MktS_2025/`. The evaluation scripts described in the notes are meant to validate the precomputed LLM outputs and compare them against human benchmark responses.

## Why it matters

This repo sits at the intersection of academic replication, AI evaluation, and behavioral science. It explores whether LLM-generated digital twins can capture real human responses and behavior patterns, while also emphasizing reproducibility, validation, and careful documentation of discrepancies.

## Relevant artifacts

The most important files for understanding the project are:

- `README.md`
- `INSTRUCTIONS.md`
- `notes/paper_summary.md`
- `notes/replication_scope.md`
- `notes/codebase_review.md`

These files explain the objective, methodology, scope, and technical checks used throughout the project.
