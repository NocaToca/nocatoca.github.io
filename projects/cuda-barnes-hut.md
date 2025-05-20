---
layout: project_page
title: CUDA Barnes Hut
permalink: /projects/cuda-barnes-hut/
---

[Code](https://github.com/NocaToca/CUDA-Barnes-Hut?tab=readme-ov-file)

[Write-Up](https://docs.google.com/document/d/1a9YPQ1YdiOTFx864HNF2UlbCzCvARnTqW7a4SNW86MM/edit?tab=t.0#heading=h.n51h1yp7slig)

# Overview
While taking a CUDA course, I decided to revisit the an old idea I had. I made a simulation in Unity a long time ago that didn't have actual gravity interaction. I wanted to change this, using GPU programming to implement a more realistic n-body simulation. <br><br>

After researching common n-body algorithms, I settled on the Barnes-Hut method over brute force and fast multipole due to its balance between complexity and performance. As a brief overview, Barnes-Hut uses a hierarchical tree structure to group bodies and approximate gravitational forces, which speeds up simulations significantly by avoiding full pairwise calculations. <br><br>

Unfortunately, I did hit a snag. My AMD GPU doesn’t support CUDA! To work around this, I used Google Colab to write and test your CUDA code remotely, though limitations like no rendering and session timeouts made development difficult. This is why it's not all that pretty, as I used matplotlib after exporting the data to jsons to view my output. <br><br>

The core of the implementation involved building a Barnes-Hut tree on the GPU, calculating centers of mass, and using a distance-based threshold (theta) to decide whether to use approximations or compute direct forces. You can read a lot more about it in the report. <br><br>