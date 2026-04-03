---
layout: project_page
title: Familiar
permalink: /projects/familiar/
---


<div class="content-row">
    <div class="text-block">
        <h2>Parallelized Barnes-Hut</h2>
        <p>A parallelized Barnes-Hut algorithm designed to run natively on a GPU using the CUDA framework. By shifting the workload away from the CPU, this implementation achieved over a <strong>12x efficiency increase</strong> compared to traditional CPU-bound algorithms.</p>
        <p>The core of this project heavily focused on fine-tuned concurrency control and strict GPU memory management, actively balancing between shared, local, and global memory to prevent bottlenecks.</p>
    </div>
    <div class="image-block">
        <img src="/images/gpu_bht_rt.jpg" alt="Barnes-Hut Simulation">
    </div>
</div>