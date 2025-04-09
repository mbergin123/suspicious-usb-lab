
# 🔍 Suspicious USB Lab

This project documents my forensic analysis of a suspicious USB device as part of a Blue Team Labs Online challenge. Using REMnux and a set of open-source tools, I investigated the behavior of files within a USB dump and uncovered indicators of malicious activity.

---

## 🧪 Lab Setup

- **Environment**: REMnux running in VMware Workstation
- **Access Method**: SSH from Windows PowerShell into REMnux

---

## 🗂️ Investigation Steps

1. **Unzipped the downloaded USB archive**
   - Found a folder named `BLTO Suspicious USB` containing multiple files, including `README.pdf` and `autorun.inf`.

2. **Verified file contents**
   - Opened `BLTO.txt` to understand the lab scenario.
   - Created hashes for the files using hashing tools for integrity and malware analysis.

3. **File Type Identification**
   - Confirmed `README.pdf` is a valid PDF file using magic number analysis (referenced Gary Kessler's magic numbers list).
   - Inspected `autorun.inf`, which suggested that the USB would automatically launch the `README.pdf` upon insertion.

4. **PDF Behavior Analysis**
   - Used `peepdf` to explore the internals of the PDF.
   - Found `OpenAction` and `AA` (Additional Actions) objects triggering execution of JavaScript.
   - Interacted with Object `27` to analyze JavaScript code designed to export a data object.
   - Found that Object `28` launches `cmd.exe` and attempts to execute `README.pdf` from user directories (Desktop/Documents).

5. **Malware Detection**
   - Uploaded `README.pdf` hash to VirusTotal.
   - Confirmed the file is malicious and flagged by multiple antivirus engines.

---

## 🧠 Key Learnings

- How autorun files can be used to automatically execute files from USBs.
- How PDFs can embed JavaScript and launch OS-level commands.
- The importance of deep file analysis using tools like `peepdf` and `VirusTotal`.

---

## 🛠 Tools Used

- REMnux
- PowerShell
- `sha256sum`
- `file` and `cat`
- `peepdf`
- VirusTotal

---

## ✅ Outcome

I was able to:
- Analyze the suspicious USB files thoroughly.
- Identify and validate the embedded malware.
- Successfully complete all questions in the lab challenge.

---

📁 _This project was completed as part of Blue Team Labs Online training and is intended for educational and demonstrative purposes only._

