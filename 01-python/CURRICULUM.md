# Python Curriculum — Topic Registry

> **This is the source of truth for the `01-python` learning track.**
> Each topic = one Jupyter notebook (concepts + worked examples) + one drill script (practicals).
> The plan lives here in the repo — not in any Claude session — so it's always available.

## How to Use in a New Session

1. Open a new Claude Code session in this repo
2. Say: **"I want to start topic N of the Python curriculum — read `01-python/CURRICULUM.md` first"**
3. Claude reads this file, finds the topic spec, and generates exactly that topic's notebook + drill script
4. When done, update the status column below and commit

---

## Progress Tracker

| # | Title | Folder | Status | Est. |
|---|-------|--------|--------|------|
| 0 | Environment Setup (WSL) | — | ⬜ Not Started | 30-45 min |
| 1 | Python Basics, Types, Control Flow | fundamentals/ | ⬜ Not Started | 2.5h |
| 2 | Data Structures | fundamentals/ | ⬜ Not Started | 2.5h |
| 3 | Functions, Decorators, Closures | fundamentals/ | ⬜ Not Started | 2.5h |
| 4 | Comprehensions, Generators, Iterators | fundamentals/ | ⬜ Not Started | 2h |
| 5 | Type Hints, Protocols, Dataclasses | best-practices/ | ⬜ Not Started | 2h |
| 6 | Testing with pytest | best-practices/ | ⬜ Not Started | 2.5h |
| 7 | Logging and Observability | best-practices/ | ⬜ Not Started | 1.5h |
| 8 | Environment Management and Packaging | best-practices/ | ⬜ Not Started | 1.5h |
| 9 | OOP for ML | patterns/ | ⬜ Not Started | 2.5h |
| 10 | Functional Patterns and Async | patterns/ | ⬜ Not Started | 2.5h |
| 11 | File Handling and Serialization | patterns/ | ⬜ Not Started | 2h |
| 12 | Memory Management: Copy vs View | patterns/ | ⬜ Not Started | 2.5h |
| 13 | Multiprocessing and Concurrency | patterns/ | ⬜ Not Started | 2.5h |
| 14 | Profiling and Performance | patterns/ | ⬜ Not Started | 2h |
| 15 | NumPy Essentials | numpy-pandas/ | ⬜ Not Started | 2.5h |
| 16 | Pandas for ML | numpy-pandas/ | ⬜ Not Started | 2.5h |
| C | Capstone: Mini ML Pipeline | capstone/ | ⬜ Not Started | — |

**Status key:** ⬜ Not Started · 🔄 In Progress · ✅ Done

---

## Topic Specifications

Full spec for each topic — what Claude generates when you say "start topic N".

---

### Topic 0 — Environment Setup (WSL Prerequisite)

**Output:** Working Python 3.11 venv + Jupyter + VSCode configured. No notebook or drill — pure setup.

**Current environment state (WSL Ubuntu 20.04):**
- Python 3.8.10 installed (too old) — need 3.11+
- `uv` 0.10.9 already installed at `~/.local/bin/uv` — use this
- Jupyter not installed
- No project venv — system Python leaking (`$VIRTUAL_ENV=/usr`)
- VSCode Server running

**Steps:**

```bash
# 1. Install Python 3.11
uv python install 3.11
uv python list

# 2. Create project venv
cd ~/projects/ai-systems-engineering
uv venv .venv --python 3.11
source .venv/bin/activate
python --version   # must show 3.11.x

# 3. Install all learning dependencies
uv pip install \
  jupyter jupyterlab ipykernel \
  numpy pandas matplotlib \
  pytest pytest-cov \
  mypy \
  pyyaml python-dotenv \
  joblib \
  httpx \
  line-profiler memory-profiler \
  python-json-logger \
  rich

# 4. Register Jupyter kernel
python -m ipykernel install --user --name ai-systems --display-name "AI Systems (Python 3.11)"
jupyter kernelspec list

# 5. Smoke test
python -c "import numpy, pandas, pytest; print('All good')"
```

**VSCode extensions to install (manual):**
- Python (`ms-python.python`)
- Jupyter (`ms-toolsai.jupyter`)
- Pylance (`ms-python.vscode-pylance`)
- Ruff (`charliermarsh.ruff`)

