---
layout: default
version: 0.1.1
---

# Lower Speck {{ page.version }}

Lower Speck is a method for creating a light-weight requirements specification document.

Keep reading to learn how to make a Lower Speck document and how to use it in a software product.

## The Need for a Requirements Document

A Lower Speck document provides a well-defined, programmer-friendly, single location to specify and change requirements throughout the lifetime of a software product.

Most rapid application projects use informal requirements documents written in plain human language. These have a varying amount of detail and are difficult to cite. Often, they exist in several different documents sent over different mediums; for example, via email and ticketing systems.

Software requirements change over time, and often the full set of requirements is unclear to most or all parties with an interest in the software.

Any centralized requirements document can help clear up organizational confusion.

With a Lower Speck document:

- Developers can identify poorly explained requirements.

- Developers can include requirement citations in code to aid in system maintenance.

- Stakeholders can see the connection between their informal documents and the software.

- Automated tools can show which requirements have been addressed.

- Changing requirements can be documented.

- No special software is strictly required.

- Even large lists of requirements stay as light-weight as possible.

## The Lower Speck Process

The following describes how Lower Speck can be used during development of software.

1. Stakeholders MUST give developers a plain language specification.

2. Developers MUST produce a Lower Speck document as shown in the next section. This MAY include flagging any requirements they believe are insufficient.

3. Developers MAY revise the stakeholders' original plain language document to include references to the Lower Speck document.

4. The stakeholders MAY review the Lower Speck document to discover any misunderstandings.

5. The stakeholders MAY choose this time or any other time to request changes.

6. When changes are requested, the developers MUST insert new requirements and MAY flag any existing requirements as obsolete.

7. As development proceeds, developers MUST include references to requirements ID's as explained below. 

8. The Lower Speck document SHOULD be saved with the software code in a version control system.

## The Lower Speck Format

A Lower Speck document follows these formatting rules. These rules are written in the Lower Speck format.

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

```
1. The specification MAY contain any number of blank lines.

2. A non-blank line of the specification SHALL be considered a requirement.
2.a. Any line MAY have leading whitespace. Leading whitespace is not part of the requirement.

3. A requirement MUST begin with an ID.
3.a. An ID MUST be a numeric segment followed by a series of alphabet segments.
3.b. ID segments MUST be separated and followed by single dots.
3.c. An ID MUST NOT contain whitespace.
3.d. An ID MUST have one or more segments.

4. An ID MUST be followed by whitespace.

5. Following the ID and the space, the requirement MAY include a flag section.
5.a. The flag section MUST start with a left parenthesis and end with a right parenthesis.
5.b. The flag section SHOULD contain tokens.
5.c. The flag section's tokens MUST be separated by commas.
5.c.a. The flag section's tokens MAY include X. An X indicates that the requirement is obsolete.
5.c.b. The flag section's tokens MAY include I. An I indicates that the specification is insufficient.
5.c.c. The flag section MAY include custom tokens.
5.c.d. Custom tokens MUST begin with a dash (-).

6. If a flag section is present, it MUST be followed by whitespace.

7. The text of the requirement is the final part. It MUST be text in plain language.
7.a. A requirement's text SHOULD use SHOULD, MUST, MAY, etc. as defined in RFC 2119.
7.b. A requirement's text MUST NOT include newlines.
7.c. All text SHOULD be in complete sentences with proper grammar.

8. Specification requirements SHALL be well-ordered according to the following.
8.a. A requirement with only one segment in its ID SHALL be considered a top-level requirement.
8.b. A multi-segment ID SHALL identify a sub-requirement.
8.c. A sub-requirement MUST have an ID starting with the ID of its parent.
8.d. A requirement with no sub-requirements SHALL be considered a bottom-level requirement.
8.e. A sub-requirement MUST follow its parent requirement.
8.f. Requirements MUST be ordered numerically and alphabetically by their ID's.
8.g. Two requirements that have the same parent, or no parent, SHALL be considered siblings.
8.h. The complete set of ordered siblings MUST have no ID gaps. I.e., the existence of "2.c." implies that "1.", "2.", "2.a.", and "2.b." MUST exist.
8.i. The first top-level requirement MUST have ID "1.".
8.j. The first of a set of sub-requirements MUST have "a." as the last segment of its ID.
8.k. Alphabetic segments MUST proceed by adding more characters when necessary. I.e., the sub-requirements following "z." are "aa.", "ab.", "ac.", and so on.
```

## Lower Speck References in Code

For Lower Speck to be useful, requirement ID's MUST be referenced in code.

A reference MUST be formatted as `LWR <ID>`, usually in a code comment. Automated tools SHOULD use text search to find references in this format. The full text of the requirement MAY also be included in the comment.

A code segment MAY have no reference to a requirement.

A code segment MAY have multiple references.

A single requirement MAY be referenced multiple times.

To fully address a specification, all bottom-level ID's MUST be referenced.

In projects that use testing suites, references SHOULD be included with the tests and SHOULD NOT be included in operational code.

In projects without testing suites, references SHOULD be included with the operational code.

## Making Changes to a Lower Speck Document

Developers SHOULD make changes to the Lower Speck document as needed.

A requirement MUST NOT be removed when making changes.

A requirement's ID MUST NOT change.

A requirement with no flag section MAY have one added.

A flag section with no tokens is empty and MAY be removed.

A requirement MAY be marked obsolete by adding an X token to its flag section.

A requirement's text MAY be changed to another version if the meaning remains the same.

A requirement's text MUST NOT change to reflect a different meaning.

An obsoleted requirement MAY have additional text to explain its reason for obsolescence.

When a requirement becomes obsolete, any code referencing it SHOULD be reviewed. References to obsoleted requirements MAY be removed.

An obsoleted requirement SHOULD remain obsoleted. If the requirement needs to be reintroduced, a new requirement SHOULD be written.

A requirement MAY be marked insufficient by adding an I token to its flag section. An insufficient requirement is one that is expected to have sub-requirements added later.

An requirement MAY be unmarked insufficient by removing the I token from its flag section.

Blank lines MAY be removed or added.

## Justification (or TL;DR)

The primary purpose of Lower Speck is to establish a list of requirements and reference them from the software code.

This is achieved by giving each requirement a permanent ID. Therefore, it's important that no requirements be deleted from the list. Instead they are flagged obsolete.

The rest of the specification mostly ensures that the list is well defined so that it can be easily verified by both humans and software.

## TO DO

Need More Examples.

## About

Lower Speck is authored by <a href="http://dankuck.github.io/">Daniel Kuck-Alvarez</a>.

Released under a <a href="http://creativecommons.org/licenses/by/3.0/">Creative Commons - CC BY 3.0</a> license.
