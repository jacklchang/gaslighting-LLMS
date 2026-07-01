# Do Prompt-Defined Personas Hold? Auditing Multi-Agent LLM Systems with Persona Vectors

## Motivation

Multi-agent LLM systems increasingly rely on prompt-defined personas to simulate diverse perspectives, stress-test ideas, and approximate human deliberation. The implicit assumption is that a character sketch reliably steers an agent's reasoning throughout a session. However, we cannot confidently say whether agents defined by distinct personas actually maintain internal distinctiveness across turns, or whether their representations converge toward a shared mean as the context window fills with other agents' outputs.

If convergence happens, the diversity guarantees that multi-agent systems advertise are weaker than claimed. This has direct implications for AI alignment more broadly: deliberative multi-agent architectures are being proposed as tools for value pluralism, red-teaming, and oversight. If the agents are silently converging, these functions degrade without any visible signal at the behavioral level.

## Research Question

Do prompt-defined personas in multi-agent LLM systems maintain representational distinctiveness in activation space across turns, or do they converge toward a shared internal representation as the session progresses?

## Method

I will run structured multi-agent brainstorming sessions using the Virtual Roundtable architecture (Dorn et al., 2026), with agents assigned maximally distinct character sketches. Using the automated persona vector pipeline from Chen et al. (2025), I will extract a persona direction for each agent from its character sketch alone, then project each agent's hidden states onto its persona vector at every turn. This produces a turn-by-turn fidelity score per agent. I will then test whether fidelity scores converge across agents over time, and whether convergence correlates with reduced semantic diversity in session outputs.