**`.vscode/settings.json` to create:**
```json
{
  "python.defaultInterpreterPath": "${workspaceFolder}/.venv/bin/python",
  "python.terminal.activateEnvironment": true,
  "editor.formatOnSave": true,
  "[python]": {
    "editor.defaultFormatter": "charliermarsh.ruff"
  }
}
```

**Done when:** `python --version` shows 3.11.x, `import numpy, pandas` works, VSCode shows "AI Systems (Python 3.11)" kernel.

---

### Topic 1 — Python Basics, Types, Control Flow, Error Handling

**Files:**
- `01-python/fundamentals/01-python-basics.ipynb`
- `01-python/fundamentals/01-python-basics-drills.py`

**Notebook sections:**
1. The execution model — interpreter, REPL, scripts vs notebooks. What happens when you `import`.
2. Types — `int`, `float`, `bool`, `str`, `None`, `bytes`. "Everything is an object." `id()`, `type()`, `isinstance()`.
3. String operations — f-strings with format specs (`:02d`, `:.4f`, `!r`), slicing, common methods. ML training logs live in strings.
4. Variables and mutability — why `a = b` doesn't copy. Shared references and when it bites you.
5. Control flow — `for`, `while`, `if/elif/else`, `break/continue/else` on loops (yes, loops have `else`).
6. Functions — `def`, `return`, default args, `*args`, `**kwargs`. Why `**kwargs` is everywhere in PyTorch.
7. Error handling — `try/except/else/finally`, exception hierarchy, `raise`, custom exceptions. GPU OOM pattern.
8. Modules — `import`, `from x import y`, `__name__ == "__main__"` guard.

**Drill script exercises:**
- Format a training log string with epoch/loss/acc using f-string format specs
- `merge_config(defaults, overrides)` — returns merged dict, no mutation of inputs
- Extract model names from a list of file paths (string methods + filtering)
- Retry wrapper using `try/except` with backoff — test with a flaky function
- Module with `main()` + `__name__` guard — can be imported or run directly

**Analogy anchors:** dynamic typing → K8s pod spec CPU as `"500m"` or `0.5` · `**kwargs` → variadic Helm values · `try/except` → pod restart policy with backoff

**ML forward connections:** f-strings for training loop logging · `**kwargs` in `model = MyModel(**config)` · `try/except` for GPU OOM · `__name__` guard in training scripts

---

### Topic 2 — Data Structures: List, Dict, Set, Tuple, Collections

**Files:**
- `01-python/fundamentals/02-data-structures.ipynb`
- `01-python/fundamentals/02-data-structures-drills.py`

**Notebook sections:**
1. `list` — O(1) append/index, O(n) insert/search. Slicing creates copies (memory cost). `sort` vs `sorted`.
2. `tuple` — immutable list. Multi-return, dict keys, fixed records.
3. `dict` — hash map, O(1) lookup, ordered (3.7+). `.get()`, `.setdefault()`, comprehensions, `{**a, **b}`, `|=`.
4. `set` — O(1) membership, dedup, intersection/union/difference.
5. `collections` — `defaultdict`, `Counter`, `deque(maxlen)`, `namedtuple`.
6. Performance intuition — `sys.getsizeof`, `timeit`, list vs set membership benchmark.
7. Nested structures — configs, JSON-like data, safe deep access.

**Drill script exercises:**
- Class label distribution with `Counter` — identify imbalanced classes
- Group samples by label with `defaultdict(list)`
- Sliding window over a data stream with `deque(maxlen=N)`
- Deep-merge two nested config dicts
- Benchmark list vs set membership for 100k items — print speedup factor

**Analogy anchors:** `dict` → K8s ConfigMap · `set` → IP allowlist · `deque(maxlen)` → ring buffer / circular log · `Counter` → Prometheus metric aggregation

**ML forward connections:** model configs as dicts · `Counter` for class imbalance · `defaultdict` for dataset splits · `deque` for sliding window training metrics

---

### Topic 3 — Functions, Decorators, Closures

**Files:**
- `01-python/fundamentals/03-functions-decorators-closures.ipynb`
- `01-python/fundamentals/03-functions-decorators-closures-drills.py`

