# Apex Runtime — Development & Code Rules

These rules exist to keep Apex Runtime **clean, understandable, efficient, research-oriented, and maintainable**.

The goal is not to produce the maximum amount of code. The goal is to produce **the right code, written properly**.

---

## 1. No AI-Generated Code by Default

- **Do not use AI-generated code for this project by default.**
- Contributors should understand the problem, design the solution, and write the implementation themselves.
- AI may be used for:
  - Learning concepts
  - Understanding documentation
  - Explaining errors
  - Discussing algorithms
  - Comparing possible approaches
  - Reviewing code
  - Finding bugs or potential issues
  - Understanding unfamiliar APIs
- AI should **not replace the contributor's understanding or implementation ability**.

### If AI-generated code is used

If a contributor uses AI-generated code for any reason:

1. They must understand every important part of the generated code.
2. The code must be reviewed manually.
3. The code must be adapted to Apex Runtime's architecture and coding standards.
4. Unnecessary code must be removed.
5. Performance must be considered.
6. Memory usage must be considered.
7. Naming and structure must match the rest of the project.
8. The contributor must be able to explain the implementation to another contributor or mentor.

**Never copy-paste AI-generated code blindly.**

---

# 2. No Unwanted Code

Every piece of code must have a purpose.

Do not add:

- Unused functions
- Unused variables
- Unused imports
- Duplicate implementations
- Dead code
- Debugging code
- Temporary hacks
- Unnecessary abstractions
- Unused dependencies
- Features that are not part of the current objective

Before creating a new file, function, class, or dependency, ask:

> **Do we actually need this?**

If the answer is no, don't add it.

---

# 3. Keep the Code Easy to Read

Apex Runtime is an open-source project.

Code should be understandable not only to the original author but also to:

- Students
- Contributors
- Professors
- Researchers
- Engineers
- Future maintainers

Prefer:

```text
clear code > clever code
simple design > unnecessary complexity
readability > short code
maintainability > quick hacks
```

Avoid writing code that is unnecessarily clever or difficult to understand.

---

# 4. Follow a Consistent Project Structure

Do not randomly create files or folders.

Follow the project's established architecture.

Before adding a new module:

1. Check whether an existing module already handles the responsibility.
2. Check the repository structure.
3. Follow existing naming conventions.
4. Discuss major architectural changes before implementing them.

A contributor should not introduce an entirely new architecture for a small feature.

---

# 5. One Responsibility Per Module

Each module should have a clear responsibility.

For example:

```text
hardware/
    profiler
    memory
    gpu

models/
    analyzer
    metadata
    estimator

runtime/
    scheduler
    executor
    memory_manager

optimization/
    quantization
    offloading
    paging
```

Avoid creating a giant file that contains everything.

Prefer small, logically separated components.

---

# 6. Avoid Premature Optimization

Optimization is important for Apex Runtime, but:

> **Do not optimize code before understanding the bottleneck.**

Before optimizing:

1. Measure the current performance.
2. Identify the bottleneck.
3. Explain why it is a bottleneck.
4. Implement the optimization.
5. Benchmark again.
6. Document the improvement.

Never claim:

> "This is faster."

without measurements.

Whenever practical, provide before/after benchmark results.

---

# 7. Memory Efficiency Is a First-Class Requirement

Apex Runtime is fundamentally a **memory-aware inference project**.

When writing code, consider:

- RAM usage
- VRAM usage
- CPU memory
- GPU memory
- Model memory
- KV-cache memory
- Temporary allocations
- Data copies
- CPU ↔ GPU transfers
- Disk I/O
- Memory fragmentation

Avoid unnecessary copies of large tensors or model data.

For large-model code, always ask:

> **How much memory does this operation require?**

---

# 8. Avoid Unnecessary Dependencies

Do not add a library simply because it makes a small task easier.

Before adding a dependency:

- Check whether the functionality already exists.
- Check whether the standard library can solve it.
- Check the dependency's license.
- Check its maintenance status.
- Consider its size and runtime overhead.
- Consider whether it is actually necessary.

Every dependency increases the project's maintenance and security surface.

---

# 9. Respect Existing Inference Engines

Apex Runtime should not reinvent existing systems unnecessarily.

When appropriate, investigate and build on established technologies such as:

- llama.cpp
- vLLM
- SGLang
- ONNX Runtime
- TensorRT-LLM
- Hugging Face tooling

Before implementing a low-level feature from scratch, ask:

> **Does an established project already solve this problem?**

If yes, understand it first and decide whether Apex should integrate, extend, wrap, or research a different approach.

---

# 10. Benchmark Everything Important

Performance claims must be backed by measurements.

Important metrics may include:

