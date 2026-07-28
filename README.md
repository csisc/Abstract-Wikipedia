# Multilingual Punctuation and Preposition Documentation

## Rule-Based Natural Language Generation (NLG) Guidelines for Abstract Wikipedia

## Overview

This documentation defines a linguistic framework for handling **punctuation** and **preposition systems** in rule-based Natural Language Generation (NLG), especially within the context of **Abstract Wikipedia**.

The goal is to separate:

1. **Semantic structure** — the meaning representation of a statement.
2. **Syntactic realization** — how a language expresses that meaning.
3. **Orthographic realization** — punctuation, spacing, capitalization, and citation placement.

Punctuation and prepositions should not be treated as fixed universal rules. They are language-dependent realization mechanisms that must be modeled explicitly.

---

# Documentation Structure

## Punctuation Documentation

| File                     | Scope                                                                                       |
| ------------------------ | ------------------------------------------------------------------------------------------- |
| `punctuations/part-1.md` | Sentence structure, termination, interrogation, exclamation, pause, segmentation, quotation |
| `punctuations/part-2.md` | Connection, organization, omission, lexical and morphological functions                     |
| `punctuations/part-3.md` | Semantic, pragmatic, editorial, mathematical, digital, and typographic functions            |

---

## Preposition Documentation

| File                     | Scope                                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------------------------- |
| `prepositions/part-1.md` | Spatial relations                                                                                    |
| `prepositions/part-2.md` | Temporal relations and participant roles                                                             |
| `prepositions/part-3.md` | Causation, means, manner, association, and relation                                                  |
| `prepositions/part-4.md` | Comparison, quantity, composition, topic, logic, possession, social relations, information structure |

---

# 1. Abstract Wikipedia NLG Model

Abstract Wikipedia separates knowledge representation from language realization.

A statement should first exist as an abstract semantic structure:

```
Subject → Predicate → Object
```

Example:

```
Marie Curie → discovered → radium
```

This semantic representation is then expanded into a language-specific realization.

Examples:

English:

```
Marie Curie discovered radium
```

French:

```
Marie Curie a découvert le radium
```

Arabic:

```
اكتشفت ماري كوري الراديوم
```

Japanese:

```
マリー・キュリーはラジウムを発見した
```

The semantic layer should not contain punctuation decisions.

---

# 2. Statement Core and Extension Model

## Core Rule

The core statement:

```
Subject + Verb + Object
```

should **not automatically terminate with a full stop**.

A sentence-final punctuation mark should only be introduced after all possible extensions have been processed.

## Incorrect model

```
Marie Curie discovered radium.
```

The period prematurely closes the statement.

Possible extensions become impossible:

```
Marie Curie discovered radium.
She was born in Poland.
She received two Nobel Prizes.
```

---

## Correct Abstract NLG model

Semantic core:

```
Marie Curie
    discovered
        radium
```

Possible extensions:

```
Marie Curie discovered radium
    and
    received two Nobel Prizes
    in
    1911
    for
    her research
```

Final realization:

```
Marie Curie discovered radium and received two Nobel Prizes in 1911 for her research.
```

---

# 3. Conjunction and Preposition Expansion

The statement generator should allow extensions through:

## Conjunctions

Examples:

```
and
but
or
because
although
while
```

Semantic expansion:

```
A → B
+
C → D
```

Realization:

```
A did B and C did D.
```

---

## Prepositions

Examples:

```
in
from
with
by
for
about
through
during
after
before
```

Semantic expansion:

```
Entity
    relation
        target
```

Example:

Abstract:

```
Book
    topic
        History
```

English:

```
A book about history
```

French:

```
Un livre sur l'histoire
```

Japanese:

```
歴史についての本
```

---

# 4. Punctuation Handling Rules

## Punctuation Is Language-Specific

Punctuation should be treated as a realization layer.

It should not be generated from the semantic representation.

Example:

Semantic:

```
question(entity)
```

Possible realizations:

English:

```
?
```

French:

```
?
```

Arabic:

```
؟
```

Japanese:

```
？
```

---

## Hard-Code Punctuation Rules

Punctuation behavior should be stored in language-specific modules.

Example:

```
Language:
    English

QuestionMark:
    ?

Language:
    Arabic

QuestionMark:
    ؟
```

---

