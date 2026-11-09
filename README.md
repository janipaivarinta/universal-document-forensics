# Universal Document Forensics

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24081280.svg)](https://doi.org/10.5281/zenodo.24081280)

**Version 1.0** · Local, evidence-based technical examination of Office documents and PDFs.

Universal Document Forensics is a Python command-line tool for inspecting document metadata, internal structures, integrity, and software identifiers. It produces human-readable forensic reports while **leaving the original files unchanged**.

The tool is intended to support technical review, including educational and academic-integrity workflows. Its findings require human interpretation: **metadata, software identifiers, and structural characteristics do not reliably prove AI use or academic misconduct.**

## Supported formats

| Format | Technical examinations |
| --- | --- |
| `.docx` | ZIP/XML integrity, metadata, RSIDs, document structure, tracked changes, software and AI-related markers |
| `.doc` | Legacy OLE structure, available metadata, application identifiers, embedded strings |
| `.xlsx` | ZIP/XML integrity, workbook and worksheet structure, formulas, metadata, software markers |
| `.xls` | Legacy OLE structure, available workbook metadata, application identifiers, embedded strings |
| `.pptx` | ZIP/XML integrity, slides, notes, comments, metadata, software markers |
| `.ppt` | Legacy OLE structure, available presentation metadata and embedded strings |
| `.pdf` | PDF structure, metadata, producer/creator, creation dates, embedded-file indicators, software markers |

Additional checks include SHA-256 file hashes and noteworthy technical characteristics. Reports aim to distinguish **indicators of programmatic document generation** from **claims about AI use**; these are not equivalent.

## Requirements

- Python 3 (use a currently supported version).
- The script: `universal_document_forensics.py`.
- Optional Python packages `olefile` and `pypdf` for more complete legacy Office and PDF examination.

Modern Office ZIP/XML inspection primarily uses Python's standard library. Some checks may be reduced if optional packages are missing.

## Installation

Download or clone the repository, then run the script with Python. The following examples assume the repository is available locally.

### Debian 13 / Linux

Install Python and optional analysis libraries using Debian packages:

```bash
sudo apt update
sudo apt install python3 python3-olefile python3-pypdf git
```

Clone and enter the repository:

```bash
git clone https://github.com/janipaivarinta/universal-document-forensics.git
cd universal-document-forensics
```

Check the command-line options:

```bash
python3 universal_document_forensics.py --help
```

### macOS

Install Python 3 if it is not already available (for example, from [python.org](https://www.python.org/downloads/macos/) or through Homebrew). Verify it:

```bash
python3 --version
```

Clone the repository and create an isolated Python environment:

```bash
git clone https://github.com/janipaivarinta/universal-document-forensics.git
cd universal-document-forensics
python3 -m venv .venv
source .venv/bin/activate
python -m pip install olefile pypdf
python universal_document_forensics.py --help
```

If Git is not installed, download the repository as an archive, extract it, and open Terminal in the extracted directory.

### Windows 10/11

Install a current Python 3 release from [python.org](https://www.python.org/downloads/windows/). Ensure the Python launcher or `python` command works in PowerShell. Git is optional if you download the repository as a ZIP archive.

In **PowerShell**, clone the repository (if Git is installed), then create a virtual environment:

```powershell
git clone https://github.com/janipaivarinta/universal-document-forensics.git
cd universal-document-forensics
py -3 -m venv .venv
.\.venv\Scripts\python.exe -m pip install olefile pypdf
.\.venv\Scripts\python.exe .\universal_document_forensics.py --help
```

Alternatively, download and extract the repository ZIP, then open PowerShell in that directory and run the commands starting with `py -3 -m venv .venv`.

Using the virtual environment's Python executable directly avoids changing PowerShell's script-execution policy.

## Usage

The examples below assume that the script accepts `--input-dir`, `--file`, and `--output-dir`. Check `--help` for the exact options in your copy.

### Analyze all supported documents in a directory

**Linux / macOS:**

```bash
cd ~/Desktop
python3 "/path/to/universal-document-forensics/universal_document_forensics.py" \
  --input-dir . \
  --output-dir ./forensics-reports
```

Replace `/path/to/universal-document-forensics/` with the actual installation path.

**Windows PowerShell** (example with the script in `C:\Tools\universal-document-forensics`):

```powershell
cd "$HOME\Desktop"
& "C:\Tools\universal-document-forensics\.venv\Scripts\python.exe" `
  "C:\Tools\universal-document-forensics\universal_document_forensics.py" `
  --input-dir . `
  --output-dir .\forensics-reports
```

### Analyze a single document

**Linux / macOS** (from the repository directory):

```bash
python3 universal_document_forensics.py \
  --file "assignment.docx" \
  --output-dir ./forensics-reports
```

**Windows PowerShell** (from the repository directory):

```powershell
.\.venv\Scripts\python.exe .\universal_document_forensics.py `
  --file "assignment.docx" `
  --output-dir .\forensics-reports
```

### Optional Linux/macOS shell alias

To invoke the script from any working directory, add an alias to your shell configuration (`~/.bashrc` for Bash or `~/.zshrc` for Zsh), using the real script path:

```bash
alias universal-document-forensics='python3 "/absolute/path/to/universal_document_forensics.py" --input-dir . --output-dir ./forensics-reports'
```

Reload the configuration (for Bash, `source ~/.bashrc`). Then run `universal-document-forensics` from the directory containing documents to inspect.

## Example report output

```text
forensics-reports/
├── assignment.docx_report.txt
├── spreadsheet.xlsx_report.txt
├── presentation.pptx_report.txt
└── document.pdf_report.txt
```

Depending on the file format and available metadata, reports may include:

- File identification and SHA-256 hash
- Container and structural integrity checks
- Document structure and available metadata
- Software and AI-related identifiers or markers
- Noteworthy observations, warnings, and contextual interpretation
- A neutral summary of what the available evidence does—and does not—support

Report filenames and sections should be checked against the current script implementation.

## Interpretation and academic integrity

**This is a technical examination tool, not an AI detector or an automatic misconduct decision system.**

An application identifier, unusual metadata, missing RSIDs, or a programmatically generated structure can have many explanations, including legitimate exports, conversions, templates, accessibility tools, or document processing software. A document may also have been copied into another editor and saved again, altering or replacing earlier metadata.

Reports should describe observable facts, clearly distinguish observations from hypotheses, and avoid asserting that an individual used AI or violated academic rules without independent supporting evidence. Institutional review procedures and opportunities for the document author to explain findings remain essential.

## Privacy and file handling

- The tool is designed for **local processing**; no document upload to an external service is required.
- Original documents are **not modified** by the analysis.
- Generated reports may contain sensitive metadata, document content excerpts, filenames, and other identifiers. Store and share reports according to your organization's data-protection requirements.
- SHA-256 hashes can help identify the examined file, but a hash alone does not establish authorship or provenance.

## Limitations and validation

- Legacy `.doc`, `.xls`, and `.ppt` files use binary OLE structures. Inspection of their containers and properties does **not** reconstruct full document contents or editing histories.
- PDF analysis depends on accessible structure and metadata. PDF producer/creator fields are not proof of the editing workflow or author.
- Encrypted, damaged, malformed, or unusual documents may produce partial results or errors.
- Metadata may be missing, inaccurate, modified, or rewritten by later software.
- An initial basic test reportedly completed across all seven listed extensions, using synthetic Office containers and a generated PDF. This is **not comprehensive validation** with real-world legacy files, encrypted files, or malformed documents.

## AI transparency

This project was developed with assistance from OpenAI ChatGPT (GPT-6). AI assistance was used in drafting and refining code and documentation; this disclosure does not imply that every line was generated by AI or that AI output was independently verified. See [AI-TRANSPARENCY.md](AI-TRANSPARENCY.md) for the scope, limitations, and responsibility statement.

## Citation

If you use Universal Document Forensics in research,
teaching, or academic work, please cite the software.

Citation metadata is available in [CITATION.cff](CITATION.cff).

**Author:** Jani Päivärinta  
**Software:** Universal Document Forensics  
**Version:** 1.0  
**Year:** 2026  
**License:** MIT

## License

Copyright (c) 2026 Jani Päivärinta. Licensed under the [MIT License](LICENSE). The license applies to this project's original code and documentation, not to separately licensed third-party dependencies.
