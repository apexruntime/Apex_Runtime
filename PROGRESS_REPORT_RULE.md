# Apex Runtime — Contributor Progress & Reporting Rules

## 1. Purpose

The `PROGRESS_RULE.md` system exists to document the real work performed by every contributor.

Apex Runtime is intended to be an open-source and research-oriented project. Therefore, every meaningful contribution should be documented so that:

- Contributors receive proper credit.
- The team can track project progress.
- Professors and mentors can understand individual contributions.
- Future contributors can understand the project's development history.
- Progress can be converted into LinkedIn/project updates.
- Final contributor reports can be generated from documented work.
- Research decisions and experiments remain traceable.

> **If you worked on it, document it. If you claim it, show evidence.**

---

# 2. Every Contributor Should Maintain a Progress File

Each contributor should have their own progress file.

Recommended structure:

```text
progress/
├── README.md
├── contributor-name.md
├── contributor-name-2.md
├── contributor-name-3.md
└── ...
```

For example:

```text
progress/
├── ayush.md
├── rahul.md
├── ananya.md
└── rohan.md
```

The contributor's progress file should be updated regularly.

---

# 3. What Should Be Reported?

Contributors should document meaningful work such as:

- Features implemented
- Bugs fixed
- Research performed
- Experiments conducted
- Benchmarks
- Performance improvements
- Memory optimizations
- Documentation
- Architecture proposals
- Testing
- Code reviews
- Hardware testing
- Model experiments
- Research papers studied
- Technical discoveries
- Failed experiments
- Important decisions
- Problems encountered
- Solutions discovered

Do **not** report trivial activity simply to make the progress log longer.

For example:

### Not useful

```text
Changed a variable name.
Opened VS Code.
Worked on project for 2 hours.
```

### Useful

```text
Implemented the initial VRAM detection module and tested it
on an RTX 3050 6GB system.

Result:
Detected VRAM: 6144 MB
Detection accuracy: verified against nvidia-smi.
```

---

# 4. Progress Entry Format

Every progress entry should follow this format:

```markdown
## [DATE] — [SHORT TITLE]

### Objective

What were you trying to accomplish?

### Work Done

What did you actually implement, research, test, or investigate?

### Technical Details

Explain the important technical decisions.

### Result

What happened?

### Evidence

Provide relevant evidence such as:

- GitHub PR
- Commit
- Benchmark
- Screenshot
- Experiment results
- Research notes
- Documentation
- Demo

### Problems / Challenges

What problems did you encounter?

### Solution

How did you solve them?

### Next Step

What will you work on next?
```

---

# 5. Example Progress Entry

```markdown
## 2026-10-09 — Initial Hardware Profiler

### Objective

Create the first hardware profiling module for Apex Runtime.

### Work Done

Implemented initial detection for:

- CPU information
- System RAM
- GPU information
- GPU VRAM

### Technical Details

The profiler collects available hardware information before
the scheduler makes an inference decision.

This information will later be used by the runtime to determine
whether a model should run locally, use CPU/GPU offloading,
use memory paging, or fall back to cloud execution.

### Result

Successfully detected:

- CPU: AMD Ryzen 7
- RAM: 16 GB
- GPU: NVIDIA RTX 3050
- VRAM: 6 GB

### Evidence

PR: #12

Benchmark/Output:

```text
RAM: 16 GB
VRAM: 6 GB
GPU: RTX 3050
```

### Problems / Challenges

Different systems expose hardware information differently.

### Solution

Added hardware detection with fallback handling instead of
assuming a specific GPU configuration.

### Next Step

Begin the model memory estimation module.
```

---

# 6. Record Failed Experiments

Failure is part of research.

Contributors should **not hide failed experiments**.

A failed experiment can be extremely valuable if it explains what we learned.

Example:

```markdown
## 2026-10-12 — 7B Model on 4GB VRAM

### Objective

Attempt to run a 7B model entirely inside 4GB VRAM.

### Result

Failed.

The model exceeded available VRAM after accounting for
weights and runtime memory.

### Finding

Model weight size alone is not sufficient to determine
whether inference is possible.

Additional memory is required for runtime operations,
activations and KV cache.

### Next Step

Test CPU/GPU offloading.
```

This type of result is **valuable research**, not a failure to hide.

---

# 7. Progress Must Be Honest

Never exaggerate contributions.

Do not claim:

```text
Built the entire inference engine
```

when you actually:

```text
Implemented the memory estimation module.
```

Use precise language.

Good:

```text
Implemented
Tested
Investigated
Benchmarked
Proposed
Designed
Reviewed
Documented
Optimized
Discovered
```

Avoid vague claims such as:

```text
Worked on AI
Improved the project
Did optimization
Worked on backend
```

---

# 8. Evidence-Based Progress

Whenever possible, connect progress to an actual artifact.

Examples:

```text
Commit
Pull Request
Issue
Benchmark
Experiment
Research document
Architecture diagram
Demo
Test results
```

Example:

```markdown
Evidence:
- PR #24
- Benchmark: benchmarks/memory_test_01.json
- Documentation: docs/memory-estimation.md
```

This makes the contributor's work verifiable.

---

# 9. Weekly Progress Updates

Active contributors should preferably update their progress at least once per week.

Recommended format:

```markdown
# Weekly Progress — Week 2

## Completed

- Implemented hardware profiler
- Added RAM detection
- Added GPU VRAM detection
- Added basic tests

## Research

Studied:
- GPU memory allocation
- Model weight memory
- INT8 quantization

## Results

Hardware profiler successfully tested on two systems.

## Problems

CUDA detection failed on one system without the NVIDIA
driver installed.

## Next Week

- Fix fallback handling
- Start model memory estimator
- Add benchmark framework
```

