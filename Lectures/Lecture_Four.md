# Lecture Four: Installing and Running Local LLMs

## Learning Objectives

By the end of this lecture, participants should be able to:

- explain what it means to install, initialise, and run a local LLM;
- identify a realistic small model for a modest consumer-grade laptop;
- install or inspect a local runtime such as Ollama, with LM Studio as a graphical alternative;
- start a local model server and check that it is bound to `localhost`;
- make a first small local-model request using a toy health or social example;
- explain model weights, quantisation, context length, model tags, and local server ports;
- diagnose common local setup failures;
- document local-model provenance, hardware constraints, validation plans, and governance decisions.

This lecture is intentionally practical. The aim is not to run the largest possible model or to turn participants into infrastructure engineers. The aim is to understand the practical sequence: choose a small model, install a runtime, start the service, test one prompt, inspect what happened, and decide whether the workflow is good enough for a health or social research task.

## The Installation-First Mental Model

Yesterday's remote API workflow began with an account, an API key, a model name, and a request. A local workflow begins differently:

1. Choose a local runtime.
2. Install it.
3. Choose a model small enough for the machine.
4. Download the model weights.
5. Start the runtime or local server.
6. Run one tiny test prompt.
7. Record the model, runtime, machine, and settings.

That sequence matters pedagogically. If participants do not understand the installation and initialisation process, later code examples feel detached from the real workflow.

## Recommended Class Path: Ollama First

For this course, Ollama is the recommended first path because it gives a simple command-line workflow and a local HTTP API. The official documentation describes Ollama as available for macOS, Windows, and Linux, with the default local API served at:

```text
http://localhost:11434/api
```

For a modest laptop, the model choice matters more than the API shape. Start with a very small model and accept that it may be less capable. Good classroom candidates are:

- `smollm2:360m`, around hundreds of MB, useful for proving the local workflow;
- `qwen3:0.6b`, also small enough for many laptops;
- `llama3.2:1b`, larger but still realistic for many machines.

The teaching point is not that these are the best models. The teaching point is that local models have to fit the machine, the task, and the session time.

## Basic Ollama Workflow

The usual beginner workflow is:

```bash
ollama --version
ollama pull smollm2:360m
ollama run smollm2:360m
ollama list
```

If the local server is running, a small local API test can use:

```bash
curl http://localhost:11434/api/chat -d '{
  "model": "smollm2:360m",
  "messages": [
    {"role": "user", "content": "Classify this public comment: the bus was cancelled and I missed my clinic appointment."}
  ],
  "stream": false
}'
```

Do not start with private or sensitive data. Use synthetic public-health or social-service examples until the installation, model behaviour, and logging are understood.

## Alternative Beginner Path: LM Studio

LM Studio is useful when learners prefer a graphical application. Its developer documentation describes local APIs, model management, and OpenAI-compatible endpoints. In a classroom, LM Studio can be introduced as:

- a graphical way to search for and download local models;
- a way to load one model at a time;
- a way to start a local server;
- a bridge for people who are less comfortable with command-line tools.

The same warnings apply: choose small models, check local server settings, avoid sensitive data during testing, and document the model and runtime.

## Lower-Level Path: llama.cpp

llama.cpp is important because many local tools build on similar ideas: GGUF model files, quantisation, CPU/GPU offload, and local serving. It is not the first installation path for most beginners in this course.

Introduce llama.cpp as the lower-level route for learners who later need more control over model files, quantisation choices, and server configuration.

## What Gets Installed?

Local LLM work usually involves several separate things:

- the runtime application, such as Ollama or LM Studio;
- model weights downloaded to local storage;
- a model cache directory;
- logs;
- a local server process;
- optional Python packages or client libraries.

Participants often think "the model" is one thing. In practice, the runtime, model file, tag, parameters, and local server settings are all part of the method.

## Choosing a Model for a Modest Laptop

Use this order of questions:

1. How much memory and disk space does the machine have?
2. Is the model small enough to download during class?
3. Is the model small enough to load without freezing the laptop?
4. Is the output quality sufficient for the teaching task?
5. Is the licence suitable for the intended use?

For class, prefer a tiny model that runs over a larger model that fails to load. A tiny model can still teach installation, prompting, response parsing, timing, failure modes, and governance.

## Key Concepts

### Model Weights

The model weights are the learned parameters stored in files. Installing a runtime does not mean a model is already available. Usually, the model weights must be downloaded separately.

Research implication: record the exact model tag, not just the model family.

### Quantisation

Quantisation reduces the precision of model weights so the model uses less memory and may run faster. The trade-off is that quality can change.

Research implication: quantisation is part of the method, not a minor technical detail.

