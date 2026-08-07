---
date: '2025-11-16T07:57:02-08:00'
title: 'Start Using Claude-code'
draft: true
categories: ["AI"]
tags: ["LLM", "agent"]
---

AI agents are the next big breakout. Based on my recent research, only two application directions show truly remarkable potential: **deep research** and **vibe coding**. Claude Code is one of the best examples of vibe coding.

## What is Claude Code

Claude Code is an agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster by executing routine tasks, explaining complex code, and handling git workflows -- all through natural language commands. 

**Learn more in the [official documentation](https://docs.anthropic.com/en/docs/claude-code/overview)**.

## Personal Practice

Here is a guide to install, set and use claude code

### Install nodejs

After my practice, install from node is the current best way.
```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

check node and npm version
```
node -v
npm -v
```

### Install claude code

```
sudo npm install -g @anthropic-ai/claude-code
claude --version # check version
```

### Set 3rd-part API
You can use any other LLM service you want, here is an example of using kimi API.
```
export ANTHROPIC_BASE_URL="https://api.moonshot.cn/anthropic/"
export ANTHROPIC_API_KEY="sk---"
```

start using command **claude**

And now you can get the claude code, and start your vibe coding career!

![claude-code](https://github.com/anthropics/claude-code/blob/main/demo.gif?raw=true#80%)
![pngpic](images/10B_plan_png.png)
![svgpic](images/10B_roadmap.svg)
![svgpic](images/10B_roadmap.svg){width=50%}
![svgpic](images/10B_roadmap.svg){width=400px}
![svgpic](images/10B_roadmap.svg){style="max-width:300px;"}

<img src="images/10B_roadmap.svg" style="max-width: 50%;" />

![pngpic](images/10B_plan_png.png#600px)
![svgpic](images/10B_roadmap.svg#150%)


```c++
#include <stdio.h>
int main(int argc, char* argv[){
    return 0;
}

```

{{/*
  你甚至可以用它来临时隐藏一整段
  带有复杂排版或短代码的内容
*/}}

[^_metadata]: (这也是一条隐藏注释，只要正文中没有呼叫这个标签，它就不会显示)
[//]: # (这也是一种利用链接语法的简短注释)

``这也是一种利用链接语法的简短注释

In summary, Claude Code transforms your terminal into a powerful AI-driven coding assistant, streamlining your development workflow through natural language interaction and deep codebase integration.
