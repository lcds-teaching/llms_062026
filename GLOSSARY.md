# Course Glossary

This glossary defines terms used across the lectures, labs, and solutions. It is deliberately short and practical. If a term has a more technical meaning in the research literature, the course will introduce that meaning when it becomes necessary.

## Python and Notebooks

**Code cell:** A notebook block that runs Python code.

**Markdown cell:** A notebook block that contains explanation, headings, or instructions.

**Variable:** A name that stores a value, such as `note = "patient missed appointment"`.

**String:** Text inside quotation marks.

**List:** An ordered collection of values, such as `["housing", "benefits", "clinic"]`.

**Dictionary:** A collection of named fields, such as `{"area": "North", "score": 0.72}`.

**Function:** Reusable code with a name. Functions usually take inputs and return outputs.

**Loop:** Code that repeats an action for each item in a collection.

**Boolean:** A true/false value, written in Python as `True` or `False`.

**DataFrame:** A table-like data object, usually created with `pandas`.

## NLP and LLMs

**NLP:** Natural language processing; computational work with text or speech.

**Corpus:** A collection of texts.

**Document:** One text in a corpus. It might be a paragraph, survey response, clinic note, complaint, or article.

**Token:** A piece of text used by a model. Tokens can be words, word pieces, punctuation, or other fragments.

**Tokenisation:** The process of splitting text into tokens.

**Embedding:** A numerical representation of text.

**Classifier:** A model or rule that assigns a label, such as `urgent`, `routine`, or `not relevant`.

**Summarisation:** Producing a shorter version of a longer text.

**Information extraction:** Pulling structured fields from text, such as service type, location, or risk indicator.

**Prompt:** The instruction or input sent to a language model.

**System prompt:** A higher-level instruction that sets the role, boundaries, or output format for a model.

**Temperature:** A parameter that affects how variable model outputs can be. Lower values are usually more consistent.

**Top-p:** A parameter that controls how many likely next tokens the model may choose from.

**Max tokens:** A limit on how much text the model can produce.

**Context window:** The amount of text a model can consider at once.

**Hallucination:** An output that sounds plausible but is not supported by the input or evidence.

## APIs and Local Models

**API:** A structured way for code to talk to a remote service.

**API key:** A secret token used to authenticate with an API. Never paste it into a notebook or GitHub.

**Hosted model:** A model run by a third-party provider and accessed over the internet.

**Local model:** A model run on your own machine.

**Open-weight model:** A model whose weights are available to download, subject to its licence.

**Quantisation:** A way to reduce model size and memory use, often at some cost to quality.

**Latency:** How long a model takes to respond.

**Reproducibility:** The ability to understand and, as far as possible, repeat an analysis later.

## Research and Governance

**Personal data:** Data about an identifiable person.

**Sensitive data:** Data that needs extra care, such as health information or confidential service records.

**Data minimisation:** Sending or storing only the data needed for a task.

**Validation:** Checking model outputs against evidence, labels, expert review, or other standards.

**Failure mode:** A predictable way that a method can go wrong.

**Human review:** Having a person inspect, correct, or approve outputs before they are used.

**Audit trail:** A record of inputs, parameters, model details, outputs, and decisions.