### Model Tags

Local model names often include tags such as `:360m`, `:1b`, `:latest`, or quantisation-specific labels. Tags affect what is downloaded and run.

Research implication: `llama3.2` and `llama3.2:1b` should not be treated as identical in a methods section.

### Localhost and Ports

A local model server usually listens on a local port. Ollama commonly uses `localhost:11434`; LM Studio commonly uses a local server port such as `1234` when configured that way.

Research implication: local servers should stay bound to `localhost` during class. Do not expose them to a wider network unless there is a deliberate, secured deployment plan.

### Context Length and Output Length

Local models may advertise long context windows, but practical performance still depends on hardware. Long prompts can be slow even before the model starts generating.

Research implication: long health or social documents need chunking, sampling, or retrieval designs, not blind copy-paste into one prompt.

## First Health and Social Example

Use a small synthetic example:

```text
Public comment: the evening bus was cancelled and I missed my diabetes clinic appointment.

Task: classify as one of access_barrier, housing_stress, health_need, or other. Return only the label.
```

This is enough to test whether the local model runs. It is not enough to validate a research workflow.

After the first response, ask:

- Did the model follow the allowed labels?
- How long did it take?
- Was the response deterministic enough for the task?
- Did the model add unsupported explanation?
- Would a smaller or larger model change the result?

## Common Installation and Initialisation Failures

Local model workflows fail in practical ways:

- the runtime is not installed;
- the command is not on the PATH;
- the model has not been downloaded;
- the model tag is wrong;
- the server is not running;
- the wrong port is used;
- another process is already using the port;
- the machine does not have enough memory;
- the model loads but generation is too slow;
- a security setting blocks the server;
- the server is accidentally exposed beyond `localhost`.

These are not distractions from the course content. They are part of what local LLM implementation means.

## Governance for Local Models

Local does not automatically mean safe. It changes the data-flow question, but does not remove governance.

Important questions:

- Are prompts and outputs stored in logs?
- Where are model files and caches stored?
- Is the laptop shared, encrypted, or backed up to cloud storage?
- Is the local server accessible only from the same machine?
- Does the model licence allow the intended research or teaching use?
- What validation is required before the model output is treated as evidence?

For health and social settings, begin with synthetic or public examples. Move to sensitive data only under an approved governance plan.

## Practical Session

Participants work through an install-and-initialise workflow:

1. Check whether Ollama or LM Studio is installed.
2. Choose a small model suitable for a modest laptop.
3. Download or document how to download that model.
4. Start the local runtime or local server.
5. Run one synthetic health/social prompt.
6. Optionally call the local server from Python, with live calls disabled by default.
7. Record model tag, runtime version, machine constraints, prompt, parameters, and observed failure modes.

The practical session is not primarily about comparing remote and local models. It is about making a local model real enough that participants understand what has to be installed, started, checked, and documented.

## Lecture Flow

### 1. Recap From Lecture Three

Remote APIs gave us request structure and parameter control. Local models keep some of those ideas but add installation, model files, server processes, local storage, and hardware constraints.

Discussion prompt:

> What did the API provider handle yesterday that we now have to handle on the laptop?

### 2. Install, Pull, Run

Walk through the sequence:

- install runtime;
- check version;
- pull a small model;
- run a prompt;
- list downloaded models;
- stop or restart the server if needed.

### 3. Small Models Are a Feature, Not a Failure

Explain why the class uses tiny models first. A small model lets everyone practise the workflow without needing specialist hardware.

### 4. Local Server and Python

Show how a local server makes the model callable from Python. Keep the first request short, disable streaming for beginner examples, and inspect the response shape only after the model is known to run.

### 5. Troubleshooting

Treat errors as implementation evidence. "Command not found", "connection refused", "model not found", and "out of memory" each imply a different next step.

### 6. Health and Social Research Use

Return to the same applied question throughout:

> Would this local setup be appropriate for classifying, summarising, or extracting fields from health or social text?

The answer depends on validation, sensitivity, model quality, runtime speed, and governance.

## Suggested Reading and Documentation

- Ollama documentation: https://docs.ollama.com/
- Ollama API documentation: https://docs.ollama.com/api/introduction
- Ollama model library: https://ollama.com/library
- LM Studio developer documentation: https://lmstudio.ai/docs/developer
- llama.cpp server documentation: https://github.com/ggml-org/llama.cpp/blob/master/tools/server/README.md
- vLLM OpenAI-compatible server documentation, for server-side contrast: https://docs.vllm.ai/en/latest/serving/openai_compatible_server/

Before teaching, check these links for changes. Tool names, endpoints, install commands, and model defaults change quickly.