**Notebook sections:**
1. First-class functions — functions as values, passing as arguments, storing in dicts.
2. Closures — inner functions capturing outer scope. Late binding gotcha.
3. Decorators — `@` syntax unwrapped. `functools.wraps`. Why metadata preservation matters.
4. Decorator factories — decorators that take arguments (`@retry(max_attempts=3)`).
5. `functools.lru_cache` / `@cache` — memoization. Cache info, invalidation.
6. `functools.partial` — pre-configured function factory.
7. `functools.reduce` — fold operations.

**Drill script exercises:**
- `@timer` decorator — measure elapsed time on a simulated training step
- `@retry(max_attempts, delay)` factory — test with a function that fails N-1 times
- `make_scaler(mean, std)` closure — returns scale function with baked-in stats
- `@lru_cache` tokenizer — show cache hit vs miss via `cache_info()`
- `functools.partial` to pre-configure a preprocessing function

**Analogy anchors:** decorator → K8s admission webhook · closure → Lambda with baked-in env vars · `lru_cache` → Redis cache in front of a DB · `partial` → pre-baked Helm values

**ML forward connections:** `@torch.no_grad()` is a decorator · `@property` in `nn.Module` · retry for flaky inference API calls · timing for profiling training steps

---

### Topic 4 — Comprehensions, Generators, Iterators

**Files:**
- `01-python/fundamentals/04-comprehensions-generators-iterators.ipynb`
- `01-python/fundamentals/04-comprehensions-generators-iterators-drills.py`

**Notebook sections:**
1. List/dict/set comprehensions — syntax, conditions, nested. Speed vs readability.
2. Generator expressions — lazy, one-pass, O(1) memory. `sys.getsizeof` comparison.
3. `yield` — generator functions. Resumable execution. Sending values in.
4. Iterator protocol — `__iter__`, `__next__`, `StopIteration`. What `for` actually does.
5. `itertools` — `islice`, `chain`, `cycle`, `takewhile`, `groupby`, `product`. ML use cases.
6. Memory trade-off — list vs generator for 1M items. When you must materialize.

**Drill script exercises:**
- `stream_batches(dataset, batch_size)` — yields `(X_batch, y_batch)`, never loads full dataset
- Infinite augmentation generator — wraps dataset with `cycle`, yields augmented samples
- Generator pipeline: `load → filter → augment → batch` chained together
- `take(n, iterable)` using `itertools.islice`
- Benchmark list comprehension vs generator expression for a large transform

**Analogy anchors:** generator → Kafka consumer, one record at a time · `itertools.chain` → Unix pipe · iterator protocol → K8s list-watch API

**ML forward connections:** PyTorch `DataLoader` is a generator · HuggingFace streaming datasets · `itertools.chain` for combining train + synthetic data

---

### Topic 5 — Type Hints, Protocols, Dataclasses

**Files:**
- `01-python/best-practices/05-type-hints-protocols-dataclasses.ipynb`
- `01-python/best-practices/05-type-hints-protocols-dataclasses-drills.py`

**Notebook sections:**
1. Why type hints — documentation, IDE autocomplete, `mypy`. Optional at runtime, mandatory for maintainability.
2. Basic annotations — `int`, `str`, `list[str]`, `dict[str, int]`, `T | None` (3.10+), `Optional[T]`, `Union`.
3. `typing` deep dive — `Callable`, `TypeVar`, `Generic`, `Final`, `Literal`, `TypeAlias`.
4. `dataclass` — auto `__init__`, `__repr__`, `__eq__`. `field()`, `default_factory`. `frozen=True`. `__post_init__`.
5. `Protocol` — structural typing. "If it has `.predict()` and `.fit()`, it's a model." No inheritance required.
6. `TypedDict` — typed dict for JSON payloads and config objects.
7. `from __future__ import annotations` — forward references, performance.

**Drill script exercises:**
- `TrainingConfig` dataclass with nested `OptimizerConfig` — frozen, validation in `__post_init__`
- `Predictor` Protocol — two model classes satisfying it without inheriting, typed `evaluate(model: Predictor, ...)`
- Function accepting `str | Path`, returning typed config dict
- Annotate an untyped training script, run `mypy`, fix errors

