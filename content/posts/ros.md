---
author: Ayman DAMOUN
title: Robot Operating System
date: 2022-03-08
description: Notes that I took while taking hello (real) world with ros – robot operating system MOOC.
math: true
---
In the following post I will present my notes of the course  hello (real) world with ros – robot operating system.
The course can be found at coursera [Link](https://www.coursera.org/learn/machine-learning). In addition the material and my assignment solutions are on my github repository [Link](https://www.coursera.org/learn/machine-learning). So let's start!
{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}
<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}

# Vocabulary
In this section, I will give some definitions related to
- **ROS Node**:
A ROS node is a data or information processing software unit. All functional requirements for a ROS application will be implemented as ROS Nodes. ROS Node is implemented in Python or C++ and the idea of ROS nodes ensures that we can have functional modularity in large ROS projects. In other words, ROS nodes are building blocks in the context of a large software application.

- **ROS Topic**: A ROS topic is an entity that is used to  transport information between nodes.