- Time to first token
- Tokens per second
- Peak RAM
- Peak VRAM
- Model loading time
- CPU utilization
- GPU utilization
- Memory transfer time
- KV-cache usage
- Energy consumption where measurable
- Cloud inference cost
- Quality degradation after optimization

Example:

```text
Model: 7B
Quantization: INT4
Hardware: RTX 3050 6GB

Baseline:
VRAM: 5.8 GB
Speed: 18 tok/s

Optimized:
VRAM: 3.9 GB
Speed: 21 tok/s
```

Do not invent benchmark results.

---

# 11. Document Experimental Results Honestly

Research code will sometimes fail.

That is completely acceptable.

Document:

- What was attempted
- Why it was attempted
- Hardware used
- Configuration
- Results
- Problems encountered
- What failed
- What was learned
- What should be tried next

A failed experiment is still valuable if it teaches us something.

---

# 12. Reproducibility

Whenever possible, experiments should be reproducible.

Document:

- Model
- Model version
- Quantization method
- Hardware
- Software versions
- Operating system
- Configuration
- Dataset, if applicable
- Benchmark procedure
- Random seeds where relevant

Another contributor should be able to understand how an experiment was performed.

---

# 13. No Fake Performance Claims

Never modify benchmarks to make Apex Runtime look better.

Do not:

- Hide failed tests
- Remove unfavorable results
- Cherry-pick only good benchmarks
- Compare unfair configurations
- Claim unsupported hardware compatibility
- Claim lossless compression when quality changed
- Claim a model can run in memory when it cannot

Apex Runtime values **scientific honesty over impressive numbers**.

---

# 14. Comments Should Explain "Why"

Do not write comments that simply repeat the code.

Bad:

```python
# Increment counter
counter += 1
```

Better:

```python
# Keep the most recently used layers resident to reduce
# repeated SSD-to-RAM transfers during inference.
```

Comments should explain:

- Why something is done
- Important constraints
- Non-obvious decisions
- Performance considerations
- Hardware limitations
- Research assumptions

---

# 15. Use Clear Naming

Names should communicate their purpose.

Prefer:

```text
memory_budget
available_vram
model_size
quantization_type
offload_layers
```

Avoid:

```text
x
tmp
abc
data2
thing
stuff
```

Short variable names are acceptable for very small local scopes where their meaning is obvious.

---

# 16. Keep Functions Focused

Avoid huge functions.

A function should generally perform one logical task.

Instead of:

```text
run_everything()
```

prefer:

```text
profile_hardware()
analyze_model()
estimate_memory()
select_strategy()
execute_inference()
collect_metrics()
```

This makes the runtime easier to test and understand.

---

# 17. Error Handling Must Be Meaningful

Do not silently ignore errors.

Bad:

```python
try:
    run_model()
except:
    pass
```

Errors should provide useful information.

Whenever possible, explain:

- What failed
- Why it may have failed
- What component caused it
- What the user can do next

---

# 18. No Hardcoded Hardware Assumptions

Apex Runtime is intended to work across different hardware configurations.

Avoid assumptions such as:

```text
GPU always exists
6 GB VRAM is always available
CPU always has 16 cores
RAM is always 32 GB
CUDA is always installed
```

Hardware should be detected dynamically whenever possible.

---

# 19. Configuration Over Hardcoding

Important runtime settings should be configurable.

For example:

```text
memory budget
VRAM limit
quantization mode
offloading strategy
context length
batch size
cloud fallback
model selection
```

Avoid scattering magic numbers throughout the codebase.

---

# 20. Security Matters

Apex Runtime may eventually execute models, download files, access hardware, communicate with APIs, and potentially interact with cloud infrastructure.

Therefore:

- Never commit API keys.
- Never commit passwords.
- Never commit tokens.
- Never commit private credentials.
- Validate external inputs.
- Be careful with downloaded model files.
- Review dependencies.
- Do not execute untrusted code automatically.
- Use environment variables for secrets.

Never commit:

```text
.env
API keys
private certificates
access tokens
credentials
```

---

# 21. Respect Licenses

Before using external:

- Models
- Datasets
- Libraries
- Code
- Benchmarks
- Research implementations

check their licenses and usage restrictions.

Always provide proper attribution where required.

Do not copy code from another project without understanding its license.

---

# 22. Keep Pull Requests Small and Understandable

Avoid submitting massive changes that modify unrelated parts of the project.

A good PR should clearly explain:

```text
What changed?
Why was it changed?
How was it tested?
What are the performance effects?
Are there any limitations?
```

Prefer:

```text
PR #21 — Add GPU memory profiler
```

over:

```text
PR #21 — Rewrite runtime + scheduler + UI + benchmark system
```

Small PRs are easier to review and merge.

---

# 23. Test Before Submitting

Before opening a pull request:

