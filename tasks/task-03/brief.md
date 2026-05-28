# Task 03 — Ghost System

## Briefing

> *"The ghost left something behind. It runs. It watches. It waits for the right word."*

You have recovered a binary from a compromised host. It appears to be a custom access 
tool left behind by the threat actor. Running it prompts for a passphrase.

Your job is to find the passphrase — and what lies behind it.

**[Ghost file](https://x509ghost.github.io/x509ghost-drop/declassified/ghost.exe)**

---

## Objectives

Reverse engineer the binary and extract the hidden flag.

**Flag format:** `GHOSTTASK3{...}`

---

## Hints

> *The first door is not the real door.*

> *The ghost speaks in code — not in words.*

> *To understand what something does, you must look at what it is made of.*

---

## Solve Path

This task has **three layers**. Each one must be peeled back to reach the next.

**Layer 1 — Identify what the binary is**
The file runs and prompts for a passphrase. Static analysis reveals no obvious strings.
Identify the runtime environment and extract the embedded source.

**Layer 2 — Read the source**
Decompile or disassemble the extracted bytecode. You will find multiple passwords.
Not all of them are real. The obvious ones are traps.

**Layer 3 — Find the hidden check**
The real password verification is not in the main code. It is hidden one layer deeper
inside a binary object embedded in the script. Disassemble it and reconstruct
what it is actually comparing against.

---

## Tools

| Tool | Purpose | Install |
|---|---|---|
| `pyinstxtractor` | Extract PyInstaller bundle | `pip install pyinstxtractor-ng` or standalone `.py` |
| `uncompyle6` | Decompile `.pyc` to Python source | `pip install uncompyle6` |
| `dis` (built-in) | Disassemble Python bytecode | No install needed |
| `strings` | Quick first look at binary | Built into Linux / Sysinternals on Windows |

**Tip:** If decompilers fail, the Python built-in `dis` module always works:
```
python -c "import dis,marshal; d=open('ghost.pyc','rb').read(); dis.dis(marshal.loads(d[16:]))"
```

---

## Scoring

| Criteria | Points |
|---|---|
| Flag submitted correctly | 100 pts |
| Methodology documented (tools used, steps taken) | +25 pts bonus |
| All three passwords identified (2 decoys + real) | +10 pts bonus |

**Max total: 135 pts**

---

*GHOST Exercise — Blue Team Challenge Series*