**Analogy anchors:** type hints → OpenAPI schema · `Protocol` → K8s duck typing · `dataclass` → protobuf message · `TypedDict` → JSON Schema

**ML forward connections:** HuggingFace `TrainingArguments` is a `dataclass` · PyTorch modules typed with Protocols · `TypedDict` for FastAPI request/response shapes

---

### Topic 6 — Testing with pytest

**Files:**
- `01-python/best-practices/06-testing-with-pytest.ipynb`
- `01-python/best-practices/06-testing-with-pytest-drills.py`

**Notebook sections:**
1. Why test ML code — models degrade silently; tests catch data pipeline bugs, not model quality bugs.
2. pytest basics — `test_` convention, `assert`, `-v`, `-k`, `-x`.
3. Fixtures — `@pytest.fixture`, scope (function/module/session), `conftest.py`.
4. Parametrize — `@pytest.mark.parametrize` for multiple inputs. Essential for data transforms.
5. Mocking — `unittest.mock.patch`, `MagicMock`. Mocking API calls, file I/O, GPU ops.
6. Testing data pipelines — shape assertions, dtype checks, value range checks.
7. Testing model interfaces — test Protocol satisfaction, not specific output values.
8. `pytest-cov` — coverage reports. What 80% coverage means and what it misses.

**Drill script exercises:**
- Tests for `merge_config()` from Topic 1 — edge cases (empty, None, nested)
- Fixture building a synthetic `TabularDataset` — reused across multiple tests
- Parametrized test for normalization across multiple dtypes
- Mock an API call — verify retry logic fires without hitting the network
- Shape + dtype "smoke tests" for a preprocessing pipeline

**Analogy anchors:** fixtures → K8s namespace setup/teardown · mocking → wiremock stub · `conftest.py` → shared test infra as code

**ML forward connections:** testing DataLoader output shapes · testing tokenizer output · nn.Module forward() shape tests — catches silent data bugs before training

---

### Topic 7 — Logging and Observability

**Files:**
- `01-python/best-practices/07-logging-and-observability.ipynb`
- `01-python/best-practices/07-logging-and-observability-drills.py`

**Notebook sections:**
1. `print` vs `logging` — why `print` is a liability in production ML code.
2. Logger hierarchy — `DEBUG/INFO/WARNING/ERROR/CRITICAL`. Names and propagation.
3. Configuring logging — `basicConfig`, `FileHandler`, `StreamHandler`, `Formatter`. JSON format.
4. Logger per module — `logger = logging.getLogger(__name__)` pattern.
5. Contextual logging — `extra` fields, `LoggerAdapter`, request IDs in inference servers.
6. Structured logging — `python-json-logger`, CloudWatch / Datadog ingestion.
7. Training loop observability — logging loss/metrics per step/epoch with configurable verbosity.

**Drill script exercises:**
- Replace `print()` calls in a training loop stub with proper logging at correct levels
- Logger writing INFO → stdout and ERROR → file simultaneously
- `TrainingLogger` class with `log_epoch`, `log_step`, `log_metric` emitting structured JSON
- Configure log level from `LOG_LEVEL` env var

**Analogy anchors:** logger hierarchy → DNS resolution chain · `FileHandler + StreamHandler` → sidecar log aggregator · structured JSON → OpenTelemetry span attributes

**ML forward connections:** training loop logging · inference server request logging · MLflow/W&B hooks sit on top of Python's `logging` module

---

### Topic 8 — Environment Management and Packaging

**Files:**
- `01-python/best-practices/08-env-and-packaging.ipynb`
- `01-python/best-practices/08-env-and-packaging-drills.py`

**Notebook sections:**
1. Why venvs — dependency isolation. "Works on my machine" in Python.
2. `venv` vs `conda` vs `uv` — when to use what.
3. `pip`, `requirements.txt`, `pyproject.toml` — the evolution. Why `pyproject.toml` is standard now.
4. `pyproject.toml` deep dive — `[project]`, `[dependencies]`, `[tool.pytest]`, `[tool.mypy]`.
5. Package structure — `src/` layout vs flat. `__init__.py`. What makes something importable.
6. `__init__.py` patterns — `__all__`, lazy imports, clean public API.
7. Editable installs — `pip install -e .`. Shared utilities in ML monorepos.
8. `python-dotenv` — never hardcode API keys.