- Run the relevant tests.
- Run the project.
- Check for errors.
- Check memory usage when relevant.
- Check performance when relevant.
- Remove debug statements.
- Remove unused imports.
- Format the code.
- Update documentation if necessary.

Do not submit code that has not been tested.

---

# 24. Keep Documentation Updated

If a change affects:

- Architecture
- Installation
- API
- Configuration
- CLI commands
- Runtime behavior
- Benchmarks
- Research methodology

update the relevant documentation.

Documentation is part of the project, not an optional extra.

---

# 25. Explain Research Decisions

For research-oriented components, document the reasoning behind important decisions.

For example:

```text
Why INT4 instead of INT8?

Why this offloading strategy?

Why this scheduler?

Why this paging policy?

Why this cache policy?

Why was this model chosen?

What trade-off does this introduce?
```

The project should show not only **what we built**, but also **why we built it that way**.

---

# 26. Don't Hide Experimental Code

Experimental code is allowed, but it must be clearly separated from stable code.

Use appropriate labels such as:

```text
experimental/
research/
benchmarks/
prototypes/
```

Do not mix unfinished experimental implementations into production runtime code without explanation.

---

# 27. Backward Compatibility

When modifying an existing API or component:

- Check existing users of the component.
- Avoid breaking interfaces unnecessarily.
- Document breaking changes.
- Update tests and documentation.

If a breaking change is necessary, explain why.

---

# 28. No "Magic"

Avoid mysterious behavior.

The scheduler should be able to explain decisions such as:

```text
Selected CPU + GPU Offload

Reason:
VRAM available: 4.8 GB
Estimated model memory: 7.2 GB
RAM available: 18.4 GB
Network: Offline

Decision:
Move selected layers to CPU memory.
```

Whenever practical, Apex Runtime should be **observable and explainable**.

---

# 29. Prefer Measurable Decisions

Where possible, runtime decisions should be based on measurable information rather than arbitrary assumptions.

For example:

```text
hardware capacity
memory pressure
model requirements
latency target
quality target
network conditions
cloud cost
```

This is especially important for the scheduler.

---

# 30. Keep the Main Branch Stable

The main branch should represent a reasonably working version of the project.

Experimental or incomplete work should normally happen in feature branches.

Example:

```text
main
develop
feature/hardware-profiler
feature/quantization
feature/memory-paging
research/scheduler-v1
```

---

# 31. Commit Messages Should Be Meaningful

Avoid:

```text
update
changes
final
new code
fixed
```

Prefer:

```text
feat: add hardware memory profiler
fix: prevent unnecessary tensor copies
perf: reduce CPU-GPU transfer overhead
docs: add scheduler architecture
test: add memory estimator tests
```

---

# 32. Do Not Optimize for Lines of Code

A contributor is **not** judged by how much code they write.

A 100-line solution that solves the problem correctly is better than 1,000 lines of unnecessary code.

The goal is:

> **Minimum necessary complexity.**

---

# 33. Code Review Culture

Code review is not personal criticism.

Reviewers should focus on:

- Correctness
- Readability
- Architecture
- Performance
- Memory efficiency
- Security
- Maintainability
- Research validity

Contributors should be open to changing their implementation when a better approach is demonstrated.

---

# 34. Ask Before Major Architectural Changes

Before introducing a major change to:

- Runtime architecture
- Scheduler design
- Memory system
- Model format
- Dependency stack
- Public APIs
- Execution model

discuss the proposal with project maintainers.

For major research ideas, create a short proposal explaining:

```text
Problem
Current approach
Proposed approach
Expected benefit
Potential risks
How it will be measured
```

---

# 35. Learn Before Implementing

If you don't understand a component, don't blindly implement it.

For example, before modifying:

```text
KV cache
CUDA memory
quantization
GPU kernels
model loading
tensor operations
paging
scheduler
```

learn the underlying concept first.

**Understanding comes before implementation.**

---

# 36. The Golden Rule

Every contribution should satisfy these questions:

```text
1. Does it solve a real problem?
2. Is it actually needed?
3. Is it understandable?
4. Is it efficient?
5. Is it tested?
6. Is it documented?
7. Can another contributor maintain it?
8. Can I explain how it works?
9. Does it fit Apex Runtime's architecture?
10. Are the claims backed by evidence?
```

If the answer to several of these is **no**, the contribution probably needs more work.

---

# Apex Runtime Philosophy

We are not trying to build the biggest codebase.

We are trying to build a **serious, understandable, measurable, and useful AI inference runtime**.

### Our priorities

```text
Correctness
    ↓
Understanding
    ↓
Simplicity
    ↓
Maintainability
    ↓
Performance
    ↓
Optimization
```

And most importantly:

> **Write code that you understand, measure what you claim, and build only what is necessary.**

---

## Final Rule

### Don't write code just because you can.

### Write code because the project needs it.