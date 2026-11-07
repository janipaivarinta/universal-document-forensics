# AI Transparency — Universal Document Forensics

**Project:** Universal Document Forensics  
**Document date:** 2026-11-07  
**AI assistant:** OpenAI ChatGPT (GPT-6)

## Purpose of this disclosure

This document describes the use of generative AI assistance in the development and documentation of Universal Document Forensics. It is intended to make the development process more transparent, not to imply that AI-generated output is necessarily correct or independently validated.

## Role of AI assistance

ChatGPT was used as a development assistant in the project, including work on Python code, technical explanations, installation instructions, and project documentation. The exact contribution of AI to individual source-code lines or revisions has not been independently measured. Git history and developer review remain the appropriate records for tracing specific changes.

AI assistance is not a substitute for testing, code review, or professional judgment. The project maintainer remains responsible for selecting, reviewing, testing, and publishing the software and its documentation.

## What the tool does

The tool is designed to inspect supported Office documents and PDFs locally and produce technical reports based on available metadata, file structures, software identifiers, integrity checks, and other observable characteristics. It is designed not to modify the original documents.

The tool does **not** call an AI model to determine whether a document was AI-generated. Its analysis of possible AI-related markers is based on technical indicators, which may have multiple explanations.

## Evidentiary limitations

- Metadata and structural patterns cannot reliably establish whether a person used generative AI.
- Evidence of automated or programmatic document creation is not, by itself, evidence of AI use.
- Software names, timestamps, RSIDs, producer fields, and other indicators may be absent, altered, or rewritten during ordinary editing and conversion.
- A missing marker does not prove that AI was not used; a present marker does not by itself prove misconduct.
- Findings should be corroborated and interpreted by qualified humans, especially in educational or disciplinary contexts.

**The tool must not be treated as an automated academic-misconduct detector or as a basis for disciplinary conclusions without independent assessment and appropriate institutional procedures.**

## Privacy and processing

The software is intended to operate locally, without uploading examined files to an external AI service. Users should review the installed source code and environment before relying on this property. Generated reports can include personal information or sensitive document metadata and should be protected accordingly.

## Validation and ongoing maintenance

A basic test has been described for the seven documented file extensions, including synthetic Office containers and a generated PDF. This is not a comprehensive validation of legacy, encrypted, damaged, or unusual files. Functionality, accuracy, and security should be tested against representative real-world samples before operational use.

Changes to AI-assisted development practices, model usage, or material limitations should be documented in future revisions of this file.

## Licensing

The project's original code and documentation are distributed under the [MIT License](LICENSE). Third-party components remain subject to their own licenses.