**Drill script exercises:**
- `pyproject.toml` for a hypothetical `ml-pipeline` package
- `src/` layout with two importable modules, editable install, verify imports
- Load config from `.env` with `python-dotenv`, fall back to defaults
- `__init__.py` exposing clean public API, hiding internals

**Analogy anchors:** `venv` → Docker container for deps · `pyproject.toml` → Helm `values.yaml` + `Chart.yaml` · editable install → volume mount vs baked image · `__all__` → K8s RBAC

**ML forward connections:** every ML project needs a package structure · HuggingFace / LangChain are pip packages · required before publishing your own tools

---

### Topic 9 — OOP for ML

**Files:**
- `01-python/patterns/09-oop-for-ml.ipynb`
- `01-python/patterns/09-oop-for-ml-drills.py`

**Notebook sections:**
1. Classes — `__init__`, instance vs class variables, `self`. Blueprint vs instance.
2. Dunder methods — `__repr__`, `__str__`, `__len__`, `__getitem__`, `__iter__`, `__contains__`, `__eq__`, `__hash__`.
3. `__call__` — making objects callable. How `model(x)` works in PyTorch. Deep dive.
4. Properties — `@property`, `@setter`. Controlled access, lazy initialization.
5. Inheritance and `super()` — MRO, extending without breaking.
6. Abstract base classes — `ABC`, `@abstractmethod`. Required interfaces.
7. Context managers — `__enter__`, `__exit__`, `contextlib.contextmanager`. Resource lifecycle.
8. `@classmethod` as alternative constructors — common in ML config loaders. `@staticmethod`.
9. `__slots__` — memory optimization for objects created millions of times.

**Drill script exercises:**
- `TabularDataset` with `__len__`, `__getitem__`, `__iter__`, `__repr__` — matches PyTorch Dataset API
- `Scaler` with `fit()` and `__call__()` — callable transformer
- `BaseTransform` ABC + two concrete implementations
- Context manager for timing: `with timer("forward pass"): ...`
- `ModelConfig` with `@classmethod from_yaml(path)` alternative constructor

**Analogy anchors:** `__call__` → K8s controller reconcile loop · context manager → AWS SDK session context · ABC → CRD validation schema · `@classmethod` → factory/builder pattern

**ML forward connections:** every `nn.Module` uses `__call__` via `forward()` · Dataset requires `__len__` + `__getitem__` · `torch.no_grad()` is a context manager · `__slots__` for memory-efficient sample objects

---

### Topic 10 — Functional Patterns and Async

**Files:**
- `01-python/patterns/10-functional-and-async-patterns.ipynb`
- `01-python/patterns/10-functional-and-async-patterns-drills.py`

**Notebook sections:**
1. Pure functions and side effects — why ML training benefits from referential transparency.
2. `map`, `filter`, `reduce` — and when comprehensions win.
3. `functools.partial` — partial application for pipeline construction.
4. Function composition — transform pipelines without classes.
5. `asyncio` fundamentals — event loop, `async def`, `await`, `asyncio.run()`.
6. `asyncio.gather()` — fan-out: parallel API calls, parallel embedding generation.
7. `async for` and async generators — streaming LLM responses token by token.
8. `asyncio` vs `threading` vs `multiprocessing` — decision matrix for ML.
9. `httpx` — async HTTP for model API calls at scale.

**Drill script exercises:**
- Async batch embedding: `embed_batch(texts)` using `asyncio.gather()` with a fake async API
- Async LLM streaming: `async for token in stream_response(prompt)`
- Preprocessing pipeline via `functools.partial` + function composition (no classes)
- Benchmark sequential vs `asyncio.gather()` for 20 fake API calls — show wallclock diff
- `async def predict(request)` FastAPI-style stub with `await model.ainfer()`

**Analogy anchors:** `asyncio` → Node.js event loop · `asyncio.gather()` → parallel K8s pod creation · `async for` → chunked HTTP streaming · `partial` → pre-configured Helm release

**ML forward connections:** FastAPI `async def` handlers · HuggingFace `AsyncInferenceClient` · LangChain streaming · parallel embedding generation in RAG pipelines

---

### Topic 11 — File Handling and Serialization

