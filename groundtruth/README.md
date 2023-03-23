## Folder Description

This folder contains the ground truths and functional dependencies (preprocessing step in synthesized KB) in the form of pickle files. We have provided the files for SANTOS Large (real), SANTOS Small (santos) and TUS benchmark. If you want to run SANTOS over other benchmarks, you need to add these files for each of them.

## Generating Ground truth files for New Benchmark

To create ground truth files, first you need to manually label (i) the intent columns of each query table and (ii) the set of data lake tables that are unionable with the query table. Along with the [benchmarks](https://zenodo.org/record/7758091) we release in Zenodo, you can find csv files that contains labeling of TUS benchmark (/TUS_benchmark_relabeled_groundtruth.csv) and SANTOS Small Benchmark (santos_benchmark/santos_small_benchmark_groundtruth.csv). Once you have these information, create two pickle files as described below and upload them to this folder. Note that you should also upload the benchmark tables. Find details in [benchmark](../benchmark/) folder. 

### Creating ground truth pickle files 

1. [Benchmark_Name]IntentColumnBenchmark.pickle file is a python dictionary that contains the name of query tables as key and the index of intent column as value. For example for a benchmark named "test" having two query tables data_mill_a.csv (intent column index = 0) and cihr_co-applicant_b.csv (intent column index = 1), we create a pickle file named testIntentColumnBenchmark.pickle that persists a python dictionary as follows:
    ```
    {   
        'data_mill_a': 0,
        'cihr_co-applicant_b': 5
    }
    ```
2. [Benchmark_Name]UnionBenchmark.pickle file is a python dictionary that contains the name of query tables as key and the list of their unionable tables as value. For example for a benchmark named "test" having a query table "data_mill_a.csv" with two unionable tables "data_mill_0.csv" and "data_mill_1.csv" and another query table "cihr_co-applicant_b.csv" with three unionable tables "cihr_co-applicant_1.csv", "cihr_co-applicant_2.csv" and "cihr_co-applicant_3.csv", we create a pickle file named testIntentColumnBenchmark.pickle that persists a python dictionary as follows:
    ```
    {
        'data_mill_a.csv': ['data_mill_0.csv', 'data_mill_1.csv'],
        'cihr_co-applicant_b.csv': ['cihr_co-applicant_1.csv', 'cihr_co-applicant_2.csv', 'cihr_co-applicant_3.csv']
    }
    ```

### Creating functional dependencies file

In SANTOS, we find functional dependencies using [Metanome](https://hpi.de/naumann/projects/data-profiling-and-analytics/metanome-data-profiling.html) package. See [Functional Dependency Discovery: An Experimental Evaluation of Seven Algorithms](https://dl.acm.org/doi/pdf/10.14778/2794367.2794377) and [Repeatability - FDs and ODs](https://hpi.de/naumann/projects/repeatability/data-profiling/fds.html) for additional details. You can find the executable files and a python script to generate the pickle file [here](https://drive.google.com/drive/folders/1kNEkIWXYUh4FpLEiro4YMsQBkW-7FpQo?usp=share_link).
