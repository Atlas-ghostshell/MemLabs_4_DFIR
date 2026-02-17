## MemLabs Lab 4 — Obsession

Digital Forensics Case Study (Memory Forensics & NTFS Metadata)


---

## Overview

Lab Name: MemLabs Lab 4 – Obsession
Category: Memory Forensics / File System Forensics
Operating System: Windows 7 SP1 (x64)
Artifacts Available: Memory dump only
Objective: Recover a deleted but important file from memory

This lab simulates a post-compromise forensic investigation where an attacker deleted a sensitive file after exfiltration. The only remaining evidence was a volatile memory image.

The challenge tests the investigator’s understanding of Windows internals, specifically how NTFS stores file data, and whether deletion actually removes content from memory.


---

## Investigation Goals

Identify user activity and suspicious artifacts

Determine whether the deleted file can still be recovered

Recover the flag without relying on disk artifacts

Use memory-resident structures only



---

## Methodology & Workflow

1. System Profiling

Initial system analysis confirmed:

Windows 7 SP1 environment

Normal system behavior

No overt malicious processes


This ruled out traditional malware-centric approaches and shifted focus toward file system artifacts.


---

2. Artifact Discovery (Sticky Notes)

A Sticky Notes process was identified and analyzed:

Contained a message hinting that clipboard artifacts were a dead end

Served as an intentional nudge toward deeper forensic techniques


This was a decoy, not the solution.


---

3. File System Enumeration (MFT Analysis)

Using NTFS metadata analysis via Volatility:

A deleted file named Important.txt was identified

The file could not be dumped via standard dumpfiles

Strong indication that the file’s content was resident (stored entirely inside the MFT)


This is a known NTFS behavior for small files.


---

4. Resident Data Extraction (Key Breakthrough)

Instead of chasing file paths, the investigation pivoted to resident NTFS attributes:

Enumerated MFT entries inside memory

Identified the MFT record number associated with Important.txt

Extracted resident data directly from the MFT entry

Manually reconstructed the file content from hex data


## Critical Insight:

> Deleting a file does not necessarily remove its data — especially if it is resident within the MFT.




---

## Flag Recovery

The recovered resident data revealed the complete flag embedded within the deleted file.

> Flag intentionally omitted here
(CTF integrity preserved)




---

## Responsible Use of AI

AI was used as a controlled forensic assistant, not a decision-maker.

AI-assisted tasks:

Automating repetitive Volatility command execution

Helping triage large outputs

Validating hypotheses and artifact relevance


Human-controlled tasks:

Artifact selection

Forensic reasoning

Validation of findings

Final conclusions


This hybrid approach improved speed and accuracy without sacrificing forensic rigor.


---

## Key DFIR Lessons

Deleted files may persist via resident NTFS attributes

Memory forensics extends beyond processes and malware

NTFS metadata can outlive user actions

MFT analysis is critical in post-compromise scenarios

AI is most effective when used to assist, not replace, investigators



---

## Tools Used

Volatility 3

NTFS / MFT analysis plugins

Hex interpretation & manual reconstruction

AI-assisted command orchestration (supervised)



---

## Conclusion

Lab 4 was a textbook demonstration of why deep systems knowledge matters in DFIR.
The attacker assumed deletion was enough. NTFS disagreed.

This investigation reinforces a core DFIR truth:

> Data is stubborn.
Metadata remembers.
Memory tells the truth.




---

## Next: MemLabs Lab 5
Expect heavier artifacts, deeper pivots, a few hints.
🧠 Sharpen the forensic narrative even further.
