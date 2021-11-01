
# SAPPORO: workflow management system that supports continuous testing of workflows

Hirotaka Suetake (The University of Tokyo)
Tazro Ohta (DBCLS)



![]()
![]()

<font size=5><b>Acknowledgement:</b> Prof. Masanori Arita, Prof. Atsushi Shimizu, Dr. Yuichi Kodama, Dr. Osamu Ogasawara (DDBJ), Dr. Hidemasa Bono (DBCLS), Prof. Takeo Igarashi, Dr. Tsukasa Fukusato (The University of Tokyo), and the Workflow Meetup community in Japan. This work is supported by DDBJ.</font>

---

# Background

* DNA Databank of Japan (DDBJ) provides JGA, a database for human genotype and phenotype
    * a counterpart of NCBI's dbGaP or EBI's EGA
* Users demand an interface to analyze the data without CUI
* Need a system that is user-friendly, reliable, and **secure data handling** 

---

# Design concept

**1. Data security rather than flexibility**

* Prevent users to move/delete the data during the process
* Users only select input data ID for predefined workflows

**2. Reduce the cost of development**

* No more workflow language, no more workflow runner
    * Use existing WF langs, runners, and API standard

**3. Ensure the reliability of the predefined workflows**

* Continuous testing of predefined workflows

---

# Overview: WF Manager/Computing/Data

![center 23%](images/SAPPORO_slide_fig2.png)

---

# Software architecture

![center](images/SAPPORO_slide_fig1.png)

* 3 components: Service, Web, Fileserver 
* Easy deploy by docker-compose
* Only admins can register workflows in SAPPORO-service
* Workflows fetch input data, export output data
* Sapporo-web automatically check if the registered workflows are working correctly

---

# Web UI: Select workflow

![SAPPORO - Workflow center 35%](https://i.imgur.com/qKk1oxz.png)

---

# Web UI: Prepare run

![prepare workflow center](https://i.imgur.com/MXW3cn3.png)

---

# Web UI: Manage running workflow

![SAPPORO - Run center 35%](https://i.imgur.com/qlvyMbt.png)

---

# Challenges

* A new test framework integration
    * developing as a CLI application
    * not to just check exit code is `0`, also test for output data consistency and for failing test cases

# Documentation and Source code

- by MIT License on GitHub [suecharo/SAPPORO](https://github.com/suecharo/SAPPORO)
- Search for **"SAPPORO workflow"** on Google or GitHub

