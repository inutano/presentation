# Improve portability of bioinformatics software across HPC and cloud infrastructures

**6th International IBM Cloud Academy Conference 2018**
25 May 2018 @ The Institute of Statistical Mathematics

[]()
[]()

Tazro Ohta, Database Center for Life Science
Tomoya Tanjo, National Institute of Informatics
Osamu Ogasawara, National Institute of Genetics

![affiliation logos](images/institutes_logos.png)

---

# Acknowledgement :pray:

- Intercloud CREST group
- Staff of DDBJ and DBCLS
- Galaxy Community Japan
- Community members of Galaxy, CWL, and OBF

---

# Background

"Genomics as a big data science"

---

# Many samples for many purposes :microscope:

Unlike the other area, bioinformatics data analysis comes with

- Data explosion
  - 100MB-100GB per sample
  - 10-100,000 samples per research
  - Large-scale int'l collaborations / many individual projects
- Thousands of software tools
  - Open source command line tools from individual developers
- "Workflow" to connect tools and iterate for samples
  - "Routinely unique"

---

# #tools > 2,000

![bioconda recipes center](images/biconda.png)

---

# Routinely unique

![routinely unique center](images/routinely_unique.jpg)

- 46 data analysis projects in 18 months required 34 different types of analysis
- "Many projects required customized techniques that used only once"

<span style="font-size:80%">[Chang J. (2015) Core services: Reward bioinformaticians. *Nature*](http://doi.org/10.1038/520151a)</span>

---

# Routines breakdown

- Set up servers
- Install and configure tools and workflows
- Transfer data
- Fetch reference data from the public databases
- Manage preprocessing jobs
- Set up interactive environment for statistics (e.g. Jupyter)
- Collect and keep result data
- **Repeat on reviewer's demand :innocent:**

*Can clouds help us to reduce the cost of the routines?*

---

# Packaging bioinformatics tools and workflows

Getting out of dependencies hell

---

# Packaging tools

- Efforts for years to containerize tools
- Containers are now provided for most of popular tools
  - [biocontainers](http://biocontainers.pro/)
  - [bioboxes](http://bioboxes.org)
- Ongoing trials for other containers for HPC
  - udocker
  - singularity

![container_logos center](images/container_logos.png)

---

# Benchmark: native vs docker

![https://doi.org/10.7717/peerj.1273/table-1](images/table_di_Paolo.png)

- Native vs Docker execution benchmark comparison
- "the observed standard deviation is smaller when running with Docker"

<span style="font-size:80%">[Di Tommaso P, et al. (2015) The impact of Docker containers on the performance of genomic pipelines. *PeerJ*](https://doi.org/10.7717/peerj.1273)</span>

---

# Packaging workflows

![workflow center 120%](images/workflow.png)

[]()
[]()

- Tools are often used as components of a workflow
- Everyone has their favorite wf job management software;
  - Galaxy, Taberna, Airflow, Nextflow, Cromwell, and.. **shell**
- Sharing workflows among the different environments is hard

---

![Common Workflow Language](https://cdn.rawgit.com/common-workflow-language/logo/0b98d341/CWL-Logo-nofonts.svg)

### The age of Common Workflow Language

- "A specification for describing analysis workflows and tools"
- A new open-source community standard since 2014
  - for all data analysis tasks, not only bioinformatics
- describes structure of tools and workflows in YAML
  - base container image, base command, input/output

---

# CWL: how it works

- Requirements
  - tool and workflow definition files (.cwl)
  - job configuration file (.yaml or .json)
  - workflow engine that supports CWL execution

---

# CWL in action - tool definition

```
cwlVersion: v1.0
class: CommandLineTool
hints:
  DockerRequirement:
    dockerPull: inutano/rsem:0.1.0
baseCommand: ["rsem-calculate-expression"]
inputs:
  threads:
    type: int
    inputBinding:
      prefix: -p
  fastq:
    type: File
    inputBinding:
      position: 1
outputs:
  readsPerGene:
    type: File
    outputBinding:
      glob: "*ReadsPerGene.out.tab"
```

---

# CWL in action - workflow definition

```
cwlVersion: v1.0
class: Workflow
inputs:
  runThreadN: int
  dataURL: string
outputs:
  readsPerGene:
    type: File
    outputSource: rsem/readsPerGene
steps:
  download_data:
    run: download_data.cwl
    in:
      dataURL: dataURL
    out: [dataFiles]
  rsem:
    run: rsem.cwl
    in:
      threads: runThreadN
      data: download/dataFiles
    out: [readsPerGene]
```

---

# CWL in action - job configuration

```yaml
runThreadN: 8
dataURL: ftp.ddbj.nig.ac.jp/pathto/example.fastq
```

---

# CWL in action - execution

using CWL reference implementation ([cwltool](https://github.com/common-workflow-language/cwltool)):

```
$ cwltool rsem_workflow.cwl rsem_workflow_jobconf.yml
```

### Basic idea

- CWL focuses on "What" of workflow
  - structure of workflow incudling input, action, and output
- "How" should be determined by execution environment
  - job scheduling and management are depending on engines

---

# Implementations supporting CWL

|Software|Platform support|
|:---:|:---|
|cwltool|Linux, OS X, Windows, local execution only|
|Arvados|AWS, GCP, Azure, Slurm|
|Toil|AWS, Azure, GCP, Grid Engine, LSF, Mesos, OpenStack, Slurm, PBS/Torque|
|Rabix Bunny|Linux, OS X, GA4GH TES (experimental)|
|CWL-Airflow|Linux, OS X|
|REANA|Kubernetes, CERN OpenStack (OpenStack Magnum)|
|Cromwell|local, HPC, Google, HtCondor|
|CWLEXEC|IBM Spectrum LSF 10.1.0.3+|

---

OK now everything's portable...
So ***where*** should I run my workflows?

---

# Select the best instance for given WF

An ideal system to optimize cloud instance selection will require **resource usage data of past WF executions**

![diagram of optimization function center 130%](images/instance_selection.png)

---

# Collecting resource usage of data analysis workflows

---

# CWL-metrics

- github.com/inutano/cwl-metrics
  - collects container resource usage including
    - total CPU usage
    - max memory usage
    - total disk IO
    - exec time
  - collects metadata of tools and workflows via cwltool
- easy to install, run (almost) everywhere

---

# CWL-metrics: How it works

- collect metrics data via influxdata/telegraf
- collect WF metadata via cwltool
- store in elasticsearch, output summary data

![diagram center 130%](images/cwl-metrics.png)

---

# Example: WFs on different instance type

![some nice plots center 30%](images/comparison.png)

---

# Future work

- A compact summary file format taken with CWL file
- Support more workflow engines
- Support multihost environment
- Support containers other than docker

# Summary

- Genomics need more machines, more easy-to-use clouds
- Packaging tools and workflows for easy migration to the clouds
- Collecting data for environment selection optimization
  - Need more metrics data of wider variety of workflows
