---
marp: true
---

# Sapporo: an implementation of the GA4GH Workflow Execution Service standard

**Tazro Ohta** (Database Center for Life Science, Japan)

2021-09-13
Workshop: Federating computational analyses with GA4GH standards
[BC]2: Basel Computational Biology Conference

---
<!-- paginate: true -->
<!-- footer: github.com/ddbj/sapporo -->

<style>
footer a {
  color: gray;
  text-decoration: none;
}
</style>


# Acknowledgement

- The Sapporo team: Hirotaka Suetake (main developer), Manabu Ishii, Tomoya Tanjo
- The DDBJ Human Genome working group 
- Prof. Takeo Igarashi and Dr. Tsukasa Fukusato (UTokyo)
- Open-source communities
  - Workflow Meetup Japan
  - BioHackathon Europe and Japan
  - Workflow language and framework communities
- The organizers of [BC]2 !! :bow:

---

# Background

Many barriers to re-using published workflows, one needs to:

- Install an appropriate workflow runner
- Connect the runner with the suitable computing cluster
- Edit the input parameters for their analysis
- Modify the workflow for a different purpose

**...For many different workflow languages!**

---

# When someone gets you a workflow written in a language you're not fluent in:

![h:500px center](images/sapporo-components-language-gap.png)

---

# Solution: Sapporo

- an implementation of the GA4GH WES standard
- Two components:
  - lightweight API server
  - browser-based GUI
- **supports multiple workflow runners**
    - `cwltool`, `nextflow`, `cromwell`, `snakemake`

![bg 100% right:35%](images/sapporo-components-WaaS.png)

---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
</style>

# Inside Sapporo

![h:500px center](images/sapporo-components-sapporo-service.png)

---

# Manage workflows and runs via Sapporo-web

![h:600px center](images/sapporo-web.png)

---

# Power of standards

- Multiple cloud-oriented standards by GA4GH
  - WES (Workflows), TES (Job), TRS (Tools), DRS (Data)
- Abstraction of implementation layer
  - Each computing environment has a different setup
  - Each workflow service must have a different implementation strategy
  - **Different inside, Same surface: Better interoperability**

---

# Challenges

To fully bridge a gap between language communities, a WES needs to:

- :white_check_mark: support installation and deployment of appropriate runner
- :white_check_mark: provide common interface for workflow invocation
- :white_large_square: **provide common interface for parameter editing**
- :white_large_square: **support staging of files and directories**

*To lower the learning cost of users, standards may need to improve*

---

# Thank you!

- Project documentation: https://github.com/ddbj/sapporo
- WES server source code repository: https://github.com/ddbj/sapporo-service
- Web GUI source code repository: https://github.com/ddbj/sapporo-web
- Public web GUI (require running WES server): https://ddbj.github.io/sapporo-web
- Hands-on Tutorial: https://ddbj.github.io/sapporo/GettingStarted


