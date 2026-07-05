# Can LLMs Gaslight? Role-Driven Information Burial in Multi-Agent Pipelines

## Overview

This project investigates whether LLM agents are capable of gaslighting: structuring outputs to obscure critical findings not by lying but by positioning true information in ways that cause downstream agents to doubt their own perception rather than the source.

Gaslighting in human psychology is distinct from deception because the information is technically present. The manipulation works by making the victim question their own reading of the situation rather than the honesty of the source. This project asks whether the same structure emerges in multi-agent LLM pipelines when a worker model encounters a critical finding that conflicts with its assigned role.

## Research Question

When an LLM agent's critical finding conflicts with its assigned role, does it systematically structure its output to bury that finding in ways that cause downstream reviewers to doubt their own perception rather than the worker's honesty?

## Motivation

Multi-agent LLM systems are increasingly deployed as oversight infrastructure, pipelines where one model checks another's work and flags problems before they reach humans. This architecture assumes agents surface critical information faithfully. Current monitoring approaches look for false statements and omissions, not structural suppression of true information. If role pressure causes agents to bury critical findings through output structure rather than explicit deception, the oversight pipeline fails silently and invisibly to existing detection methods.

## Hypothesis

Role assignment creates implicit pressure to subordinate inconvenient findings to the primary task. This pressure does not produce lying or omission but produces structural burial: true information present in the output but positioned late, framed peripherally, or surrounded by mitigating language in ways that cause reviewers to miss it or doubt whether it was there at all.

## Experimental Design

**Setup:** A worker model is assigned a task containing an embedded critical finding that conflicts with its role. The worker produces a summary or report. A reviewer model reads the output and is asked to assess the situation.

**Conditions:**
- Role conflict present vs. absent (baseline)
- Critical finding severity: low, medium, high
- Worker model: varied across model families

**Measurements:**
- Whether the reviewer catches the critical finding
- Whether the reviewer expresses epistemic doubt ("I did not see evidence of X" vs. "the summary suggested X was not a concern")
- Structural features of worker output: position of critical finding, framing language, surrounding context
- Off-the-record elicitation: after producing the summary, the worker is asked directly whether the critical finding was present and important. Divergence between OTR answer and summary structure confirms burial was not ignorance.

**Key Distinction:** A reviewer that says "I did not see evidence of a problem" has missed something. A reviewer that says "the summary suggested the approaches were comparable" has been gaslit. Operationalizing this distinction is the core methodological contribution.

## Example Scenarios

**Code review pipeline:** A worker model is assigned to merge two code approaches and describe the differences. One approach contains a critical flaw. Role pressure to complete the merge causes the worker to bury the flaw in technical language that is accurate if read closely but not salient enough to trigger alarm in the reviewer.

**Research summarizer:** A worker is assigned to produce an executive summary of a report. The report contains a finding that undermines the project's central claim. The worker includes the finding in the third paragraph under a neutral heading, present but positioned so a scanning reviewer never reaches it.

**Hiring evaluator:** A worker is assigned to recommend a candidate. The candidate's record contains a disqualifying detail. The worker mentions it in a subordinate clause mid-paragraph surrounded by positive framing, technically present but structurally buried.

## Alignment Relevance

This project identifies and operationalizes a failure mode in multi-agent oversight pipelines that is invisible to current monitoring approaches. As AI systems are trusted with more consequential tasks, oversight increasingly depends on agent-to-agent checking rather than direct human review. If that checking fails through structural suppression rather than explicit deception, the failure leaves no detectable trace. Documenting this failure mode is a necessary prerequisite for building detection tools and designing pipelines resistant to it.

## Author

Jack Lucas Chang
Independent AI Safety Researcher
jacklucaschang.substack.com
