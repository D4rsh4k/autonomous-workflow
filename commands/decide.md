---
name: decide
description: Human decision at a pipeline gate. Use to approve a gate, pick a design option, or provide feedback.
arguments: decision
---

# /decide $ARGUMENTS

The human is responding to a gate review in the autonomous feature development pipeline.

## Read Current State

1. Load `.build/current-run/state.json`
2. Confirm gate_status is "awaiting_human" — if not, inform the human that no gate is currently awaiting a decision and show current status.
3. Identify which gate is active from current_gate.

## Process the Decision

### Gate 1 (Spec Alignment)
**Expected:** `approved` or free-text feedback
- If `approved`: Log to gate-log.md, update state, proceed to Gate 2
- If feedback: Log feedback, route to Tony for brief revision, re-present Gate 1

### Gate 2 (Design Options)
**Expected:** `option-a` through `option-e`, or free-text feedback
- If `option-{x}`: Validate option exists, log choice, trigger teardown of unchosen routes, trigger Ive's detailed spec, proceed to Gate 3
- If feedback: Log feedback, route to Tony/Ive for revision, re-present Gate 2

### Gate 3 (Technical Contract)
**Expected:** `approved` or free-text feedback
- If `approved`: Log, proceed to Gate 3.5 (tech spec)
- If feedback: Log feedback, route to Tony/Bob for revision, re-present Gate 3

### Gate 3.5 (Tech Spec Review)
**Expected:** `approved`, `approved-with-migration`, or free-text feedback
- If `approved`: Log, proceed to Gate 4 (build + QA)
- If `approved-with-migration`: Log with explicit migration approval, proceed to Gate 4
- If feedback: Log feedback, route to Bob for revision, Jackie re-reviews, re-present Gate 3.5

### Gate 4 (QA + Review)
**Expected:** `approved` or free-text feedback
- If `approved`: Log, trigger post-Gate 4 learning loop, ask human for workflow feedback
- If feedback: Log feedback, route to Tony for fixes, Gordon re-tests, re-present Gate 4

## Error Handling

- No `state.json`: "No active pipeline run. Start one with `/build <requirement>`."
- Not awaiting human: "The pipeline isn't waiting for a decision right now. Run `/status` to see current state."
- Invalid input for gate: Inform human what's expected, ask to try again.
