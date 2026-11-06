---
permalink: /
redirect_from:
  - /about/
  - /about.html
  - /publications/
  - /teaching/
---

## About Me

I'm a PhD student in [Electrical and Computer Engineering](https://engineering.virginia.edu/departments/electrical-and-computer-engineering) at the [University of Virginia](https://www.virginia.edu/), where I work in the [High-Performance Low-Power Lab (HPLP)](https://engineering.virginia.edu/labs-groups/high-performance-low-power-lab) with [Prof. Mircea R. Stan](https://engineering.virginia.edu/faculty/mircea-r-stan) on efficient and secure hardware for edge AI.

My work spans the full stack: RTL design, physical design through signoff and tapeout (GF12), NPU and SoC integration, compilers and runtimes, FPGA prototyping, and cycle-accurate simulation in C++.

My research centers on LLM inference accelerators and quantization–hardware co-design, alongside lightweight security primitives for resource-constrained devices.

<h2 id="news">News</h2>
<ul class="news">
{% for item in site.data.news %}
  <li><span class="news-date">{{ item.date }}</span> <span class="news-text">{{ item.text }}{% if item.link %} <a href="{% if item.link contains '://' %}{{ item.link }}{% else %}{{ item.link | relative_url }}{% endif %}">[link]</a>{% endif %}</span></li>
{% endfor %}
</ul>

## Research Interests

- **AI accelerator architecture:** LLM inference, precision-scalable datapaths, NPUs
- **Hardware–software co-design:** quantization, compilers and runtimes, design space exploration
- **Hardware security:** PUFs and cryptography

{% include publications.html %}

## Talks

<ul>
{% for talk in site.data.talks %}
  <li>{% if talk.project %}<a href="{{ talk.project | relative_url }}"><autocolor>{{ talk.title }}</autocolor></a>{% else %}{{ talk.title }}{% endif %}. <em>{{ talk.venue }}</em>, {{ talk.year }}.</li>
{% endfor %}
</ul>

<h2 id="service">Service &amp; Honors</h2>

<h4>Program Committee</h4>
<ul>
  <li>Student Program Committee, IEEE/ACM International Symposium on Microarchitecture (MICRO), 2026</li>
</ul>

<h4>Session Chair</h4>
<ul>
  <li>IEEE International Conference on RFID Technology and Applications (RFID-TA), 2024</li>
</ul>

<h4>Journal Reviewer</h4>
<ul>
  <li><em>IEEE Transactions on Computers</em></li>
  <li><em>Journal of Systems Architecture</em></li>
  <li><em>Integration, the VLSI Journal</em></li>
</ul>

<h4>Honors</h4>
<ul>
  <li>LAD'26 Fellow, International Conference on LLM-Aided Design (LAD), 2026</li>
  <li><strong>Best Paper Award</strong>, IEEE International Conference on Computer Design (ICCD), 2026</li>
  <li>DAC Young Fellow, Design Automation Conference, 2023</li>
</ul>

<h2 id="teaching">Teaching</h2>

<h4>Teaching Assistant, ECE, University of Virginia</h4>
<ul>
  <li><strong>ECE 6380</strong>: AI Hardware, Fall 2023</li>
  <li><strong>ECE 6501</strong>: Advanced Embedded Systems, Spring 2023</li>
  <li><strong>ECE 6435</strong>: Computer Architecture and Design, Spring 2022</li>
</ul>

<h4>Guest Lectures</h4>
<ul>
  <li><strong>AI Hardware and RISC-V AI Extensions</strong>, AI Hardware course, ECE, University of Virginia, 2023</li>
</ul>

<h4>Mentorship</h4>
<ul>
  <li>Mentored undergraduate researchers on AI accelerator design and FPGA-based prototyping.</li>
  <li>Mentored undergraduate researchers on PUF design and open-source silicon tapeout flows.</li>
</ul>
