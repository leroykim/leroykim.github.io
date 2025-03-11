---
layout: post
title: Creating and Retrieving a FlyteDirectory URL in Flyte
categories: [Flyte, Workflow Orchestration]
tags: [Flyte, Python]
author: Dae-young Kim
comment: true
---
Flyte makes it easy to handle large datasets by treating directories as structured outputs using FlyteDirectory. This allows seamless management of files without manually handling storage paths.

In this post, we’ll demonstrate the simplest way to create a FlyteDirectory and retrieve its URL.

## 1. Process and Save Data in a FlyteDirectory
```python
import pandas as pd
from pathlib import Path
from flytekit import task, workflow, FlyteDirectory

@task
def generate_output_directory() -> FlyteDirectory:
    """Creates a directory, generates sample data, and returns a FlyteDirectory."""
    
    # Define local and remote directories
    local_dir = Path("output_data")
    local_dir.mkdir(parents=True, exist_ok=True)

    # Create a sample CSV file
    output_file = local_dir / "sample_data.csv"
    df = pd.DataFrame({"column_a": ["Value1", "Value2"], "column_b": [123, 456]})
    df.to_csv(output_file, index=False)

    # Return as FlyteDirectory with a remote storage location
    return FlyteDirectory(str(local_dir), remote_directory="s3://your-bucket/output_data")
```
This function:
- Creates an `output_data` folder.
- Saves a sample CSV file.
- Returns a `FlyteDirectory` that maps to a remote storage location.

## 2. Define and Run a Flyte Workflow
```python
@workflow
def data_pipeline() -> FlyteDirectory:
    """Flyte workflow to generate and return a FlyteDirectory."""
    return generate_output_directory()

# Run the workflow
result = data_pipeline()
print(f"Processed files saved at: {result.remote_source}")
```

This workflow:
- Calls the generate_output_directory task.
- Returns a FlyteDirectory containing the processed files.
- Prints the remote URL where files are stored.

## Conclusion
This is the simplest way to create a `FlyteDirectory` and get its URL. You can expand this to handle real-world data and integrate it with cloud storage solutions like AWS S3 or Google Cloud Storage.