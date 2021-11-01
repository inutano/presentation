---
marp: true
---

# Sapporo: an implementation of GA4GH Workflow Execution Service standard to bridge the different workflow language communities

**Tazro Ohta** (Database Center for Life Science), **Hirotaka Suetake** (The University of Tokyo), **Manabu Ishii** (Genome Analytics Japan), **Tomoya Tanjo** (National Institute of Genetics)

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
- The organizers of OBF/BOSC and ISMB/ECCB :bow:

---

# Background: many workflows are out there..

To reuse a shared workflow, one needs to:

- Install an appropriate workflow runner
- Connect the runner with the computing cluster
- Edit the input parameters for their data
- Modify the workflow for a different purpose

**Can you do them all for any of the workflow frameworks?**

---

# When someone gets you a workflow written in a language you're not fluent in:

![h:500px center](images/sapporo-components-language-gap.png)

---

# Solution: Sapporo

- an implementation of the GA4GH WES standard
- lightweight API server and browser-based GUI
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

# Manage workflows via Sapporo-web

![h:600px center](images/sapporo-web.png)

---

# Problems all solved? No

To fully bridge a gap between language communities, a WES needs to:

- :white_check_mark: support installation and deployment of appropriate runner
- :white_check_mark: provide common interface for workflow invocation
- :white_large_square: provide common interface for parameter editing
- :white_large_square: support staging of files and directories

*The issues are between the layers of WES, workflows, and languages*

---

# Requests to the communities

---

# When you write and share a workflow:

Mind your workflow is valuable and *everyone* wants to use it!

- Follow the language's best practice
- No implicit requirements
- A workflow should be self-contained
  - Ideally just one definition file with dependencies specified by remote URLs
  - At least all in one git repository
- Sharing workflow with input examples would be very helpful
  - Use default input option to provide examples

---

# When you develop(ed) a workflow language:

Some may not edit, but just run with your framework.

- Provide a command to inspect a workflow definition file
  - It should return the input parameter scheme with type annotation
- Consider an option to pass input parameters via JSON/YAML

---

# Thanks for watching!

- Project documentation: https://github.com/ddbj/sapporo
- WES server source code repository: https://github.com/ddbj/sapporo-service
- Web GUI source code repository: https://github.com/ddbj/sapporo-web
- Public web GUI (require running WES server): https://ddbj.github.io/sapporo-web
- Hands-on Tutorial: https://ddbj.github.io/sapporo/GettingStarted


