# SGAI Massive p7m Extractor

Free extractor for digitally signed documents (`.p7m`) for Windows.

Copyright (C) 2023-2026 Filippo Forlani.  
Developed by Filippo Forlani with SGAI R&D Team - [www.sgai.net](https://www.sgai.net)

[Download SGAIMassivep7mExtractor.exe](dist/SGAIMassivep7mExtractor.exe)

Windows 7 / 10 / 11 - Freeware - No installation

---

Extracts in one go the original document (PDF, XML, Italian e-invoices, etc.) from one or more digitally signed `.p7m` files (CAdES), including whole folders with their subfolders.

- **A single `.exe` file**: no installation, no DLLs, no dependencies.
- **Drag & drop**: drop files or folders onto the icon and get the extracted documents.
- **Bulk processing**: handles whole folders, subfolders included.
- **Nested envelopes** (`doc.pdf.p7m.p7m`), DER/BER and Base64/PEM formats.
- **Byte-for-byte identical content** to the signed one: the document is not altered.
- **Privacy**: no registration, no Internet connection, no data collection.

## How to use

1. Download [SGAIMassivep7mExtractor.exe](dist/SGAIMassivep7mExtractor.exe).
2. Copy it to your **Desktop**.
3. Drag one or more `.p7m` files, or a folder, onto the SGAI icon.
4. Press **ENTER** to start the extraction.
5. Documents are extracted next to the originals; for a folder, into a `pdf\` subfolder (subfolders included).
6. At the end a **summary** is shown (files processed, extracted, skipped, errors with their reason, output folder); press **ENTER** to close.

Double-clicking the icon without files shows the help.

> **Windows SmartScreen warning.** On first launch Windows may show "Windows protected your PC", because the program is new and not yet code-signed. To continue: **More info -> Run anyway**. You can verify the file integrity with:
>
> ```powershell
> Get-FileHash SGAIMassivep7mExtractor.exe
> ```

### Right-click menu (optional)

```bat
SGAIMassivep7mExtractor.exe --register
```

adds "Extract with SGAI p7m Extractor" to the context menu of `.p7m` files and folders (current user only, no administrator rights needed). `--unregister` removes it. If you move the program, run `--register` again.

## Command line

```bat
SGAIMassivep7mExtractor.exe [options] <file.p7m | folder | mask> ...
```

Masks such as `*.p7m` or `C:\invoices\*.xml.p7m` are accepted.

| Option | Description |
|---|---|
| `-h`, `--help`, `/?` | show the help |
| `-V`, `--version` | show the version |
| `--license` | show the full licence and third-party components |
| `-o`, `--output DIR` | output folder (created if missing) |
| `-r`, `--recursive` | folders: include subfolders (default) |
| `--no-recursive` | folders: only files in the given folder |
| `-t`, `--keep-tree` | folders: recreate the subfolder structure (default: all files in a single folder) |
| `-s`, `--suffix TEXT` | append TEXT to every extracted file name (default: `_SGAI` on `.pdf` files only) |
| `--no-suffix` | no suffix: `doc.pdf.p7m` -> `doc.pdf` |
| `-x`, `--skip-existing` | do not overwrite existing files |
| `-n`, `--dry-run` | show what would be done without writing anything |
| `-q`, `--quiet` | show only errors and the summary |
| `--pause` | wait for ENTER before closing (default) |
| `--no-pause` | do not wait at the end (scripts/batch) |
| `--pause-on-error` | at the end, wait for ENTER only if there are errors |
| `--register` | add the entry to the context menu of `.p7m` files and folders and to "Open with" |
| `--register-default` | like `--register` and make it the default program for `.p7m` files (current user) |
| `--unregister` | remove the associations created |
| `--` | everything after this is a file, not an option |

**Examples**

```bat
SGAIMassivep7mExtractor.exe invoice.xml.p7m
SGAIMassivep7mExtractor.exe -o D:\extracted --no-suffix C:\mail\*.p7m
SGAIMassivep7mExtractor.exe -t -x --no-pause "C:\Signed archive"
```

**Exit codes:** `0` = ok, `1` = errors, `2` = wrong usage, `3` = no p7m files found.

## Important notes

- The program **extracts** the document but **does not validate** the digital signature or the certificate.
- The extracted file **has no legal value**: the original signed file prevails and must be kept.
- *Detached* signatures (`.p7m` files containing only the signature, not the document) are reported as errors.

## Privacy

No registration, activation or account required. The program **does not collect, store or send any data**: it never connects to the Internet, has no telemetry or usage statistics and keeps no logs. It only reads the files you give it and only writes the extracted documents; it changes the Windows registry (current user) only with `--register` / `--unregister`.

## Licence

**Freeware - Copyright (C) 2023-2026 Filippo Forlani. All rights reserved.**
Distributed by SGAI S.r.l. under licence from the author.

- Free to use, including professional use within companies and organisations.
- Redistribution allowed only free of charge, complete and unmodified, together with the licence.
- Selling, bundling in commercial products or services, modifying or decompiling it without the author's written permission is forbidden.
- Provided "as is", without warranty and without any liability of the author or the distributor for its use or results.
- The software is **not open source**: this repository publishes only the executable program.

The sole copyright owner is Filippo Forlani. SGAI S.r.l. distributes the program under its own name under licence from the author, without owning it. The name and brand "SGAI" belong to SGAI S.r.l.

Full text: [LICENSE.txt](LICENSE.txt) (also with `SGAIMassivep7mExtractor.exe --license`).

### Third-party components

- Built with **Embarcadero Delphi**; the parts of the Run-Time Library included in the executable are redistributed under the Embarcadero licence.

## Contact

Author: **Filippo Forlani** - filfor@gmail.com

For permissions, commercial licences or reports, please write to the author.
