# Intrusion-Detection-and-Prevention-System-IDPS
IV.	Implementation and Evaluation
1.	Tools Used
Apache Spark framework: This framework provides tools for processing large amounts of data. It uses a data abstraction technique called RDD (resilient distributed dataset) to manage distributed data on an HPC cluster and to handle errors, all in a cloud environment. Here are some important concepts and components in the structure:
●	Node (or host) - is a computer within an HPC cluster.
●	Driver (an application) - is a module containing application code and communicates with the cluster manager.
●	Master node (cluster manager) - communicates with the driver and is responsible for distributing resources to applications.
●	Worker node - is a machine capable of executing application code and maintaining an instance.
●	Context (SparkContext) - is the main entry point for Spark functions, providing an API for operations on data (e.g., broadcasting variables, creating data, etc.).
●	Executor - is a process on a worker machine that executes tasks.
●	Task - is a unit of work sent to an executor. 

Additionally, this framework provides a library called MLib. This Apache Spark machine learning library is scalable, handling distributed matrices, allowing for distributed training of Extreme Learning Machine models on a large scale.
-	Programming Language: Python.
-	Programming Tool: Visual Studio 2022.

2.	Sample Dataset:
-	We used a dataset similar to the author's - the CTU-13 dataset (containing labeled traffic in attack scenarios), specifically using scenario 8 in this dataset:

![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/010fe05b-e3f2-4fff-a8a4-bd6f7e12318c)
Figure 6. Scenarios in the dataset

-	This file is originally in .pca file format and has been processed by our group into a spreadsheet for easy viewing and analysis. Our group also added a column named "Class" indicating the class to which the traffic belongs, where "1" indicates malicious traffic, and "0" indicates benign traffic.
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/295de76d-e68b-41d2-ab39-42db90c8f4b7)

Figure 7. Spreadsheet of traffic for scenario 8

3.	Method Used:
-	First, our group processed the dataset data (originally a .pcap file containing information on netflows) and extracted the attributes of those netflows:
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/6c86f16e-2c02-4b7a-a47d-dc16bdb3a510)

Figure 8. Attribute extraction

-	The next step is to anonymize the data using the sigmoid algorithm and based on the time distance between the data, which is 1 minute (our group relies on a time window of 1 minute and the next is:
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/60326232-33b8-478b-ac23-91afa8538940)

Figure 9. Data anonymization

-	After this step, the data has been anonymized and is secure even when stolen by attackers. The next step is to calculate the output layer weight. Our group closely adhered to and implemented the algorithm through the following code snippet:
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/9be9a343-6fa3-4742-97ab-3fbfafd21f5e)

Figure 10. Computation of output layer weight

-	After this step, we will obtain a matrix β containing output layer weights. Next, we will use β (in the code snippet it is the variable beta_hat) to classify the samples:
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/ccf7f0a5-2f5c-4fec-98df-65b9d837e361)

Figure 11. Classification of samples

-	To classify the samples, we compute the sigmoid index of the values in the sample vector and set a threshold to determine whether the sample is malicious or not (over 0.5 is malicious and vice versa):
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/835763fd-1f2d-408d-9c11-68ed2512cbc2)

Figure 12. Setting threshold and classifying samples

4.	Experimental Results:
-	Confusion Matrix:
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/dc5daa59-1fad-48fe-9163-0f6a1ce88f3e)

Figure 13. Classification matrix of ELM(0.2, 1) scenario

![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/57953f1c-8243-4f78-b50f-8f4c42210052)

Figure 14. Classification matrix of ELM(0.2, 1) scenario

-	Model Evaluation by Our Group:
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/9b33f619-ccd6-4da0-b70c-cc06effa32dd)


-	Comparison with the Author's Paper:
![image](https://github.com/nguyendinhkha/Intrusion-Detection-and-Prevention-System-IDPS-/assets/82517228/31230c81-dbbe-4034-8f09-8375ef73e66c)

Figure 15. Performance of the model implemented by our group

V.	Conclusion and Future Work
This article has proposed a method for detecting attacks based on ELM technology using HPC cluster resources to train a classifier that is less time and resource consuming. The design and characteristics of ELM classification allow efficient computation and analysis of collected data in edge computing environments. The proposed method analyzes and classifies aggregate traffic flow online using NetFlows on specific edge nodes, close to the data source requiring protection. The article has presented the architecture of the proposed system and some implementation details. Specifically, the article has outlined how the process of training ELM classifiers can be separated and transferred to the cloud to leverage edge computing capabilities only for performing traffic classification based on more complex pre-built models. The article has also demonstrated the effectiveness of the proposed detection scheme through a series of experiments on real-world attack datasets.
In the future, we can enhance this system further by expanding the computing and storage capabilities of the cloud system, leading to superior computational and storage capabilities of classifiers trained on it.

VI.	References

 Kozik, R., Choraś, M., Ficco, M., & Palmieri, F. (2018). A scalable distributed machine learning approach for attack detection in edge computing environments. Journal of Parallel and Distributed Computing, 119, 18-26. https://doi.org/10.1016/j.jpdc.2018.03.006

 Garcia, S., Grill, M., Stiborek, J., & Zunino, A. (2014). An empirical comparison of botnet detection methods. Computers and Security, 45, 100-123. doi:10.1016/j.cose.2014.05.011










