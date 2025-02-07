---
layout: post
title: Ensuring Correct Execution Context in Ray Tune’s Distributed Environment
categories: [Large Language Models (LLMs), Hyperparameter Search, RAY Tune]
tags: [LLM, RAY Tune, Closure]
author: Dae-young Kim
comment: true
---
# How `ray.tune.Tuner` works?
Let's say we define a tuner and its trainable like this:
```python
MODEL_CONFIG = { ... }
RAY_HP_SPACE = { ... }

def trainable(config):
    ...

tuner = tune.Tuner(
        trainable,
        tune_config=tune.TuneConfig(
            ...
        ),
        param_space=RAY_HP_SPACE,
    )
```
These are the three steps happens inside during the hyperparameter search using Ray Tune.
1. **Tuner Captures the Context:** When you initialize the Tuner, it stores (or "captures") the `trainable` function as part of its configuration. That function’s closure includes any local variables (like the trial-specific configuration passed to it) and references to global variables (like `MODEL_CONFIG`).
2. **Serialization and Distribution:** Ray Tune then serializes (pickles) the Tuner—including the captured `trainable` function—and sends it to a remote worker process.
3. **Independent Remote Environment:** The remote worker process has its own environment, independent of the driver. If `MODEL_CONFIG` was captured as a global variable and is not correctly defined or available in the worker’s environment, it may end up being `None` (or have an unexpected value). This leads to errors when the worker calls `trainable`

# Key Concepts
- **Trainable:** an object that you can pass into a Tune run.
- **Closure:** a programming concept where a function "remembers" the environment in which it was created. This means that the function retains access to variables from its surrounding scope—even after that scope has finished executing.


# Reference
- [Getting Started with Ray Tune](https://docs.ray.io/en/latest/tune/getting-started.html)
- [Ray Tune Trainables](https://docs.ray.io/en/latest/tune/key-concepts.html#ray-tune-trainables)
- [A Guide To Parallelism and Resources for Ray Tune](https://docs.ray.io/en/latest/tune/tutorials/tune-resources.html)
  
