# Synthetic Data Generation with SDV

## Overview

This repository contains code for generating synthetic data using the Synthetic Data Vault (SDV) library. SDV is a Python library for synthesizing tabular data that preserves the statistical properties and dependencies observed in the original dataset.

## Requirements

- Python 3.x
- SDV library

## Installation

To install the SDV library, run the following command:

```bash
pip install sdv
```

## Usage

1. Import necessary modules:

```python
from sdv.metadata import SingleTableMetadata
from sdv.single_table import GaussianCopulaSynthesizer
```

2. Load your real dataset into a Pandas DataFrame (`real_data`).

3. Configure metadata and constraints for the synthesizer:

```python
# Create metadata
metadata = SingleTableMetadata()
metadata.detect_from_dataframe(real_data)

# Convert metadata to a dictionary
metadata_dict = metadata.to_dict()
# Access the 'columns' dictionary from the resulting dictionary
columns_dict = metadata_dict.get('columns', {})
# Extract column names from the 'columns' dictionary
found_column_names = columns_dict.keys()

# Customize metadata and constraints as needed
```

4. Train the synthesizer:

```python
# Initialize synthesizer
synthesizer = GaussianCopulaSynthesizer(metadata=metadata)

# Train the synthesizer
synthesizer.fit(real_data)
```

5. Generate synthetic data:

```python
# Generate synthetic data
synthetic_data = synthesizer.sample(num_rows=10)
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.