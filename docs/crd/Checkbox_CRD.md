---
id: checkbox
name: Checkbox
version: 0.1.2
format: 2
lifecycle: backlog
tier: core
composition: basic
category: forms
status:
  requirements: in_progress
  design_specs: not_started
  implementation: not_started
  docs_guidance: in_progress
figma:
docs_site:
related_crds:
  dependency: []
  precedent: []
last_updated: 2026-11-25
---

# CRD: Checkbox

---

# 1 · Requirements

## Purpose

A single yes/no control. People use it to pick any number of options in a form, confirm
something before submitting ("I agree to the terms"), or select rows in tables and lists.

## Scope

**In scope:**

- One checkbox, with or without a visible label
- Options in a form, alone or grouped
- Standalone confirmations
- Row selection in tables and lists, including a "select all" parent

**Out of scope:**

- Group label and group error: Checkbox group
- Description, error message and required marker: Field
- A setting that takes effect immediately: Switch
- One choice from a set: Radio

## Anatomy

- **Box**: the square control that holds the value
- **Indicator**: the mark inside the box: a tick when checked, a dash when mixed, nothing when
  unchecked
- **Label**: the text after the box. Optional
- **Link**: consumer content inside the label. Optional

## Functional requirements

* F1: A checkbox holds one of three values: unchecked, checked or mixed.
* F2: Activating an unchecked checkbox makes it checked.
* F3: Activating a checked checkbox makes it unchecked.
* F4: Activating a mixed checkbox makes it checked.
* F5: Only the consumer sets mixed. Activation never produces it.
* F6: The label sits after the box.
* F7: A long label wraps. It never truncates.
* F8: When the label wraps, the box aligns with its first line.
* F9: The label may contain a link.
* F10: The person can't change a disabled checkbox's value.

## States

* S1: Every state exists for each value: unchecked, checked and mixed.
* S2: Default: at rest.
* S3: Hover: the pointer is over the box, the label or between them.
* S4: Pressed: the pointer is held down on the box, the label or between them.
* S5: Focus: the checkbox has keyboard focus.
* S6: Disabled (F10).
* S7: Error: the box shows an error treatment.
* S8: Error and disabled never combine.

## Behaviour

* B1: Clicking the box, the label or between them toggles the value.
* B2: Clicking the link follows it and leaves the value unchanged.
* B3: [review] On a value change, the box fill and the indicator transition in on check and out
  on uncheck.
* B4: Under reduced motion, a value change jumps straight to the end state.

## Content

## Accessibility

* A1: The mixed value sets the box's `indeterminate` property, so it is announced as mixed.
* A2: The indicator is decorative and hidden from assistive technology.

## Integration

**Composition rules:**

**Children:** none. The indicator's tick is the check icon; its dash is the minus icon.

**Used in:** Checkbox group, Field, tables and lists

## Ruled out

- A second size: web only, and no evidenced need yet.
- A read-only state: native checkboxes ignore `readonly`. Show the value as text instead.
- The label before the box: that settings-list pattern wants a Switch.
- Truncating the label: it would hide a confirmation's terms.
- Mixed becoming unchecked on activation: surprises people expecting "select all".
- Cycling back to mixed: the consumer would have to remember the earlier partial selection, and
  people rarely understand it.
- Description, error message and required marker as Checkbox parts: Field owns them, so
  Checkbox stays a single control.
- A box-only click target: B2 handles links in the label instead.

## Open questions

| Question | Owner | By | Status |
|---|---|---|---|

## Notes

The rule that Field and Checkbox group set S7's error state belongs in their CRDs.

---

# 2 · Design specifications

## Properties in Figma

| Property | Type | Default | Options | Description |
|---|---|---|---|---|

## Design decisions

* 2026-11-25: Colours come from a Component-tier set shared with Radio and Switch: controls
  carry too many states for Semantic (token conventions § Which tier, step 2).
* 2026-11-25: The label is optional (Anatomy), so row selection uses Checkbox rather than a
  separate control.
* 2026-11-25: The box shows an error state (S7), so a lone confirmation shows the problem where
  the person acts. The Field's message is the second cue.
* 2026-11-25: S8: a disabled checkbox can't be fixed, so an error on it only frustrates.
* 2026-11-25: Checkbox stays `composition: basic` even if a Link sits in the label (F9): the
  link is consumer content, which Checkbox doesn't render or own.

---

# 3 · Implementation

## Implementation decisions

## Dev notes & deviations

---

# 4 · Documentation guidance

## Usage

**When to use:**

- Choosing any number of independent options
- Confirming something before submitting, such as accepting terms
- Selecting rows in a table or list

**When not to use:**

- The change should apply immediately, with no submit: use Switch
- Only one option can be chosen: use Radio

**Patterns:**

- "Select all": a parent checkbox shows mixed while some, but not all, of its children are
  checked (F5).

**Content:**

- Without a visible label, the accessible name says which row it selects: "Select invoice 42",
  not "Select".

## Gotchas

- When you set mixed, also clear the underlying checked value. Otherwise the native element
  activates mixed to unchecked, not checked (F4).

---
