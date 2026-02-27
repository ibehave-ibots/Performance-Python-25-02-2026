# High-Performance Python for Scientific Computing

This three-day course provides a structured, measurement-driven approach to improving the performance of scientific Python code. Rather than relying on isolated tricks, we focus on understanding how time, memory, and data movement interact in real analytical workflows.

The aim is not simply to make code faster, but to help participants reason clearly about performance trade-offs and design decisions.

---

# Course Structure

The course progresses from measurement and diagnosis (Day 1), to compute acceleration (Day 2), to data storage and IO optimization (Day 3). Each session combines short conceptual input with practical experimentation.

---

# Logistics and Setup

To ensure a smooth workflow during the course, we standardize the development environment.

## Development Environment

| Tool    | Purpose                          | Notes                                                                    |
| ------- | -------------------------------- | ------------------------------------------------------------------------ |
| VS Code | Editor and execution environment | We will use VS Code throughout the course. Please install it in advance. |
| Git     | Version control                  | Used to receive updates and instructor demos.                            |
| Pixi    | Environment management           | Used to install and manage the Python environment for the course.        |

---

## Installing Pixi

Pixi should be installed **globally on your system**, not inside a virtual environment.  Installation instructions can be found here: https://pixi.prefix.dev/latest/reference/cli/pixi/install/

After installation, verify it works:

```bash
pixi --version
```

To install the course environment (from the project root directory):

```bash
pixi install
```

This will create the managed environment based on the provided configuration file.

To activate the environment:

```bash
pixi shell
```

Alternatively, VS Code can be configured to use the Pixi-managed interpreter directly.

---

## Getting Course Materials

All course materials are provided via Git.

To clone the repository initially:

```bash
git clone <repository-url>
cd <repository-folder>
```

Throughout the course, new materials, instructor demos and small updates will be added. To receive them:

```bash
git pull
```

Please pull updates regularly, especially at the start of each session.

---

## Workflow During the Course

* All exercises will be run inside VS Code.
* Notebooks and scripts are organized by day and session.
* Each notebook, instructor demos, and solutions will be available in new commits as the workshop progresses.
* Benchmark experiments should be run locally (unless working on GPU via Colab).

If you encounter environment or installation issues, we will resolve them early to avoid blocking progress later.

---

# Day 1 — Measurement and Diagnosis

The first day establishes a disciplined approach to performance analysis. We focus on profiling before modifying code.

| Session               | Focus                     | Description                                                                                                                                                     |
| --------------------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Course Overview       | Framing performance       | Clarifying what “performance” means in scientific computing and why intuition often fails.                                                                      |
| Measuring Wall Time   | Reliable benchmarking     | Using `time.perf_counter()` and `%timeit` to obtain stable measurements and interpret variability. Emphasis on scaling behavior rather than single data points. |
| Structural Scaling    | Growth patterns           | Investigating how runtime changes with problem size and how structural changes (e.g., preallocation, separating logic into functions) affect performance.       |
| What Python Executes  | Interpreter overhead      | Inspecting bytecode with `dis` to understand interpreter cost and Python–C boundaries.                                                                          |
| Stack Trace Profiling | Bottleneck identification | Using `cProfile`, `line_profiler`, and sampling profilers to identify which functions and lines dominate execution time.                                        |
| Memory in NumPy       | Allocation awareness      | Understanding views vs copies, dtype effects, temporaries, and in-place operations to reduce peak memory and hidden costs.                                      |

**Core principle:** Measure first, modify second.

---

# Day 2 — Compute Acceleration

On the second day, we examine how to reduce interpreter overhead, use parallelism appropriately, and leverage compiled acceleration.

| Session                         | Focus                  | Description                                                                                                                      |
| ------------------------------- | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| CPU vs Wall Time                | Working vs waiting     | Distinguishing CPU time from elapsed time and understanding IO and blocking behavior.                                            |
| Threads, Processes, and the GIL | Concurrency models     | Clarifying when threading helps, when multiprocessing is appropriate, and why mixing parallel systems often reduces performance. |
| Compiled Acceleration           | Reducing overhead      | Using `numexpr` and Numba to move computation into compiled code and avoid Python-external overhead.                             |
| Parallel Numba                  | Controlled parallelism | Introducing `@njit(parallel=True)` and `prange`, including diagnostics and practical limitations.                                |
| GPUs with CuPy & PyTorch        | Device acceleration    | Working with GPU arrays, understanding transfer costs, batching strategies, and kernel size considerations.                      |

**Core principle:** Acceleration requires structural clarity.

---

# Day 3 — Data on Disk and Analytical Workflows

The final day shifts attention to storage, IO, and computational planning.

| Session             | Focus                  | Description                                                                                                     |
| ------------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------- |
| IO vs Compute       | Utilization awareness  | Measuring CPU utilization while waiting on disk and distinguishing compute-bound from IO-bound workloads.       |
| NumPy Storage       | Format trade-offs      | Comparing `np.save`, compressed formats, and `np.memmap`, and evaluating compression vs throughput trade-offs.  |
| xarray              | Structured data access | Working with labeled datasets, partial reads from HDF5-based formats, and structured analysis.                  |
| Chunking Strategies | Planning computation   | Understanding lazy execution, chunk sizing, and how chunk structure affects rolling and aggregation operations. |

**Core principle:** Storage layout determines analytical speed.

---

# Learning Outcomes

By the end of the course, participants will be able to:

* Measure runtime and memory usage rigorously
* Interpret scaling behavior rather than isolated timings
* Identify true computational bottlenecks
* Reduce interpreter and allocation overhead
* Apply parallel and compiled acceleration appropriately
* Optimize data layout for analytical workflows

---

This course treats performance improvement as a structured, evidence-based process. Participants are encouraged to test assumptions, question results, and reason from measurement rather than intuition.