The exact frequency can be adjusted depending on the contributor's role.

---

# 10. LinkedIn Progress Updates

Important contributor milestones may be converted into official Apex Runtime LinkedIn/project updates.

Examples of milestones:

- First successful prototype
- Major module completed
- Major optimization
- Important research finding
- Successful benchmark
- First model running
- Major contributor milestone
- Release
- Research publication
- Conference/hackathon milestone

### Important

LinkedIn posts must represent the contributor's **actual contribution**.

Do not exaggerate or misrepresent the work.

A contributor should be credited by name when appropriate.

---

# 11. LinkedIn Post Preparation

When a milestone is selected for a LinkedIn post, the project team may create a post using the contributor's documented progress.

The post should include:

### Problem

What problem were we solving?

### Contribution

What did the contributor actually work on?

### Technical Work

What technologies or concepts were involved?

### Result

What was achieved?

### Evidence

What measurable result or demonstration exists?

### Learning

What did we learn?

### Future Work

What comes next?

---

# 12. Example LinkedIn Contribution Post Structure

```text
🚀 Apex Runtime Progress Update

Today we are sharing the progress of [Contributor Name]
who worked on [Component].

Problem:
[Problem being solved]

Contribution:
[What the contributor implemented/researched]

Technical Work:
[Important technical details]

Result:
[Measured result]

What we learned:
[Important finding]

Next:
[Next milestone]

This work is part of Apex Runtime, an open-source project
focused on hardware-aware and memory-efficient AI inference.

Contributor:
[Name]

GitHub:
[Link]
```

The final post should be reviewed by the contributor before publication.

---

# 13. Contributor Approval

Before publishing a LinkedIn post that focuses on an individual contributor:

1. The contributor should be informed.
2. Their contribution should be represented accurately.
3. Technical claims should be verified.
4. The contributor should have an opportunity to correct factual mistakes.
5. No personal information should be published without permission.

The contributor may request corrections to inaccurate technical descriptions.

---

# 14. Final Contributor Report

At the end of a contributor's participation, they should prepare a final report.

Recommended file:

```text
reports/
├── contributor-name-final-report.md
├── contributor-name-final-report.pdf
└── ...
```

The final report should summarize the contributor's actual work.

---

# 15. Final Report Structure

```markdown
# Apex Runtime — Contributor Final Report

## Contributor

Name:

Role:

Contribution Period:

GitHub:

---

## 1. Overview

Briefly describe your involvement in Apex Runtime.

---

## 2. Responsibilities

What areas were you responsible for?

---

## 3. Work Completed

List the major contributions.

---

## 4. Technical Contributions

Explain the important technical work in detail.

---

## 5. Research / Experiments

Describe experiments performed and their results.

---

## 6. Benchmarks

Provide measurable results where applicable.

---

## 7. Problems Encountered

Describe significant technical challenges.

---

## 8. Solutions

Explain how those challenges were addressed.

---

## 9. Failed Experiments

Document important approaches that did not work
and what was learned from them.

---

## 10. Pull Requests / Commits

List important contributions.

---

## 11. Knowledge Gained

What technical concepts did you learn?

---

## 12. Collaboration

Describe collaboration with other contributors,
professors, mentors, or researchers.

---

## 13. Impact

Explain how your work contributed to Apex Runtime.

---

## 14. Future Work

What should be improved or researched next?

---

## 15. Conclusion

Summarize your overall contribution and experience.
```

---

# 16. Contribution Levels

Contributors should not be ranked only by the number of commits.

Contribution should be evaluated based on:

### Technical Impact

Did the work improve the project?

### Research Value

Did the work produce useful knowledge?

### Quality

Is the implementation reliable and maintainable?

### Documentation

Can others understand and reproduce the work?

### Collaboration

Did the contributor help other team members?

### Consistency

Did the contributor maintain meaningful progress?

### Evidence

Can the contribution be demonstrated?

---

# 17. Do Not Game the Progress System

Do not create meaningless commits or progress entries just to appear active.

Examples of bad practices:

```text
Changing formatting repeatedly
Creating unnecessary commits
Splitting one tiny change into many artificial contributions
Writing long progress reports with no actual work
Claiming other people's work
```

Quality matters more than quantity.

---

# 18. Credit and Attribution

Every meaningful contribution should be credited appropriately.

Depending on the contribution, credit may appear in:

- GitHub contributors
- README
- Release notes
- Research documentation
- LinkedIn posts
- Final project report
- Publications
- Presentations
- Project website

Contributors should not claim work performed by someone else.

---

# 19. Ownership of Contributions

A contributor's work should remain traceable.

Whenever possible, contributions should be connected to:

```text
Contributor
    ↓
Issue
    ↓
Implementation / Research
    ↓
Pull Request
    ↓
Review
    ↓
Merge
    ↓
Progress Entry
    ↓
Final Report
```

This creates a transparent project history.

---

# 20. Progress Is Part of the Project

Progress documentation is not bureaucracy.

It helps us understand:

```text
What we tried
      ↓
What worked
      ↓
What failed
      ↓
What we learned
      ↓
What changed
      ↓
What should happen next
```

This is especially important for a research-oriented project like Apex Runtime.

---

# 21. Golden Rule

> **Document real work, show evidence, give proper credit, and never exaggerate a contribution.**

Apex Runtime should be able to look back months or years later and answer:

> **Who worked on what, why did they do it, what happened, and what did we learn?**
```