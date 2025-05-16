# fg
Elastic Search access

To install:	```pip install fg```

## Overview

The `fg` package provides a comprehensive interface for interacting with Elasticsearch, allowing for operations such as searching, counting, and sampling documents, as well as importing data from MongoDB into Elasticsearch. It includes functionality to handle complex queries, manage document mappings, and perform data extraction and transformation efficiently.

## Features

- **ElasticCom Class**: Central to the package, this class facilitates connections to Elasticsearch and provides methods to perform various operations like search, count, and data extraction.
- **Data Sampling**: Supports sampling strategies based on arithmetic sequences or random field values, useful for handling large datasets.
- **Integration with MongoDB**: Offers methods to import data directly from MongoDB collections into Elasticsearch, which is handy for data migration or synchronization tasks.
- **Data Export**: Includes utilities to export data from Elasticsearch into Python dictionaries or pandas DataFrames, supporting data analysis and manipulation.
- **Utility Functions**: Additional helper functions to manage and convert data types, handle UTF-8 encoding issues, and more.

## Usage Examples

### Connecting to Elasticsearch

```python
from fg import ElasticCom

# Initialize ElasticCom with the index name
elastic_instance = ElasticCom(index="your_index_name")
```

### Searching Documents

```python
# Perform a search operation
search_results = elastic_instance.search(query={"match_all": {}})
```

### Sampling Documents Based on Arithmetic Sequence

```python
# Sample documents using an arithmetic sequence
sampled_docs = elastic_instance.sample_with_arithmetic_seq(sample_size=10)
```

### Importing Data from MongoDB

```python
from pymongo import MongoClient

# Connect to MongoDB
mongo_client = MongoClient()
mongo_db = mongo_client["your_mongo_db"]
mongo_collection = mongo_db["your_collection"]

# Import data from MongoDB to Elasticsearch
import_result = elastic_instance.import_mongo_collection(mongo_db=mongo_db, mongo_collection=mongo_collection)
```

### Exporting Search Results to DataFrame

```python
# Export search results to a pandas DataFrame
df = elastic_instance.search_and_export_to_df(query={"match_all": {}})
```

## Class and Method Documentation

### Class: ElasticCom

- **`__init__(self, index, doc_type=None, hosts='localhost:9200', **kwargs)`**: Initializes a connection to an Elasticsearch cluster.
- **`search(self, *args, **kwargs)`**: Executes a search query.
- **`count(self, *args, **kwargs)`**: Counts the documents matching a query.
- **`sample_with_arithmetic_seq(self, sample_size, initial_idx=None, **kwargs)`**: Samples documents based on an arithmetic sequence.
- **`sample_based_on_random_field_val(self, n_rand_picks=10, rand_field='timestamp', rand_batch_size=1, *args, **kwargs)`**: Samples documents based on random values of a specified field.

### Utility Functions

- **`get_search_hits(es_response, _id=True, data_key=None)`**: Extracts hits from an Elasticsearch response.
- **`es_types_to_main_types(mapping)`**: Converts Elasticsearch field types to more general types.
- **`to_utf8_or_bust(obj)`**: Ensures strings are in UTF-8 format, attempting conversion if necessary.

## Notes

- Ensure Elasticsearch and MongoDB instances are accessible from the environment where `fg` is used.
- Handle exceptions and errors, especially when dealing with network operations and data conversions.

This package is designed to simplify and streamline the process of working with Elasticsearch, providing high-level abstractions for common tasks while still allowing detailed control when needed.