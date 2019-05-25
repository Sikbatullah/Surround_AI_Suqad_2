# Feeding the Data: Fetch ()
```
def fetch_data(surround_config):
    dir_path = surround_config.get_path("surround.path_to_epl_data")
    all_files = glob.glob(dir_path + "/*.csv")

    df_from_each_file = (pd.read_csv(f) for f in all_files)
    input_data = pd.concat(df_from_each_file, ignore_index=True, sort=False)
    return input_data
 ```
 In EPL match prediction `fetch_data` starts by directing the path of `surround_config` to epl data. 
 ```
 path_to_epl_data: ../data/epl_csv
 ```
 Then it grabs all the data from that set path in this case the csv files. Afterwards the csv files are converted into dataframes. In the process of converting these files to dataframes, the index of each file is ignored which in terms gives us the `epl_data` which is our `input_data`.