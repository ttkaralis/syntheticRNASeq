# **syntheticRNASeq**

![image alt](./docs/synthetic-RNASeq_logo.png)

## **Introduction**
syntheticRNASeq is a python package that allows generation of synthetic RNA-Sequencing data by sampling a negative binomial distribution.
The output of the generators are pandas data frames with genes in rows and samples in columns.

## **Usage**

Installation (python `virtualenv` recommended):

```
virtualenv venv
source venv/bin/activate
pip install syntheticRNASeq  
```

Run it:
```
import syntheticRNASeq as synRNA
from synRNA import SingleSampleGenerator, ReplicateGenerator, MultipleSampleGenerator
```

### **Generation of a single sample**

To create a single sample we will use the *SingleSampleGenerator* class and call the *generate_single_sample* function:

```
single_sample = SingleSampleGenerator(number_of_genes = 60_000,
									  neg_binomial_n = 0.5,
									  neg_binomial_p = 0.05,
									  seed = 0)
single_sample = single_sample.generate_single_sample()
```

### **Generation of a replicates from a single sample**

To create triplicates from a single sample created from the above function we will use the *ReplicateGenerator* class and call the *get_sample_replicates* function:

```
replicates = ReplicateGenerator(normal_distribution_sigma = 1,
								df = single,
								seed = 0)
replicates = replicates.get_sample_replicates()
```

### **Generation of multiple samples**

To create multiple sample we will use the *MultipleSampleGenerator* class and call the *generate_multiple_sample* function:

```
multiple_samples = MultipleSampleGenerator(number_of_samples = 3,
										   number_of_genes = 60_000,
										   neg_binomial_n = 0.5,
										   neg_binomial_p = 0.05,
										   seed = 0)
multiple_samples = multiple_samples.generate_multiple_sample()
```

## Developer guide

Requirements:

```sh
pip install --upgrade pip
pip install build twine
```

##### Local editable install
```sh
# From repo root
python -m venv .venv
source .venv/bin/activate
pip install -e .
python -c "import syntheticRNASeq as s; print('dev ok')"
```

### Versioning

Update the version in pyproject.toml (and syntheticRNASeq/__init__.py if present). Use semver:
```
0.1.0 -> 0.1.1  # patch
0.1.0 -> 0.2.0  # minor
0.1.0 -> 1.0.0  # major
```

### Building the package
```
rm -rf dist build *.egg-info
python -m build
ls dist/
# dist/syntheticRNASeq-<version>-py3-none-any.whl
# dist/syntheticRNASeq-<version>.tar.gz
```

### Publish to TestPyPI

#### dry run
```
python -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*
# then test install in a fresh venv:
python -m venv .venv-test
source .venv-test/bin/activate
pip install -i https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple syntheticRNASeq
python -c "import syntheticRNASeq as s; print('testpypi ok')"
```

#### Publish to PyPI
```
python -m twine upload dist/*
```
##### Note

Do not commit dist/, build/, or *.egg-info/. Add to .gitignore.
