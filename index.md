---
layout: default
version: 0.2.0
---

# Lower Speck {{ page.version }}

By writing out requirements, we can ensure that a project's goals are explained to any level of detail throughout the lifetime of the project.

By including references to those requirements in our software, we can ensure that all the requirements are addressed.

By following a few simple rules, we can equip the computer to verify that we've addressed all requirements.

Lower Speck is a light-weight process for requirements management.

## The Lower Speck Process

1. Stakeholders give developers a plain language specification.

2. Developers produce a Lower Speck document as shown in the next section. This may include flagging any requirements they believe are insufficient.

3. Developers may revise the stakeholders' original plain language document to include references to the Lower Speck document.

4. The stakeholders should review the Lower Speck document to discover any misunderstandings.

5. The stakeholders may choose this time or any other time to request changes.

6. When changes are requested, the developers insert new requirements and flag existing requirements as obsolete where appropriate.

7. As development proceeds, developers include references to requirement ID's in code.

8. Developers save the Lower Speck document with the software code in its version control system.

## The Lower Speck Format

A Lower Speck document is made up of requirements.

A Lower Speck document follows these formatting rules. These rules are written as an example of the Lower Speck format.

The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

```
1. The specification MAY contain any number of blank lines.

2. A requirement MUST be a non-blank line of the specification.
    2.a. Any line MAY have leading whitespace. Leading whitespace is not part of the requirement.

3. A requirement MUST begin with an ID.
    3.a. An ID MUST be a numeric segment followed by a series of alphabetical segments.
    3.b. Each ID segment MUST be followed by a single dot.
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
        5.c.e. Custom tokens MUST NOT contain a right parenthesis.

6. If a flag section is present, it MUST be followed by whitespace.

7. The final section MUST be the text of the requirement, in plain language.
    7.a. A requirement's text SHOULD use SHOULD, MUST, MAY, etc. as defined in RFC 2119.
    7.b. A requirement's text MUST NOT include newlines.
    7.c. All text SHOULD be in complete sentences with proper grammar.

8. Specification requirements MUST be well-ordered according to the following.
    8.a. A top-level requirement MUST have only one segment.
    8.b. A sub-requirement MUST have a multi-segment ID.
    8.c. A sub-requirement MUST have an ID starting with the ID of its parent.
    8.d. A requirement with no sub-requirements SHALL be considered a bottom-level requirement.
    8.e. A sub-requirement MUST follow its parent requirement.
    8.f. Requirements MUST be ordered numerically and alphabetically by their ID's.
    8.g. Two requirements that have the same parent, or no parent, SHALL be considered siblings.
    8.h. (X) The complete set of ordered siblings MUST have no ID gaps. I.e., the existence of "2.c." implies that "1.", "2.", "2.a.", and "2.b." MUST exist.
    8.i. (X) The first top-level requirement MUST have ID "1.".
    8.j. The first of a set of sub-requirements MUST have "a." as the last segment of its ID.
    8.k. Alphabetic segments MUST proceed by adding more characters when necessary. I.e., the sub-requirements following "z." are "aa.", "ab.", "ac.", and so on.
    8.l. A complete set of ordered sub-requirement siblings MUST have no ID gaps. I.e., the existence of "2.c." implies that "2.", "2.a.", and "2.b." MUST exist.
    8.m. Top-level siblings MAY have ID gaps.
        8.m.a. Top-level siblings MUST be ordered, even if they have ID gaps.
```

Note that requirement 8.h. has been obsoleted and 8.m. has been added instead. Top-level requirements can have ID gaps now, but sub-requirements cannot have ID gaps.

Note that requirement 8.i. has been obsoleted. The first top-level ID does not have to be 1.

## Lower Speck References in Code

For Lower Speck to be useful, requirement ID's MUST be referenced in code.

A reference MUST be formatted as `LWR <ID>`, usually in a code comment, where `<ID>` is replaced by the ID of a requirement. The comment MAY also include the text of the requirement.

Automated tools SHOULD use text search to find references in this format. The full text of the requirement MAY also be included in the comment.

A code segment MAY have no reference to a requirement. Some code is not expressly required.

A code segment MAY have multiple references. Some code addressed multiple requirements.

A single requirement MAY be referenced multiple times. Some requirements need to be addressed by several different sections of code.

To fully address a specification, all bottom-level ID's MUST be referenced. A reference to a bottom-level ID is sufficient to consider the top-level as partially addressed.

In projects that use automated testing suites, references SHOULD be included with the tests and SHOULD NOT be included in operational code. Tests and requirements are closely-related concepts.

Example with a PHPUnit test:

```php
/**
 * @LWR 3.c. The get method must return an empty string when no Customer is 
 * present.
 */
function testGetReturnsEmptyString()
{
    ...
}
```

In projects without testing suites, references SHOULD be included with the operational code.

Example in JavaScript code with no automated tests:

```js
// LWR 17.a. The bullet editor interface must be shown when a bullet point is
// clicked.
$('.bullet-point').on('click', (bulletPoint) => {
    ...
});
```

## Making Changes to a Lower Speck Document

Developers SHOULD make changes to the Lower Speck document as needed.

Once a requirement has been published in a Lower Speck document, the following rules MUST be followed.

A requirement MUST NOT be removed when making changes.

A requirement's ID MUST NOT change.

A requirement with no flag section MAY have one added.

A flag section with no tokens is empty and MAY be removed.

A requirement MAY be marked obsolete by adding an `X` token to its flag section.

A requirement's text MAY be rephrased if the meaning remains the same.

A requirement's text MUST NOT change to reflect a different meaning.

An obsoleted requirement MAY have additional text to explain its reason for obsolescence.

When a requirement becomes obsolete, any code referencing it SHOULD be reviewed. References to obsoleted requirements SHOULD be removed.

An obsoleted requirement SHOULD remain obsoleted. If the requirement needs to be reintroduced, a new requirement SHOULD be written.

A requirement MAY be marked insufficient by adding an `I` token to its flag section. An insufficient requirement is one that is expected to have sub-requirements added later.

A requirement MAY be unmarked insufficient by removing the `I` token from its flag section.

Blank lines MAY be removed or added.

## Justification

The primary purpose of Lower Speck is to establish a list of requirements and reference them from the software code.

This is achieved by giving each requirement a permanent ID. Therefore, it's important that no requirements be deleted from the list. Instead they are flagged obsolete.

The rest of the specification mostly ensures that the list is well-defined so that it can be easily verified by both humans and software.

## TO DO

Need More Examples.

## About

Lower Speck is authored by <a href="http://dankuck.github.io/">Daniel Kuck-Alvarez</a>.

Released under a <a href="http://creativecommons.org/licenses/by/3.0/">Creative Commons - CC BY 3.0</a> license.
