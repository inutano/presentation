# Workflows that run everywhere and where to run them

#### Runtime metrics analysis for workflow deployment


Tazro Ohta, Database Center for Life Science (DBCLS)

![](images/dbcls.png)

---

# Workflows are now portable

- Tools are packaged in containers
- Workflows are written in Common Workflow Language
- Good bye to `git clone` `make` `stackoverflow`

![center](images/morpheus.jpg)

---

# *EVERYWHERE* means options

**Where** should I run my workflow?

- Laptop/Desktop
- Shared computing cluster
- Cloud platforms
  - General instance
  - Compute optimized
  - Memory optimized
  - Storage optimized

---

# Know your workflows

To run them at the best performance, you should know:

- Runtime metrics (resource usage)
  - Processing time
  - CPU/Memory usage
  - Block I/O
  - Network I/O
- Performance with relation to
  - inputs
    - data size / file size
    - parameters / arguments
  - environment/hardware

---

# CWL-metrics: Runtime metrics analysis

![50%](images/RUNCWL_logo.png)

- A system to capture runtime metrics via Docker API
- Analyze metrics with workflow metadata such as Inputs
- github.com/inutano/cwl-metrics or google 'cwl-metrics'


---

# How to use

1. Wrap your tools in Docker containers
2. Write CWL of your tools/workflow
3. Install CWL-metrics and Run
    - `curl -L "https://tinyurl.com/cwl-metrics" | bash`
    - will install CWL-metrics and run daemon process
4. Exec `cwltool` to run your workflow with specified options
5. `cwl-metrics fetch` to get summarized runtime metrics

---

![center 30%](images/cwl-metrics-01.png)

---

# How it works

![center 100%](images/cwl-metrics-02.png)

---

# The data it captures

[Full list](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/docker) at [influxdata/telegraf](https://github.com/influxdata/telegraf)

- docker daemon info: assigned cpus, mems, #containers, etc.
- docker container info: pid, exitcode, started/ended at, etc.
- mem: max usage, total usage, cache, etc.
- cpu: total usage, percent usage, user/kernel, etc.
- network: receive/transmit bytes, packets, errors, etc.
- block I/O: read, write, total, etc.

---

# Analysis of runtime metrics

- `cwl-metrics fetch`
  - client for elasticsearch
  - outputs summarized JSON or TSV data
- Use Kibana to visualize raw data
- Use elasticsearch API directly from command line

---

# RNA-Seq workflow comparison

- doi.org/10.1101/456756 or Search 'cwl-metrics' on [bioRxiv](https://www.biorxiv.org/search/cwl-metrics)
- Materials
  - 7 workflows at [pitagora-galaxy/cwl](https://github.com/pitagora-galaxy/cwl)
  - 9 samples of different #reads and length from SRA
  - 6 different AWS instances
    - m5/c5/r5
    - 2xlarge and 4xlarge

---

# HiSAT2-StringTie workflow (Time, SE/PE)

![center](images/tool-for-samples.png)

---

# Comparison of workflows (Time/Mem)

![center](images/sample-for-tools.png)

---

# Comparison of metrics and cost per run

![center](images/cost-table.png)

---

# Future plan

- Resource prediction using stored data
- Improve implementation
  - less dependencies
  - work with other containers
- Integrate with Provenance
  - put metrics information in provenance object

---

# Share your workflow by CWL!

We will help to collect the metrics!