**Files:**
- `01-python/patterns/11-file-handling-and-serialization.ipynb`
- `01-python/patterns/11-file-handling-and-serialization-drills.py`

**Notebook sections:**
1. `pathlib.Path` — `read_text()`, `iterdir()`, `glob()`, `mkdir(parents=True)`. Why `os.path` is legacy.
2. File I/O modes — text vs binary, encoding, context managers.
3. JSON — `json.load/dump`, custom encoders for NumPy types (the #1 ML gotcha), streaming large JSON.
4. YAML — `pyyaml`. Loading model configs. Safe load vs unsafe load.
5. CSV — `csv` module vs Pandas. When to use which.
6. Pickle — speed, danger, when ML uses it anyway.
7. `joblib` — ML-specific serialization. Parallel pickling. Why sklearn uses it.
8. Protocol Buffers / MessagePack — brief intro for model serving at scale.

**Drill script exercises:**
- Load a YAML config, validate required keys, save modified version back
- Serialize a dict with NumPy arrays to JSON — handle `TypeError: ndarray not serializable`
- Scan directory tree for all `.pt` checkpoints using `pathlib.glob()`
- Save/load sklearn-style model with `joblib` — measure size vs pickle
- Atomic checkpoint saver: write to temp file, rename (blue-green swap)

**Analogy anchors:** `pathlib` → fluent K8s API client · atomic write → blue-green deploy · `joblib` → cacheable container image layers · pickle danger → `eval()` injection

**ML forward connections:** YAML for model configs · `torch.save` uses pickle · the NumPy JSON bug hits everyone in their first ML project

---

### Topic 12 — Memory Management: Copy vs View *(HIGH priority for ML)*

**Files:**
- `01-python/patterns/12-memory-copy-vs-view.ipynb`
- `01-python/patterns/12-memory-copy-vs-view-drills.py`

**Notebook sections:**
1. Python memory model — reference counting, `id()`, "box vs label" mental model.
2. Mutable vs immutable — why `list` mutates, why `str`/`tuple`/`int` don't.
3. Shallow vs deep copy — `copy.copy()` vs `copy.deepcopy()`. The nested structure trap.
4. NumPy views vs copies — **slicing returns a view** (same memory). `np.copy()` for a real copy. The #1 silent bug.
5. Strides — memory layout. `arr.strides`, `np.ascontiguousarray()`. Why transpose is free but can hurt performance.
6. Memory-efficient ops — in-place (`+=`, `np.add(a, b, out=a)`), avoiding intermediate allocations.
7. `tracemalloc` — finding where allocations happen.
8. Garbage collector — `gc`, reference cycles, `weakref`. Large ML object graphs.

**Drill script exercises:**
- View mutation trap: modify a NumPy slice, show the original changed
- `safe_normalize(arr)` — copies before modifying, verifies original unchanged
- Memory comparison: 1000 separate arrays vs one reused pre-allocated array with in-place ops
- `tracemalloc` to find top 3 allocations in a data loading loop
- C-contiguous vs F-contiguous: measure performance difference on matrix ops

**Analogy anchors:** view vs copy → shared volume vs container image copy · strides → column-major vs row-major DB index · reference counting → K8s owner references · `tracemalloc` → JVM heap profiler

**ML forward connections:** #1 source of subtle dataset bugs · PyTorch `.detach()` / `.clone()` are the same concept · memory efficiency directly impacts training throughput

---

### Topic 13 — Multiprocessing and Concurrency *(HIGH priority for ML)*

**Files:**
- `01-python/patterns/13-multiprocessing-and-concurrency.ipynb`
- `01-python/patterns/13-multiprocessing-and-concurrency-drills.py`

**Notebook sections:**
1. The GIL — what it blocks (CPU-bound threads), what it doesn't (I/O). Why threading is still useful.
2. `threading` — `Thread`, `Lock`, `Event`, `Queue`. I/O-bound work, progress reporters.
3. `multiprocessing` — `Process`, `Pool`, `Queue`, shared memory. CPU-bound preprocessing.
4. `concurrent.futures` — `ThreadPoolExecutor`, `ProcessPoolExecutor`. The high-level API.
5. `Pool.map()` — parallel data transforms. DataLoader worker pattern.
6. Shared memory — `multiprocessing.shared_memory`. Share NumPy arrays across processes without pickling.
7. IPC — `Queue`, `Pipe`, `Manager`. Coordinating workers.
8. Decision matrix — `asyncio` for I/O · `multiprocessing` for CPU · `threading` for mixed.

**Drill script exercises:**
- Parallel image preprocessing: `ProcessPoolExecutor.map()` — compare sequential vs 4-worker wallclock
- Thread-safe metric accumulator with `threading.Lock` — concurrent updates from multiple workers
- Producer-consumer: one process generates batches, one preprocesses — connected by `Queue`
- Replicate PyTorch `num_workers`: pre-fetch batches in background while "GPU" computes
- `shared_memory` to share a large NumPy array across 4 workers without copying

**Analogy anchors:** GIL → single-threaded Redis · `ProcessPoolExecutor` → K8s Job with parallelism · `Queue` → SQS/RabbitMQ · `shared_memory` → shared PVC between pods

**ML forward connections:** PyTorch DataLoader `num_workers` uses `multiprocessing` internally · data preprocessing pipelines · distributed training foundations

---

### Topic 14 — Profiling and Performance *(HIGH priority for ML)*

**Files:**
- `01-python/patterns/14-profiling-and-performance.ipynb`
- `01-python/patterns/14-profiling-and-performance-drills.py`

**Notebook sections:**
1. Profiling mindset — measure first, optimize second. Premature optimization is costly in ML.
2. `timeit` — microbenchmarking fairly (warmup, iterations, cache effects).
3. `cProfile` + `pstats` — function-level profiling. `cumtime` vs `tottime`.
4. `line_profiler` — `@profile` for line-by-line. Where the hot loop actually is.
5. `memory_profiler` — line-by-line memory. Finding the allocation that doubles your RAM.
6. `py-spy` — sampling profiler, zero overhead, works on live processes.
7. NumPy performance — vectorization, `np.einsum`, broadcasting vs reshaping.
8. Bottleneck identification — 80/20 in ML pipelines: usually data loading, not model compute.

**Drill script exercises:**
- Profile a preprocessing function with `cProfile` — identify top 3 bottlenecks
- `line_profiler` on a batch assembly loop — find the hot line
- Benchmark 3 normalization implementations: Python loop vs comprehension vs NumPy
- `memory_profiler` on a data loading function — find the peak allocation
- Rewrite a loop-based feature extractor with NumPy vectorization — verify + measure speedup

**Analogy anchors:** `cProfile` → distributed tracing (find the slow span) · `line_profiler` → APM waterfall · `py-spy` → eBPF/perf sampling profiler · memory profiler → JVM heap dump

**ML forward connections:** training loop profiling · DataLoader bottleneck identification · inference latency profiling — "it's slow" → "line 47 in dataloader.py"

---

### Topic 15 — NumPy Essentials *(CRITICAL for ML)*

**Files:**
- `01-python/numpy-pandas/15-numpy-essentials.ipynb`
- `01-python/numpy-pandas/15-numpy-essentials-drills.py`

**Notebook sections:**
1. `ndarray` — shape, dtype, ndim, strides, itemsize, nbytes. C array under Python's hood.
2. Array creation — `zeros`, `ones`, `arange`, `linspace`, `eye`, `random.randn`, `random.randint`.
3. Dtype system — `float32` vs `float64`. GPU default vs CPU default. Why it matters for PyTorch.
4. Vectorized ops (ufuncs) — arithmetic, comparison, math. The 100x speedup over loops.
5. Broadcasting — shape alignment rules. `(100,4) - (4,)` works. `(100,4) - (100,)` doesn't. Why.
6. Indexing — basic, boolean masking, fancy indexing, `np.where`.
7. Key ops — `reshape`, `transpose`, `flatten`, `squeeze`, `expand_dims`, `stack`, `concatenate`, `split`.
8. Linear algebra — `np.dot`, `@` (`matmul`), `np.linalg.norm`, `np.linalg.svd`. Direct PyTorch analogs.
9. Aggregations — `sum`, `mean`, `std` with `axis`. The `keepdims` gotcha.
10. Reproducibility — `np.random.seed()`, `np.random.default_rng()`.

**Drill script exercises:**
- `(X - mean) / std` normalization without loops — verify against `sklearn.StandardScaler`
- Boolean mask: filter rows with any NaN feature, return clean array + removed count
- Batched matmul with `@`: shape `(B, M, K) @ (B, K, N)`
- Build a confusion matrix from `y_true`, `y_pred` using only NumPy
- Softmax from scratch — handle numerical stability via `x - max(x)`

**Analogy anchors:** `ndarray` → typed C byte buffer · broadcasting → K8s resource template over replica set · `axis` → SQL GROUP BY dimension · `@` → `torch.matmul`

**ML forward connections:** PyTorch tensors ARE NumPy arrays on GPU — same API · every preprocessing pipeline · scikit-learn takes NumPy input · the foundation everything else sits on

---

### Topic 16 — Pandas for ML *(HIGH priority for ML)*

**Files:**
- `01-python/numpy-pandas/16-pandas-for-ml.ipynb`
- `01-python/numpy-pandas/16-pandas-for-ml-drills.py`

**Notebook sections:**
1. `Series` vs `DataFrame` — labeled arrays. Index as primary key.
2. Loading — `read_csv`, `read_json`, `read_parquet`. Column dtypes on load.
3. Inspection — `head`, `info`, `describe`, `value_counts`, `shape`, `dtypes`.
4. Selection — `[]`, `.loc` (label), `.iloc` (position), boolean masking.
5. Missing data — `isnull()`, `fillna()`, `dropna()`, `interpolate()`. Strategy decisions.
6. Groupby + aggregation — `groupby`, `agg`, `transform`, `apply`.
7. Feature engineering — `apply`, `map`, `cut`/`qcut`, `get_dummies` for one-hot.
8. `merge` and `join` — SQL-style joins. Index alignment pitfall.
9. `DataFrame.to_numpy()` — handoff to sklearn/PyTorch. Dtypes must match.
10. Performance — `eval()`, `query()`. When to switch to Polars.

**Drill script exercises:**
- Full EDA: load CSV, print missing counts, class distribution, descriptive stats, correlation matrix
- Feature engineering pipeline: bin continuous var, one-hot categoricals, log-transform skewed features
- Groupby: per-class mean/std of all features, identify most discriminative feature
- Clean + left-join two DataFrames, handle nulls from merge
- Convert cleaned DataFrame to NumPy float32 array — assert dtypes correct

**Analogy anchors:** `DataFrame` → SQL table with in-memory query engine · `.loc` vs `.iloc` → K8s label selector vs pod index · `groupby` → SQL GROUP BY with window function · `to_numpy()` → ORM serialize to wire format

**ML forward connections:** EDA before every training run · feature engineering before sklearn · understanding data distribution is the most underrated ML skill

---

### Capstone — Mini ML Pipeline

**Session:** After all 16 topics complete.

**Files:**
- `01-python/capstone/README.md`
- `01-python/capstone/pipeline.py`

Integrates all 16 topics into a single runnable mini ML pipeline:
- `dataclass` config with `dotenv` loading (Topics 5, 8)
- `pathlib` for file discovery (Topic 11)
- Pandas EDA + feature engineering (Topic 16)
- NumPy normalization + train/test split (Topic 15)
- `TabularDataset` class with `__len__`/`__getitem__` (Topic 9)
- Generator batch streaming (Topic 4)
- `ProcessPoolExecutor` parallel preprocessing (Topic 13)
- Structured JSON logging (Topic 7)
- `@timer` and `@retry` decorators (Topic 3)
- `asyncio.gather()` for parallel feature stats (Topic 10)
- `cProfile` run to profile the full pipeline (Topic 14)
- `pytest` smoke assertions at each stage (Topic 6)
- `joblib` checkpoint save/load (Topic 11)
- Memory-efficient in-place ops (Topic 12)

---

## README Update Protocol

After **each topic** is completed, update `01-python/README.md` with a new entry under `## Field Notes`:

```markdown
### Topic N — [Title]
*YYYY-MM-DD*

[2-4 sentences: what landed, what was surprising, what broke, what will matter in ML.
Not a summary — an honest reflection. Senior engineer's voice, not a textbook.]
```

The README grows as topics are completed. It is never pre-populated.
