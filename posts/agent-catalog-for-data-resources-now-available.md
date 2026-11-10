---
title: "Building an Agent Catalog for data resources"
date: "2026-07-21"
description: "An experiment: we built a small catalog of agent skills for data platforms on the new ARD specification, to see how agentic resource discovery holds up in practice."
category: "Engineering"
author: "Mure Team"
cover_tone: "butter"
---

When a coding agent works on a data task, someone usually decides up front which MCP servers, skills, and tools it gets, and all of them end up loaded into its context. We wanted to test the opposite: can an agent like Claude Code, Codex, or GitHub Copilot find the right capability for a data task on demand, and pull in only what it needs?

To find out, we built a small Agent Catalog for data resources. It's an experiment, not a product. The goal was to learn how resource discovery behaves with real data tooling.

## The spec we tested

The catalog implements the open [Agentic Resource Discovery (ARD) specification](https://agenticresourcediscovery.org/), developed by Microsoft, Databricks, Google, GoDaddy, Hugging Face, and GitHub among others. It was announced last month: see [Microsoft's announcement](https://commandline.microsoft.com/agentic-resource-discovery-specification-ard/) or [Google's announcement](https://developers.googleblog.com/announcing-the-agentic-resource-discovery-specification/).

The idea is simple. You describe a task in plain language, the catalog searches an index of AI data resources, and it returns ranked matches the agent can fetch from whichever registry it's pointed at. The agent loads only what the task requires, and the ranking helps a human decide what's worth installing.

## What we built

- **A registry you choose**: the catalog can point at our public registry or at a private one, and results are scoped to that source.
- **Official resources only**: we indexed around 200 skills from official sources across AWS, Databricks, dbt, DuckDB, Microsoft Fabric, Google, MotherDuck, and Snowflake. ARD also covers MCP servers and agents; we started with skills to keep the test small.
- **No auto installation**: the catalog only finds things. It never connects anything on its own, so you stay in control of what gets wired in.

## Try it

You can [browse the catalog](/agent-catalog), or install the [agent skill](https://github.com/muredata/agent-catalog) to query it from your coding agent. Because it follows the open spec, any ARD-compatible client can read the same manifest directly at [`https://muredata.com/.well-known/ai-catalog.json`](https://muredata.com/.well-known/ai-catalog.json).

We'll share what we learn as the spec and the tooling around it mature.
