---
permalink: /
title: "About"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

I'm a PhD student in [Electrical and Computer Engineering](https://engineering.virginia.edu/departments/electrical-and-computer-engineering) at the [University of Virginia](https://www.virginia.edu/), where I work in the [High-Performance Low-Power Lab (HPLP)](https://engineering.virginia.edu/labs-groups/high-performance-low-power-lab) with [Prof. Mircea R. Stan](https://engineering.virginia.edu/faculty/mircea-r-stan) on efficient and secure hardware for edge AI.

My work spans the full stack: RTL design, NPU and SoC integration, compilers and runtimes, FPGA prototyping, and cycle-accurate simulation in C++. My current work centers on LLM inference accelerators and quantization–hardware co-design, alongside lightweight security primitives for resource-constrained devices.

<ul class="interest-tags" aria-label="Research areas">
  <li>AI accelerator architecture</li>
  <li>Hardware–software co-design</li>
  <li>LLM inference &amp; quantization</li>
  <li>Hardware security</li>
</ul>

Selected projects
======
<div class="feature-list">
{% assign featured = site.projects | where: "featured", true | sort: "order" %}
{% for project in featured %}
  <a class="feature" href="{{ project.url }}">
    <span class="feature__title">{{ project.title }}</span>
    <span class="feature__status">{{ project.status }}</span>
    <span class="feature__tagline">{{ project.tagline }}</span>
  </a>
{% endfor %}
</div>

[All projects &rarr;](/projects/){: .more-link}

Selected publications
======
<ol class="pub-list">
{% assign selected = site.publications | where: "selected", true | reverse %}
{% for post in selected %}{% include pub-entry.html pub=post %}{% endfor %}
</ol>

[Full publication list &rarr;](/publications/){: .more-link}

Service &amp; honors
======
<dl class="service-list">
  <dt>Program committee</dt>
  <dd>Student Program Committee, IEEE/ACM International Symposium on Microarchitecture (MICRO), 2026</dd>
  <dt>Session chair</dt>
  <dd>IEEE International Conference on RFID Technology and Applications (RFID-TA), 2024</dd>
  <dt>Journal reviewer</dt>
  <dd><i>IEEE Transactions on Computers</i>; <i>Journal of Systems Architecture</i>; <i>Integration, the VLSI Journal</i></dd>
  <dt>Honors</dt>
  <dd>DAC Young Fellow, Design Automation Conference, 2023</dd>
</dl>
