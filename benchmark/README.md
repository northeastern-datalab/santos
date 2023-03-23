## Folder Description

This folder stores data lake tables for preprocessing (offline) phase and query tables for Query phase. Reorganize this folder as per your use. Currently, it contains three subfolders for SANTOS Small (santos_benchmark), SANTOS Large (real_tables_benchmark) and TUS Benchmark. All folders contain their respective query and dataLake subfolders with some sample tables. Please visit [this link](https://gitlab.com/dvolgyes/zenodo_get) to download full SANTOS Large Benchmark and SANTOS small Benchmark. The original TUS benchmark is available at [https://github.com/RJMillerLab/table-union-search-benchmark](https://github.com/RJMillerLab/table-union-search-benchmark). You can also run the following commands on your terminal. The commands automatically download SANTOS Large and SANTOS Small benchmarks, uncompress them and replace placeholder folders with the folders having tables. As the first command takes you to benchmark folder before downloading the benchmarks, make sure that you are in home of the repo. 
    
    ```
    cd benchmark && zenodo_get 7758091 && rm -r santos_benchmark && unzip santos_benchmark && cd santos_benchmark && rm *.csv && cd .. && rm -r real_tables_benchmark && unzip real_data_lake_benchmark && cd real_data_lake_benchmark && rm *.csv && cd .. && mv real_data_lake_benchmark real_tables_benchmark && rm *.zip && cd ..
    ```