# 5. No Universal Punctuation Assumptions

A multilingual NLG system should not assume:

```
comma = ,
period = .
quotation = ""
```

because languages differ.

Examples:

| Function  | English | French | Arabic | Japanese |
| --------- | ------- | ------ | ------ | -------- |
| Comma     | ,       | ,      | ،      | 、        |
| Period    | .       | .      | .      | 。        |
| Question  | ?       | ?      | ؟      | ？        |
| Quotation | " "     | « »    | « »    | 「 」      |

---

# 6. Citation Placement Rules

Abstract Wikipedia statements may contain inline citations.

Citation placement must be handled separately from punctuation.

The system must know whether citations appear:

* before punctuation
* after punctuation

depending on language and style rules.

---

## Example: Citation Before Punctuation (French)

Some styles:

```
Marie Curie a découvert le radium [1].
```

Structure:

```
Statement
+
Citation
+
Sentence termination
```

---

## Example: Citation After Punctuation (English)

Some styles:

```
Marie Curie discovered radium. [1]
```

Structure:

```
Statement
+
Sentence termination
+
Citation
```

---

# 7. Citation-Aware Sentence Finalization

The finalization pipeline should be:

```
1. Generate semantic statement
        ↓
2. Add syntactic extensions
        ↓
3. Add prepositional relations
        ↓
4. Determine sentence boundary
        ↓
5. Insert citations
        ↓
6. Apply punctuation rules
```

or:

```
Semantic
   ↓
Syntax
   ↓
Citation
   ↓
Punctuation
```

depending on language policy.

---

# 8. Recommended NLG Pipeline

```
Knowledge Graph
        |
        ↓
Abstract Statement
        |
        ↓
Semantic Expansion
        |
        ↓
Language Grammar
        |
        ↓
Preposition Selection
        |
        ↓
Conjunction Expansion
        |
        ↓
Citation Handling
        |
        ↓
Punctuation Realization
        |
        ↓
Final Text
```

---

# 9. Separation of Concerns

## Semantic Layer

Handles:

* entities
* relationships
* facts
* logical structures

Example:

```
Person
    occupation
        scientist
```

---

## Grammar Layer

Handles:

* word order
* agreement
* morphology
* prepositions
* particles

---

## Orthography Layer

Handles:

* punctuation
* capitalization
* spacing
* quotation marks
* citation placement

---

# 10. Design Principles for Abstract Wikipedia

## Principle 1 — Meaning Before Form

Never store:

```
Marie Curie discovered radium.
```

Store:

```
Marie Curie
discovered
radium
```

---

## Principle 2 — Delay Sentence Termination

Do not generate:

```
.
?
!
```

until the complete sentence structure is known.

---

## Principle 3 — Prepositions Are Semantic Relations

Do not store:

```
in
from
with
by
```

as words.

Store:

```
LOCATION
SOURCE
COMPANION
AGENT
```

and let the language module choose the realization.

---

## Principle 4 — Punctuation Is a Realization Rule

Do not store:

```
comma
period
quotation mark
```

inside the abstract representation.

Store:

```
pause
termination
quotation
```

and let each language decide.

---

# 11. Minimal Abstract Representation Example

Input:

```
Entity:
    Marie Curie

Action:
    discover

Object:
    radium

Time:
    1898

Source:
    scientific research

Citation:
    reference-1
```

Possible English output:

```
Marie Curie discovered radium in 1898 through scientific research [1].
```

Possible French output:

```
Marie Curie a découvert le radium en 1898 grâce à la recherche scientifique [1].
```

Possible Japanese output:

```
マリー・キュリーは1898年に科学研究を通じてラジウムを発見した[1]。
```

# 12. Conclusion

For rule-based NLG in Abstract Wikipedia:

* Statements should begin as punctuation-free semantic structures.
* The subject-verb-object core should remain open for extension.
* Prepositions should be modeled as semantic relations, not fixed words.
* Punctuation should be language-specific and hard coded.
* Citations require independent placement rules.
* Sentence termination should occur only after all extensions and references are resolved.
* The final text renderer should combine:

  * semantic representation,
  * grammar rules,
  * preposition realization,
  * citation rules,
  * punctuation rules.

This separation enables multilingual generation while preserving accuracy across languages with different grammatical and orthographic systems.
