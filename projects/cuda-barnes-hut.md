---
layout: project_page
title: CUDA Barnes Hut
permalink: /projects/cuda-barnes-hut/
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

<div class="content-row">
    <div class="text-block">
        <h2>The Four-Kernel Pipeline</h2>
        <p>To maximize throughput, the engine dispatches four distinct kernels per frame, capable of generating 30 frames of 12,000 bodies in under a minute. The general execution pipeline is:</p>
        <ul>
            <li><strong>Kernel 1:</strong> Filter out and combine overlapping stars to clamp the maximum tree depth.</li>
            <li><strong>Kernel 2:</strong> Traverse and find the maximum depth of the newly filtered tree.</li>
            <li><strong>CPU Step:</strong> Allocate a linear array in memory for the found tree depth.</li>
            <li><strong>Kernel 3:</strong> Populate the allocated Barnes-Hut Tree (BHT) with each node.</li>
            <li><strong>Kernel 4:</strong> Compute the updated positions and velocities of the stars.</li>
        </ul>
    </div>
    <div class="image-block">
        <img src="/images/kernel_runtimes.png" alt="Kernel Dispatch Runtimes">
    </div>
</div>

<div class="content-row">
    <div class="text-block">
        <h2>Encountered Issues</h2>
        <p>I hit a slight snag during development: without a local CUDA-enabled GPU, I had to compile and run everything through Google Colab. This created a massive roadblock for real-time visualization.</p>
        <p>To verify the physics and visualize the data, I introduced an additional CPU-bound step at the end of each frame that serialized and saved the positional data, allowing me to render the final results offline.</p>
    </div>
</div>

<div class="post-footer">
    <h3>View the Code</h3>
    <a href="https://github.com/NocaToca/CUDA-Barnes-Hut" target="_blank" class="repo-btn">
        <svg role="img" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
            <path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/>
        </svg>
        View Repository
    </a>
</div>