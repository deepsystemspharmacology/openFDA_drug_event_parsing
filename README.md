# openFDA drug event parsing

https://open.fda.gov/

This repository contains the code used to download/extract/process the human drug event data found [here](https://open.fda.gov/downloads/).

The notebooks were created for prototyping, then converted to scripts for running the methodology in parallel on a multicore machine. 

The processed data was then converted into a set of tables with entity relationships.

The order of code execution goes:

20191230_rxnorm_hierarchy_tables.ipynb #requires vocabulary permissions to use the concepts from OHDSI's Athena

Parsing.ipynb||Parsing.py

-->

openFDA_Entity_Relationship_Tables.ipynb||openFDA_Entity_Relationship_Tables.py

-->

tableize_openFDA_files.sh # assumes you have cloned the tableize repository from tatonetti-lab, at the same level as this repository

(optional)

-->

Pediatrics_data_parsing.ipynb||Pediatrics_data_parsing.py

-->

Exploring.ipynb

```
python3 Parsing.py
python3 openFDA_Entity_Relationship_Tables.py
./tableize_openFDA_files.sh
python3 Pediatrics_data_parsing.py #optional
```

## Notes:

- To be able to make all these requests to the FDA's servers, one has to get an API key to have access. I stored my key information in .openFDA.params. The file is hidden (via .gitignore) in this repo to not show my credentials, but you can request your own [here](https://open.fda.gov/apis/authentication/).
- I leveraged the OMOP common data format to map the drug and reaction names and IDs to standard vocabularies as found [here](http://athena.ohdsi.org/search-terms/terms). Due to possible license restrictions of these vocabularies and me wanting to be extra careful in case there is, I also hid those directories of tables. (Two directories contain tables directly from the source, and the other contains tables that were processed further by me for use in my methodology). If you create/have an account on the linked website (which I think is easy to do for researchers), then you would be able to download and use this data. 
