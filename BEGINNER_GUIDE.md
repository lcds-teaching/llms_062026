# Beginner Guide

This guide is for participants who are new to Python, notebooks, GitHub, or LLM tooling. You do not need to understand everything before the course starts. The goal is to know where to click, what to run, and what to do when something breaks.

## Start Here

Use this order:

1. Read `setup.md`.
2. Install the tools listed there.
3. Open this project folder in VS Code.
4. Open `Labs/Lab_One.ipynb`.
5. Select the `lcds-python` Python environment as the notebook kernel.
6. Run the first few cells.
7. If something fails, read the error message and check the troubleshooting section below.

The lab notebooks are designed to be worked through in order. The solution notebooks are there for review after you have tried the exercises.

## What Is a Notebook?

A notebook is a document made of cells.

- A **markdown cell** contains explanation, instructions, or headings.
- A **code cell** contains Python code that can be run.
- The output of a code cell appears directly below it.

Run cells from top to bottom. Later cells often depend on variables created earlier.

## How to Run a Cell

In VS Code or Jupyter:

- click inside a code cell;
- press the run button, or press `Shift+Enter`;
- read the output below the cell;
- move to the next cell.

If a cell gives an error, do not panic. Errors are part of programming. Read the last line of the error message first.

## How to Approach Lab Questions

For each question:

1. Read the question once without typing.
2. Read the `Programming Plan`.
3. Find the starter code cell.
4. Fill in one line at a time.
5. Run the cell.
6. Print intermediate outputs if you are unsure.
7. Compare your result with the requested output.

Most questions are meant to be solved with short code. If your answer becomes very long, pause and ask for help.

## Common Python Objects

- **String:** text in quotes, such as `"clinic access"`.
- **Integer:** a whole number, such as `12`.
- **Float:** a decimal number, such as `0.07`.
- **List:** an ordered collection, such as `["Northside", "Central"]`.
- **Dictionary:** named fields, such as `{"area": "Northside", "value": 78.4}`.
- **Function:** reusable code with a name.

The first lab introduces these slowly.

## If Something Breaks

Try these steps:

1. Run the notebook from the top again.
2. Check whether a variable was created in an earlier cell.
3. Check spelling and capitalisation.
4. Check quotation marks around strings.
5. Check indentation inside loops, functions, and `if` statements.
6. Restart the notebook kernel if outputs look inconsistent.
7. Ask for help and show the exact error message.

Useful rule: the most important part of an error is often the final line.

## Data and Examples

The core notebooks use small built-in examples, mostly drawn from public health and social research scenarios. They should run without internet access.

If a later optional exercise asks you to download data or call a model, it will say so explicitly before the code cell.

## API Keys and Local Models

You do not need API keys for the core labs.

- Lab Three explains remote APIs, but live calls are optional.
- Lab Four explains local models, but live local calls are disabled by default.
- The notebooks use mock responses unless you deliberately enable live calls.

Do not paste API keys into notebooks.

## How to Use Solutions

Try the lab first. Then open the matching file in `Solutions/`.

For example:

- lab: `Labs/Lab_Two.ipynb`
- solution: `Solutions/Lab_Two_Solutions.ipynb`

Read the solution code slowly. The aim is not just to get the answer, but to understand the pattern.
