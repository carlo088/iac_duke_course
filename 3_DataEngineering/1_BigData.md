## Big Data

Concurrency means multiple computations are happening at the same time. *Issue:* Python doesn't scale well in terms of concurrency, since it sticks to only 1 core.

End of Moore's law lead to new ASICs (Application-Specific Integrated Circuits): GPUs, TPUs.

##### CUDA
Software for NVIDIA's GPUs. In python, one can use **numba** (`pip install numba`). From numba one can import jit (Just In Time compiler): this takes python code, transforms it in GPU machine code and runs it. Also cuda provides the jit framework.

Concept of *Elasticity*: have an elastics infrastructure that can scale up or down according to demand.

##### Testing
Build Systems: SaaS (GitHub Actions), Open Source (Jenkins), Cloud Native (AWS Code Build).
Tools: pylint, Python Black, AWS Code Guru.
Debugging: print statements, PDB, Testing.
Continuos Delivery: SaaS (GitHub Actions), AWS Elastic Beanstalk.

### Big Data
3 Vs: Variability, Volume, Velocity. *Data Lake*: central repo for all data at any scale (S3 + AWS Glue). Data Lake accessible for ML training, streaming, on-premise ecc. *Data Pipeline, Feedback Loop*.

**AWS EMR Spark** lets you provision clusters with a certain number of nodes, with Spark installed. Stored in S3. Spark systems optimizes data processing on multiple nodes in a distributed systen, all orchestrated by a master. User can also use AWS EC2 to optmize cluster management. Then access notebook, select *PySpark* is a kernel (lets you run python code on top of Java to access Spark) and a execute code on the cluster.




