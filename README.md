Distributed Hadoop Cluster & Road Safety Analytics
A fully distributed 5-node Hadoop cluster built on VMware, used to analyse the 2018 UK Road Safety dataset using a custom Java MapReduce application. Developed as part of the COMP30261 Distributed Database Engineering coursework at Nottingham Trent University.

What it does
Investigates the distribution of road traffic casualties in the 2018 UK Road Safety dataset by identifying and counting accident entries associated with each casualty severity category. The analysis is performed at scale using HDFS for distributed storage and YARN + MapReduce for parallel execution across 5 nodes.

Tech Stack

Apache Hadoop 3.3.6 — Distributed storage and processing framework
HDFS — Distributed file system with block replication across nodes
YARN — Resource management and job scheduling
MapReduce (Java) — Custom job for casualty severity aggregation
Apache Spark 3.5.4 — Installed for in-memory distributed processing
Ubuntu Linux (VMware) — 5-node virtual machine cluster
Java 8 / Java 11 — Runtime environment


Cluster Architecture
NodeRolemachine01NameNode, ResourceManager, DataNode, NodeManagermachine02SecondaryNameNode, DataNode, NodeManagermachine03DataNode, NodeManagermachine04DataNode, NodeManagermachine05DataNode, NodeManager

Passwordless SSH configured across all nodes
HDFS replication factor set for fault tolerance and high availability
Firewall rules configured for all Hadoop and YARN service ports
Web interfaces enabled: NameNode UI (port 9870), ResourceManager UI (port 8088)


Configuration Files
FilePurposecore-site.xmlDefines default HDFS filesystem and NameNode hosthdfs-site.xmlReplication factor, WebHDFS, NameNode/DataNode storage directoriesmapred-site.xmlSets MapReduce framework to YARNyarn-site.xmlResourceManager host, shuffle services, NodeManager portsworkersLists all 5 nodes for daemon startup

MapReduce Job
A custom Java MapReduce application was written to:

Parse the 2018 UK Road Safety CSV dataset
Extract the casualty severity field from each record
Map each severity category to a count of 1
Reduce by aggregating total counts per severity category
Output results showing distribution of fatal, serious, and slight casualties

Running the job
bash# Upload dataset to HDFS
hdfs dfs -put road_safety_2018.csv /input/

# Run the MapReduce job
hadoop jar CasualtyAnalysis.jar cyclenest.CasualtyMapper /input /output

# View results
hdfs dfs -cat /output/part-r-00000

Key Results
The MapReduce job successfully aggregated casualty severity counts across the full dataset, demonstrating:

Correct distributed execution across all 5 nodes
HDFS block distribution and data replication working as expected
YARN container scheduling and job monitoring via ResourceManager UI
Parallel processing significantly reducing analysis time compared to single-node execution


Additional Features

Apache Spark installed across all nodes for future in-memory analytics
YARN container logs and block-level HDFS inspection available
Full multi-node file distribution and health monitoring via web UIs
Production-style architecture exceeding the minimum 3-node coursework requirement


Project Structure
DDE/
├── N1202625 - Technical Report.docx    # Full technical report with setup documentation
├── N1202625 - technical report 40%.docx # Interim report
└── N1202625 - AI Usage Form.docx       # AI usage declaration

Note: Source code not included in this repository. See technical report for full implementation details and configuration files.


Author
Vasu Goyal — Nottingham Trent University
