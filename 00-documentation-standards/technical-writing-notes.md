# Technical Writing Notes

## Purpose

This document defines the basic writing standards I will use while documenting the Secure Mission Data Platform project.

The goal is to keep the repository clear, consistent, and professional as the project grows from local Linux fundamentals into AWS architecture, Terraform, security review, cost modeling, and validation testing.

## Writing Principles

### Be Clear

Documentation should explain what was learned, what was built, why it matters, and how it connects to the project.

Avoid vague statements. Be specific about the concept, command, service, or design choice being documented.

### Be Honest

The documentation should clearly separate what has already been completed from what will be revisited later.

Use wording such as:

* currently learning
* current local lab use
* future AWS connection
* will be revisited later
* planned production upgrade

Avoid wording that makes unfinished work sound completed.

### Be Structured

Most early learning documents should follow this structure:

```text
# Topic Name

## Purpose
Why this document exists.

## What I Learned
The concept explained in plain English.

## Commands / Examples
Commands, examples, notes, or screenshots.

## Current Use
How I am using the concept right now.

## Future AWS Connection
How the concept may map to AWS later.

## Project Connection
How the concept supports the Secure Mission Data Platform.

## Lab Proof
What I practiced, tested, or validated.
```

## Documentation Standards

### Use Short Sections

Long paragraphs are harder to scan. Break documentation into clear sections with headings.

### Use Plain English

The purpose is not to sound complicated. The purpose is to explain technical ideas clearly.

### Use Code Blocks for Commands

Commands should be written inside code blocks.

Example:

```bash
df -h
```

### Explain Why the Command Matters

Do not only list commands. Explain what the command does and why it matters.

Weak example:

```text
df -h shows disk usage.
```

Better example:

```text
df -h shows filesystem disk usage in a human-readable format. This matters because disk space issues can cause services, logs, backups, and applications to fail.
```

### Separate Current Knowledge From Future Mapping

When documenting future AWS connections, avoid implying completed AWS experience too early.

Use:

```text
This concept will later be revisited when the project maps local Linux servers to AWS EC2.
```

Avoid:

```text
This proves my EC2 architecture knowledge.
```

## Project Documentation Goal

Each document should answer at least one of these questions:

* What did I learn?
* What did I build?
* Why does it matter?
* How does it connect to the architecture?
* What did I test?
* What decision does this support?
* What will be revisited later?

## Current Standard

For early Linux foundation notes, the preferred structure is:

```text
Purpose
What I Learned
Commands / Examples
Current Use
Future AWS Connection
Project Connection
Lab Proof
```

As the project becomes more advanced, architecture documents will use more specific formats such as:

* Architecture Decision Records
* runbooks
* risk registers
* cost models
* validation reports
* architecture review documents
