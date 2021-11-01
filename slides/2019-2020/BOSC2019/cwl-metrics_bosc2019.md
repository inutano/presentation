# Collecting runtime metrics of genome analysis workflows by CWL-metrics

Tazro Ohta (DBCLS)
Tomoya Tanjo (NII)
Osamu Ogasawara (DDBJ)

![]()
![]()

<font size=5><b>Acknowledgement:</b> Prof. Kento Aida and the Inter-Cloud CREST team, and the open source communities: Pitagora Network, Galaxy Project, Common Worklow Language, Bioinformatics Open Source Conference, and the BioHackathon. The system was implemented and tested on the NIG supercomputer system at the ROIS National Institute of Genetics.</font>

---

# Background

![center](images/metrics.fig1.png)

* A **dynamic resource allocation** system built on our platform
* It requires **resource prediction function** to estimate a suitable instance for given workflows
    * need **training data** for resource prediction

---

# CWL-metrics: a utility tool for cwltool

![](images/metrics_fig1.png)

* Daemon process gets step info from cwltool debug output
* Telegraf records resource usage for each Docker container
* Metrics are sent to Elasticsearch (ES)
    * Use central ES server to collect data from distributed nodes

---

# Usage

<font size=4>

```
$ curl "https://raw.githubusercontent.com/inutano/cwl-metrics/master/bin/cwl-metrics" | bash
$ cwltool --debug --leave-container --timestamps --compute-checksum --record-container-id \
   --cidfile-dir $(pwd)/result --outdir $(pwd)/result kallisto.cwl kallisto.yml 2> $(pwd)/result/cwltool.log
$ cwl-metrics fetch json | jq .
{
	"CWL-metrics":[
	{
	  	"workflow_id":"48813280-5990-11e8-9693-0aafe96a2914",
	  	"workflow_name":"KallistoWorkflow-se.cwl",
	  	"platform":{
	  		"instance_type":"m5.2xlarge",
	  		"region":"us-east-1a",
	  		"hostname":"ip-172-31-10-231.ec2.internal"
	  	},
	  	"steps":{
	  		"135df0da59c968f22d1e394c9412cb9c3fa4580cf62616790ff79ffa162c7911":{
	  			"stepname":"kallisto_quant",
	  			"container_name":"yyabuki/kallisto:0.43.1",
	  			"tool_version":"0.43.1",
	  			"tool_status":"success",
	  			"input_files":{
	  				"SRR1274306.fastq":229279368,
	  				"GRCh38Gencode":2836547930
	  			},
	  			"metrics":{
	  				"cpu_total_percent":99.7522093765586,
	  				"memory_max_usage":4053995520,
	  				"memory_cache":152821760,
	  				"blkio_total_bytes":51630080,
	  				"elapsed_time":40
	  			}
	  		}
		}
	}]
}
```

</font>

---

# Example use case: comparison of RNA-seq workflows

![center](images/metrics_fig2.png)

Duration and memory usage by 7 different workflows 

---

# Challenges

- Singularity support (WIP)
- More workflow runners other than cwltool
  - require a standard format for workflow execution logs
- Sharing workflows with resource requirements
  - require a standard format for summary of the metrics

# Resource

- https://inutano.github.io/cwl-metrics (MIT license)
- Tazro Ohta, Tomoya Tanjo, Osamu Ogasawara. Accumulating computational resource usage of genomic data analysis work ow to optimize cloud computing instance selection. *GigaScience*. 2019 doi: 10.1093/gigascience/giz052

---

# AD: NBDC/DBCLS BioHackathon 2019

![center 50%](images/bh19-logo.png)

- 120h long hackathon for `(data|tool|database)` developers
- September 1st to 7th  in Fukuoka, Japan
- http://2019.biohackathon.org/
  - Register now!
