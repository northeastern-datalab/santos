# SANTOS: Relationship-based Semantic Table Union Search

This repository contains the implementation of our paper [SANTOS: Relationship-based Semantic Table Union Search](https://arxiv.org/abs/2209.13589), appearing at SIGMOD 2023.

Authors: Aamod Khatiwada, Grace Fan, Roee Shraga, Zixuan Chen, Wolfgang Gatterbauer, Renée J. Miller, Mirek Riedewald

## Abstract

Existing techniques for unionable table search define unionability using metadata (tables must have the same or similar schemas) or column-based metrics (for example, the values in a table should be drawn from the same domain). In this work, we introduce the use of semantic relationships between pairs of columns in a table to improve the accuracy of union search. Consequently, we introduce a new notion of unionability that considers relationships between columns, together with the semantics of columns, in a principled way. To do so, we present two new methods to discover semantic relationship between pairs of columns: The first uses an existing knowledge base (KB), the second (which we call a “synthesized KB”) uses knowledge from the data lake itself. We adopt an existing Table Union Search benchmark and present new (open) benchmarks that represent small and large real data lakes. We show that our new unionability search algorithm called SANTOS outperforms a state-of-the-art union search that uses a wide variety of column-based semantics, including word embeddings and regular expressions. We show empirically in all benchmarks that our synthesized KB improves the accuracy of union search by representing relationship semantics that may not be contained in an available KB. This result hints at a promising future of creating a synthesized KBs from data lakes with limited KB coverage and using them for union search.

## Repository Organization

- **benchmark** folder contains subfolders for Labeled Benchmark, Real Benchmark and TUS Benchmark.
- **codes** folder contains SANTOS source codes for preprocessing yago, creating synthesized knowledge base, preprocessing data lake tables using yago and querying top-k SANTOS unionable tables.
- **groundtruth** folder contains the groundtruth files used to evaluate precision and recall.
- **hashmap** folder contains indexes built during the preprocessing phase.
- **images** folder contains supplementary images submitted with the paper.
- **stats** folder contains SANTOS output files related to top-k search results and efficiency.
- **yago** folder contains the original and indexed yago files.
- **README.md** file explains the repository.
- **requirements.txt** file contains necessary packages to run the project.

## Benchmark

Please visit [this link](https://drive.google.com/drive/folders/18aYj1ZwXnp4OLIsmx9khqZD0oblMp8cs?usp=sharing) to download Real Data Lake Benchmark (aka SANTOS Large), Labeled Benchmark (aka SANTOS Small) and relabeled TUS Benchmark. The original TUS benchmark is available at [https://github.com/RJMillerLab/table-union-search-benchmark](https://github.com/RJMillerLab/table-union-search-benchmark).

## Setup

1. Clone the repo
2. CD to the repo directory. Create and activate a virtual environment for this project  
  * On macOS or Linux:
      ```
      python3 -m venv env
      source env/bin/activate
      which python
      ```
  * On windows:
      ```
      python -m venv env
      .\env\Scripts\activate.bat
      where.exe python
      ```

3. Install necessary packages. We recommend using python version 3.7 or higher.
   ```
   pip install -r requirements.txt
   ```

## Reproducibility

1. Download benchmark tables from [this link](https://drive.google.com/drive/folders/18aYj1ZwXnp4OLIsmx9khqZD0oblMp8cs?usp=sharing) and upload them to their respective subfolders inside [benchmark](benchmark/) folder.

2. Download, unzip and upload [YAGO](https://yago-knowledge.org/downloads/yago-4) knowledge base to [yago/yago_original](yago/yago_original) folder.

3. Run [preprocess_yago.py](codes/preprocess_yago.py) to create entity dictionary, type dictionary, inheritance dictionary and relationship dictionary. Then run [Yago_type_counter.py](codes/Yago_type_counter.py), [Yago_subclass_extractor.py](codes/Yago_subclass_extractor.py) and [Yago_subclass_score.py](codes/Yago_subclass_score.py) one after another to generate the type penalization scores. The created dictionaries are stored in [yago/yago_pickle](yago/yago_pickle/).

4. Run [data_lake_processing_yago.py](codes/data_lake_processing_yago.py) to create yago inverted index.

5. Run [data_lake_processing_synthesized_kb.py](codes/data_lake_processing_synthesized_kb.py) to create synthesized type dictionary, relationship dictionary and synthesized inverted index.

6. Run [query_santos.py](codes/query_santos.py) to get top-k SANTOS unionable table search results.

## Citation

```


@inproceedings{2023khatiwadasantos,
title = {SANTOS: Relationship-based Semantic Table Union Search},
author={Khatiwada, Aamod and Fan, Grace and Shraga, Roee and Chen, Zixuan and Gatterbauer, Wolfgang and Miller, Ren{\'e}e J and Riedewald, Mirek},
year = {2023},
publisher = {ACM},
booktitle = {SIGMOD Conference 2023},
}
```