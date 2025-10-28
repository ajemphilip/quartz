

# Moo Moo 🐄  
*A Research-Creation Project in DIY Assistive Storytelling*

Moo Moo is a research-creation exploration into how **refreshable tactile literacy tools** can be reimagined beyond clinical interfaces — toward playfulness, agency, and **self-facilitated story experience**.  
It combines **Braille pin actuation**, **voice interaction**, and **AI-generated storytelling** in a fully DIY, open-source form.

This project extends questions raised in my Major Research Project at York University:  
*How can a child’s tactile reading device become a **collaborative character** — one that listens, responds, surprises, and learns alongside them?*

---

## Project Motivation

- Only a small fraction of children who could benefit from Braille are introduced to it early.
- Refreshable Braille displays remain **expensive** and not widely available for children.
- Traditional literacy tools sometimes feel **instructional-first**, not *joy-first*.

Moo Moo takes a different stance:  
Instead of proving *competence*, kids get to **shape** the experience through imagination and touch.

---

## Concept Overview

**Interaction Loop**
1. Child speaks a prompt  
2. Speech-to-text interprets the theme  
3. A story is generated in response  
4. Device chooses a key word → displays it in **Braille**  
5. Child spells using tactile input  
6. If correct → story continues with new details  
7. If not → hints are offered through touch + voice  

Behavior frames literacy as a **collaborative game** with a friendly character.

---

## Research Questions

- What **material qualities** of Braille — size, movement, texture — support early learners best?
- How do **playful identities** shift a child’s relationship to assistive tech?
- Can DIY fabrication reduce **cost, fragility, and intimidation** in tactile literacy tools?
- What does **co-making** with children reveal about design justice in educational AT?

---

## Design Principles (from MRP)

- **Make learning feel like play**  
  Humorous, comforting identity (Moo Moo!)
- **Encourage agency**  
  Kids direct the narrative through voice + touch
- **Open the box**  
  Designs can be repaired, modified, expanded locally
- **Accessible materiality**  
  Iterative 3D printing to tune textures, friction, height, and movement
- **Low-barrier distribution**  
  Components affordable + globally available

---

## System Architecture

**Core Components**
- Raspberry Pi Zero 2 W — logic + audio processing
- ESP32-S3 — pin motor control + real-time feedback
- Motorized **Braille pins** — modular, swappable units
- Capacitive or button-based spelling interface
- Whisper + GPT + TTS pipeline for voice + story

The device is built to evolve as fabrication methods improve.

---

## Prototyping Focus Areas

- **Linear pin reliability**  
  Thread friction, clearances, speed, noise
- **Case ergonomics**  
  Comfortable grip + friendly form language (character vibes)
- **Real-time feedback**  
  Detecting correct letters through tactile response
- **Durability**  
  Classroom-safe and parent-repairable

Each iteration is **documented**, not discarded — building a **knowledge path** others can follow.

---

## Research Context & Impact

Moo Moo aligns with:
- **Design Justice** (Costanza-Chock)  
  Tools shaped *with* communities, not *for* them
- **Techno-ableism critiques** (Shew)  
  Avoiding narratives of “fixing” bodies
- **DIY Assistive Tech** (Hurst & Kane)  
  Empowering non-experts to drive the creation of custom tools

The goal isn’t a polished consumer product —  
but a new **category** of assistive storytelling creature that invites partnership and delight.

---

## Where It’s Going

- Expanded pin arrays for full word display
- Configurable literacy modes (difficulty, pacing, hints)
- Co-design sessions with blind youth + educators
- Public documentation and open-source release

Moo Moo will continue learning **how to be a better friend to early Braille readers** —  
one story prompt at a time.

---
