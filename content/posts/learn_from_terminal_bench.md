---
date: '2025-11-18T09:21:58-08:00'
title: 'Learn from Terminal Bench'
draft: true
categories: ["AI"]
tags: ["LLM", "agent"]
---

After several days of learning from [**terminal bench**](https://github.com/laude-institute/terminal-bench/), I think that I need to note and summary what I learnt from the project.

## What is Terminal Bench

Terminal-Bench is the benchmark for testing AI agents in real terminal environments. From compiling code to training models and setting up servers, Terminal-Bench evaluates how well agents can handle real-world, end-to-end tasks - autonomously.

**How it work:** The teriminal bench repo is a falsework, it build a simple terminal agent framework, **Terminus**, can process with tmux session in a docker container. It also use liteLLM to manage all LLM server for unified evaluation. After the falsework have built, a task contributer only need to create a task follow the task template. It include 4 main needs:
1. *task.yaml:* task description (prompt); 
2. *docker-compose.yaml & Dockerfile:* docker enviorment setup for run time toolkit preparation; 
3. *solution.sh:* oracle solution (make sure the provided task can be solved in terminal); 
4. *run-tests.sh & tests/test_outputs.py:* pytest script to verify the solution result.

## What I Have Got

- AI agents already can do so many hard tasks in programming (this amazing oberservation may change AI future), emm~ Certainty can be verified by pytest tasks.
- **uv** is a new tool to manage python packages, better and faster then pip.
- Github action is a good PR and CI tool. 😘 (Using yaml and simple shell, you can manage what to do after you push to github )
  - Auto code reviewer assignment
  - Auto code check (format **ruff** and quality checker **claude review**)
  - LLM code review (claude and gemini)
  - Auto multi agent process new task add to the bench. (yaml call from a script in sub-foler *scripts_bach/test-modified-tasks.sh* or *scripts_python*) 
  
- Code agent can do code review, with the PR and CI pipline in github action, this unleashes a lot of automated coding potential.
- Terminal Bench build an agent called **Terminus**. All the task can prcessed in docker container and process sub-feedback can get from a python package of a simulation tmux session. That's a good sandbox for safety LLM-Agent evaluation.
- Build a pipline/workflow and everyone can collaborate more easily.
