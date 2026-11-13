# Keylogger Study

A keylogger built as the final project for my cybersecurity course. The goal was to understand how this class of malware works end to end — capture, encryption, exfiltration — and how it is detected, so that it can be defended against.

> ⚠️ **For education and research only.** This code exists to study malware and its detection in a controlled setting. Running keylogging software on any device without the owner's explicit, informed consent is illegal and unethical. Do not deploy it outside an isolated lab you own.

## What it does

The project implements a keylogger and studies it from both the offensive and defensive sides:

- **Capture.** Collects keystrokes and other host signals (screenshots, webcam frames, browser history).
- **Packaging.** Compresses captured data into an archive and encrypts it at rest.
- **Exfiltration.** Sends the encrypted archive off the host over email (SMTP).
- **Recovery.** A companion decryption tool (`decrypt_file.py`) recovers the captured data on the receiving side, so the full round trip can be inspected.
- **Detection analysis.** The implementation notes (see the references in `keylogger.py`) study how antivirus engines flag this kind of program — signature matching and heuristic analysis — which informed how the behavior was structured and understood.

## Repository layout

| Path | What it is |
|---|---|
| `keylogger.py` | The main capture-and-exfiltration program |
| `setup.py` / `install.py` | Environment setup and dependency installation |
| `decrypt_file.py` | Decrypts the captured archive on the receiving side |
| `data-analysis/` | Scripts for analyzing the captured data |
| `image_www/`, `image_mysql/`, `docker-compose.yml` | A self-contained Docker lab (Elgg web app + MySQL) used to run and observe the project in isolation |
| `linux_packages.txt` | System packages the project depends on |

## Running it safely

This is meant to be run only inside an isolated, disposable environment that you own — for example a throwaway VM or the included Docker lab, with no access to anyone else's data or network. The Docker environment is brought up with:

```bash
docker compose up
```

## Course context

Final project for a cybersecurity course, written with classmates (A. Greenberg, N. Fu, J. Omolewa). It was an exercise in understanding offensive techniques well enough to recognize and defend against them.
