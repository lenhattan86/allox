# AlloX: Compute Allocation in Hybrid Clusters

Allox was accepted in Eurosys 2020 https://www.eurosys2020.org/program/.
* Full paper: https://dl.acm.org/doi/abs/10.1145/3342195.3387547
* Presentation slides: https://www.eurosys2020.org/wp-content/uploads/2020/04/slides/427_TanNLe_slides.pdf
* Presentation video: https://youtu.be/mO-QI7XCBPk 

# Introduction
Modern deep learning frameworks support a variety of hardware, including CPU, GPU, and other accelerators, to perform computation. In this paper, we study how to schedule jobs over such interchangeable resources – each with a different rate of computation – to optimize performance while providing fairness among users in a shared cluster. We demonstrate theoretically and empirically that existing solutions and their straightforward modifications perform poorly in the presence of interchangeable resources, which motivates the design and implementation of AlloX. At its core, AlloX transforms the scheduling problem into a min-cost bipartite matching problem and provides dynamic fair allocation over time. We theoretically prove its optimality in an ideal, offline setting and show empirically that it works well in the online scenario by incorporating with Kubernetes. Evaluations on a small-scale CPU-GPU hybrid cluster and large-scale simulations highlight that AlloX can reduce the average job completion time significantly (by up to 95% when the system load is high) while providing fairness and preventing starvation.

# How to use AlloX
There are two main components for AlloX: 
* The scheduler is implemeted based on k8s kube-scheduler. Please refer the change here https://github.com/lenhattan86/kubernetes-allox.
* Profiler: The job profiler estimates the completion times for ML training jobs. 
* Simulator: The simulator is used in the paper for the large-scale simulation https://github.com/lenhattan86/IRFsim.

How to deploy AlloX:
* Please refer https://kubernetes.io/docs/tasks/extend-kubernetes/configure-multiple-schedulers/ to deploy our scheduler. Please using the one of the docker images here https://hub.docker.com/repository/docker/lenhattan86/my-kube-scheduler for each algorithm in the paper. 
* Please use profiler to submit your ML jobs, it will submit the job samples to estimate the processing times for the jobs. Then, it submits the jobs.

Maintainer: Tan N. Le (lenhattan86@gmail.com)