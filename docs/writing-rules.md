# Writing rules for system documentation

status: agreed
owner: Lars (@larswgarling)
last reviewed: 2026-11-22

These rules apply to the Markdown files that explain a system in all lucid-binary-GmbH repositories.
Use them when you write a new file and when you change an existing file.
People and AI agents (Claude Code, Devin, Codex, Cursor) use the same rules.

All technical writing in lucid-binary-GmbH follows ASD-STE100 Simplified Technical English (STE).
Part 1 of this file gives the STE rules that we use most.
Parts 2 to 6 give our rules for the structure and format of the files.

## Contents

1. [Language: Simplified Technical English](#1-language-simplified-technical-english)
2. [Which files these rules apply to](#2-which-files-these-rules-apply-to)
3. [Structure of a file](#3-structure-of-a-file)
4. [Format](#4-format)
5. [Diagrams](#5-diagrams)
6. [Keep the documentation correct](#6-keep-the-documentation-correct)
7. [Review checklist](#7-review-checklist)
8. [Examples: before and after](#8-examples-before-and-after)

## 1. Language: Simplified Technical English

The full standard is ASD-STE100.
You can request a free copy of the standard from ASD at [asd-ste100.org](https://www.asd-ste100.org/).
The rules below are a short version for our documents. If a rule here and the standard do not agree, the standard is correct.

### 1.1 Words

- Write in English.
- Use one word for one meaning. Use one meaning for one word.
  For example, if you write "parameter" for a constant of an equation, do not also write "coefficient" or "constant" for the same thing.
- Use simple, common words. Write "use", not "utilize". Write "start", not "initiate". Write "help", not "facilitate".
- Technical names are permitted: names of systems, tools, file formats, libraries, functions, variables and physical quantities.
  Examples: Plant Sampler, Parquet, FastAPI, `MonashWindows`, ODE, Student's-t distribution.
- Write a technical name the same way each time. Use the spelling of the owner of the name (`PharmaPy`, `OPC UA`, `PostgreSQL`).
- Write the names of our systems as the [lucid-systems system index](https://github.com/lucid-binary-GmbH/lucid-systems#system-index) gives them: Knowledge Base, Plant Sampler, Simulation Engine, Training Platform, Benchmark, Recipe.
- Write the full term the first time that you use an abbreviation, then the abbreviation in parentheses: "ordinary differential equation (ODE)".
  Each repository that uses more than five abbreviations or project terms has a glossary (see [3.4](#34-glossary)).
- Do not use slang, jargon from chat, or words that only the team knows ("the thing", "lane 1" without a definition).
- Do not use contractions. Write "does not", not "doesn't".

### 1.2 Noun groups

- Do not put more than three nouns in a row.
  Write "the batch size of the training run", not "training run batch size setting".
- If a technical name has more than three words, use it as it is. Do not add more nouns to it.

### 1.3 Verbs

- Use the active voice. Write "The service writes the time series to S3", not "The time series are written to S3".
- Use the passive voice only in descriptions, and only when you do not know who or what does the action.
- Use the simple tenses: present, past and future. Use the present tense to describe what a system does.
- Do not use the "-ing" form of a verb as a noun or an adjective. Write "When you train the model", not "When training the model".
- Use the imperative (command) form in instructions. Write "Run the tests", not "You should run the tests" or "The tests can be run".

### 1.4 Sentences

- Write one idea in one sentence.
- In instructions, write a maximum of 20 words in each sentence.
- In descriptions, write a maximum of 25 words in each sentence.
- Use the articles "a", "an" and "the" before nouns. Do not leave them out to make a sentence shorter.
- Do not use semicolons to join two sentences. Write two sentences.
- Do not use the words "it", "this" and "that" alone if the reader can think that they refer to more than one thing. Write the noun again.

### 1.5 Paragraphs

- Write one topic in one paragraph.
- Write a maximum of six sentences in a paragraph.
- Start the paragraph with the most important sentence.
- Use a table or a vertical list for three or more items of the same type.

### 1.6 Instructions (procedures)

- Write one instruction in one sentence. You can write two actions in one sentence only if the reader must do them at the same time.
- Write the condition before the instruction: "If the bucket does not exist, make it before you start the service."
- Number the steps if the reader must do them in a sequence. Use a bulleted list if the sequence is not important.
- Write warnings and cautions before the step that they apply to. Start with a command, then give the risk:

  ```markdown
  > [!WARNING]
  > Do not set `AUTH_DISABLED=true` in a deployed environment. This flag stops all authentication.
  ```

- Use "warning" for a risk to people or to confidential data. Use "caution" for a risk to equipment, data or results.
  For a caution, use the GitHub `[!CAUTION]` alert. For other important information, use `[!NOTE]`.
- Tell the reader the result of a step when the result is not clear: "The service starts on port 9000."

### 1.7 Descriptions

- Give the general information before the details.
- Write facts. Do not write "should work", "probably" or "hopefully". If you do not know a fact, write that it is unknown or "to decide".
- Write the reason for a rule or a decision in a separate sentence after the rule.

## 2. Which files these rules apply to

| File | Apply the rules | Notes |
|---|---|---|
| `README.md` at the root of a repository | Yes | Use the structure in [3.2](#32-readmemd-at-the-root-of-a-repository). |
| `README.md` in a directory (for example `src/symbolic/README.md`, `data/README.md`) | Yes | Use the structure in [3.3](#33-readmemd-in-a-directory). |
| Files in `docs/` that explain a system, a component, a data format or a procedure | Yes | |
| `SYSTEM.md`, interface contracts, decision records and templates in `lucid-systems` | Yes | Keep the structure that `lucid-systems/templates/` and `scripts/check_systems.py` require. Apply Part 1, Part 4 and Part 5 in that structure. |
| Agent rule files (`AGENTS.md`, `CLAUDE.md`, `.github/copilot-instructions.md`, `SKILL.md`) | Part 1 only | These files are instructions. Keep their structure. |
| `README.rst` and other reStructuredText files (for example in the wavelet toolboxes) | Part 1 only | Keep the format that Sphinx and PyPI need. |
| Research notes, reading lists, literature notes and session logs (for example `related_work/`, `reviews/`, `.claude/history.md`) | No | These files do not explain a system. |
| `CHANGELOG.md`, licence files, generated files | No | |

## 3. Structure of a file

### 3.1 Rules for all files

- Use one level-1 heading (`#`) at the top of the file. The heading is the name of the system or the component.
- Write one or two sentences below the level-1 heading. These sentences tell the reader what the system does and for whom.
- Do not skip heading levels. A `###` heading comes after a `##` heading.
- Use sentence case for headings: "Run the tests", not "Run The Tests".
- Use a heading that tells the reader what the section contains. For a procedure, start the heading with a verb: "Install the package", "Run the simulation".
- Do not write the same information in two files. Write it in one file and link to it from the other file.
- If a file is longer than 300 lines, move the details into files in `docs/` and link to them.

### 3.2 `README.md` at the root of a repository

Use these sections in this sequence.
Leave out an optional section if it does not apply.
Do not change the names of the sections. The same names in all repositories help the reader to find information.
[readme-template.md](readme-template.md) contains a template that you can copy.

| Section | Required | Content |
|---|---|---|
| `# <Name>` and summary | Yes | One or two sentences: what the system does and for whom. Optional: CI and coverage badges below the summary. |
| `## Status` | Yes | What works, what does not work yet, and if the results are validated. One to five sentences. |
| `## How it works` | Yes | The components and the data flow. Start with a diagram (see Part 5), then explain the diagram in text. |
| `## Install` | Yes | Prerequisites with versions, then the commands to install. Give the operating system if the procedure applies to one operating system only. |
| `## Run` | Yes | The commands to run the system, the most important options, and the result that the reader gets. |
| `## Configuration` | Optional | A table of environment variables, configuration files and options: name, meaning, default, example. |
| `## Inputs and outputs` | Optional | The data that goes in and comes out: format, location, units and a short example. |
| `## Test` | Yes | The commands for tests, linters and type checks. Tell the reader the expected result. |
| `## Related systems` | Yes | A link to the `SYSTEM.md` in `lucid-systems` that this repository implements, and links to neighbour repositories. Write "None" if there are no related systems. |
| `## Known limitations` | Optional | What the system does not do yet, and the risks. Link to an issue for planned work. |
| `## References` | Optional | Papers, datasets and external documentation, with a DOI or a URL. |

- Do not use a "TODO" section. Write planned work as GitHub issues. Write the current limits in "Known limitations".
- Do not copy requirements from a `SYSTEM.md` into a README. Link to them by requirement ID (for example `SIM-R3`).

### 3.3 `README.md` in a directory

Use the same level-1 heading and summary as in [3.1](#31-rules-for-all-files).
Then use only the sections from [3.2](#32-readmemd-at-the-root-of-a-repository) that apply to the directory, in the same sequence.
For a data directory, use "Inputs and outputs" to give the source, the licence, the format and the procedure to get the data.

### 3.4 Glossary

- Put the glossary in `docs/glossary.md`. If the repository already has a terms file (for example `docs/terminology.md`), use that file and do not make a second one.
- Use a table with three columns: term, abbreviation, meaning.
- Sort the terms alphabetically.
- Use the terms and abbreviations of the glossary in all files of the repository. If a file uses a different term, change the file or the glossary so that they agree.

## 4. Format

### 4.1 Commands and code

- Put each command in a fenced code block with a language tag (`bash`, `powershell`, `python`, `toml`).
- Do not put a prompt character (`$` or `>`) before a command. The reader must be able to copy the block and run it.
- Write one command on each line. Use a comment on the same line only for a short explanation.
- Tell the reader the directory in which to run the command, if it is not the root of the repository.
- Write placeholders in angle brackets and explain each placeholder below the block: `<dataset_name>`.
- Use code format (backticks) for file names, paths, commands, functions, variables, environment variables and values: `app/main.py`, `uv run pytest`, `AUTH_DISABLED=true`.

### 4.2 Numbers, units and dates

- Use SI units. If a source uses other units, give the SI value and the source value.
- Put a space between a number and its unit: `600 min`, `45 °C`, `1 L`. Do not put a space before `%`.
- In a table, put the unit in the column heading in square brackets: `Temperature [°C]`.
- Write dates in the format `YYYY-MM-DD`.
- Use a decimal point, not a decimal comma.

### 4.3 Lists and tables

- Use a numbered list for steps in a sequence. Use a bulleted list for other items.
- Make all the items of a list the same type: all commands, all nouns or all sentences.
- Start each list item with a capital letter. Put a full stop at the end of a list item that is a full sentence.
- Use a table to compare items or to give properties of items. Give each table a short sentence before it that tells the reader what the table shows.

### 4.4 Links

- Use link text that tells the reader what the link opens. Do not write "click here" or "this link".
- Use relative links to files in the same repository: `[I1 contract](interfaces/I1_knowledge_to_sampler/README.md)`.
- Use the full GitHub URL for files in a different repository.
- Write the source of an equation, a parameter or a dataset as a DOI, or as a book with its section. Do not invent a source.

### 4.5 Emphasis

- Use bold only for a word that the reader must not miss. Do not use bold for full sentences.
- Do not use capital letters for emphasis. Write "local only", not "LOCAL-ONLY".
- Do not use emoji.
- Use GitHub alerts (`> [!NOTE]`, `> [!CAUTION]`, `> [!WARNING]`) for notes, cautions and warnings (see [1.6](#16-instructions-procedures)).

## 5. Diagrams

- Use a Mermaid diagram in a fenced code block with the tag `mermaid`. GitHub shows Mermaid diagrams as images.
  Do not use ASCII art or image files for a diagram that Mermaid can show.
- Write one sentence before the diagram that tells the reader what the diagram shows.
- Explain the diagram in text after it. The text must give the same information, because some readers and tools cannot see the diagram.
- Write the labels in STE. A box label is a noun group: "Prior service", "ODE simulation". An arrow label tells what moves along the arrow: "Parquet objects", "Bearer token".
- Use the same names in the diagram and in the text.
- Put labels in double quotes: `A["Plant Sampler"]`. Quotes prevent errors from special characters.
- Use a maximum of 15 boxes in one diagram. If you need more boxes, make one diagram for the overview and one diagram for each part.
- Use `flowchart TD` (top to bottom) for a data flow or a decision flow. Use `sequenceDiagram` for messages between components over time.
- Make sure that GitHub can show the diagram before you merge the change. Open the file in the PR on GitHub, or render it with `mermaid-cli`.

## 6. Keep the documentation correct

- If a pull request changes the behavior, the interface, the configuration or the commands that a document describes, update the document in the same pull request.
- Make sure that each command in a document runs, and that each link opens the correct target.
- If a document has a `last reviewed` line, change the date when you review the document.
- If you find a document that is not correct and you cannot correct it, open an issue.

## 7. Review checklist

Use this checklist when you write or review a document.

- [ ] The file starts with one level-1 heading and a summary of one or two sentences.
- [ ] The sections have the names and the sequence of [3.2](#32-readmemd-at-the-root-of-a-repository) or [3.3](#33-readmemd-in-a-directory).
- [ ] Each sentence has one idea: a maximum of 20 words in instructions and 25 words in descriptions.
- [ ] Instructions use the imperative. Descriptions use the active voice and the present tense.
- [ ] The file uses one term for one concept, the same as the glossary.
- [ ] Each abbreviation is written in full at its first use.
- [ ] Commands are in fenced code blocks without a prompt character, and they run.
- [ ] Values have SI units with a space before the unit.
- [ ] Each diagram is Mermaid, has a sentence before it, is explained in text and shows correctly on GitHub.
- [ ] Links open the correct target and the link text tells the reader what opens.
- [ ] The document agrees with the code in the same pull request.

## 8. Examples: before and after

The examples below come from our repositories.

| Before | After | Rules |
|---|---|---|
| `AUTH_DISABLED=true` is a LOCAL-ONLY flag: it turns off all authentication and serves `/docs` + `/openapi.json` (so Swagger's "Try it out" works). | Use `AUTH_DISABLED=true` only on your local computer. This flag stops all authentication. It also makes the service show `/docs` and `/openapi.json`. | 1.4, 1.6, 4.5 |
| Doesn't scale past a single OPC UA endpoint/reader efficiently — switch to actor-based programming, which indirectly solves above two points. | Known limitation: Viper reads from one OPC UA endpoint only. Issue #<n> describes a change to an actor model to read from more endpoints. | 1.1, 1.4, 3.2 |
| Incase to add additional datasources like `OPCUA` or `Postgresql` add the function in `GenericReader` class in `src/s3po/readers/base.py`. | To add a data source (for example OPC UA or PostgreSQL), add a function to the `GenericReader` class in `src/s3po/readers/base.py`. | 1.1, 1.4, 1.6 |
| The serialiser is built on assumption that data has signal of interest (IS), covariates (CV), and label (LBL) as roles. (The code uses `CV`, but `docs/terminology.md` writes "CS - Covariate Signal".) | The serialiser gives each column of the data one of three roles: signal of interest (IS), covariate (CV) or label (LBL). Change the glossary to "covariate (CV)" so that the glossary, the README and the code agree. | 1.1, 1.3, 3.4 |
| `$ uv sync --extra dev` | `uv sync --extra dev` | 4.1 |
