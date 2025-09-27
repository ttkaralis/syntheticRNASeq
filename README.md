# **synthetic-RNASeq**

![image alt]([https://github.com/ttkaralis/metabolite_prediction_from_gene_expression/blob/dc080d978904a063cbe90fae17a779923931d37a](https://github.com/ttkaralis/synthetic-RNASeq/synthetic-RNASeq_logo.png)

## **Introduction**
synthetic-RNASeq is a python package that allows generation of synthetic RNA-Sequencing data by sampling a negative binomial distribution.
The output of the generators are pandas data frames with genes in rows and samples in columns.

## **Usage**

Install and import the module:

```
!pip install synthetic-RNASeq  
import synthetic-RNASeq as synRNA
```

### **Generation of a single sample**

To create a single sample we will use the * *SingleSampleGenerator* * class and call the * *generate_single_sample* * function:

```
single_sample = SingleSampleGenerator(number_of_genes = 60_000,
									  neg_binomial_n = 0.5,
									  neg_binomial_p = 0.05,
									  seed = 0)
single_sample = single_sample.generate_single_sample()
```

### **Generation of a replicates from a single sample**

To create triplicates from a single sample created from the above function we will use the * *ReplicateGenerator* * class and call the * *get_sample_replicates* * function:

```
replicates = ReplicateGenerator(normal_distribution_sigma = 1,
								df = single,
								seed = 0)
replicates = replicates.get_sample_replicates()
```

### **Generation of multiple samples**

To create multiple sample we will use the * *MultipleSampleGenerator* * class and call the * *generate_multiple_sample* * function:

```
multiple_samples = MultipleSampleGenerator(number_of_samples = 3,
										   number_of_genes = 60_000,
										   neg_binomial_n = 0.5,
										   neg_binomial_p = 0.05,
										   seed = 0)
multiple_samples = multiple_samples.generate_multiple_sample()
```


