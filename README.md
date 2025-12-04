# CDF Bootcamp - Ice Cream Factory Data Pipeline

A Cognite Data Fusion (CDF) bootcamp project demonstrating data ingestion, transformation, and analytics for an ice cream factory use case. This project extracts data from an external Ice Cream Factory API, processes it through CDF, and calculates Overall Equipment Effectiveness (OEE) metrics.

## Project Overview

This project implements a complete data operations solution for managing ice cream factory data across multiple global sites. It includes:

- **Data Extraction**: Automated extraction of time series data from the Ice Cream Factory API
- **Data Modeling**: Structured data models for assets, time series, and relationships
- **Data Transformations**: SQL-based transformations for asset hierarchy creation and time series contextualization
- **Analytics**: OEE (Overall Equipment Effectiveness) use case implementation
- **Workflows**: Automated data pipelines with scheduled execution

## Project Structure

```
├── ice-cream-dataops/          # Main CDF project directory
│   ├── modules/
│   │   └── bootcamp/
│   │       ├── data_foundation/        # Base data foundation setup
│   │       ├── ice_cream_api/          # Ice Cream Factory API integration
│   │       │   ├── data_models/        # Data model definitions
│   │       │   ├── data_sets/          # Data set configurations
│   │       │   ├── extraction_pipelines/  # Data extraction pipelines
│   │       │   ├── functions/          # Python functions for data extraction
│   │       │   ├── hosted_extractors/  # Hosted extractor configurations
│   │       │   ├── raw/                # Raw data table definitions
│   │       │   ├── transformations/    # SQL transformations
│   │       │   └── workflows/          # Workflow definitions
│   │       └── use_cases/
│   │           └── oee/                # OEE analytics use case
│   ├── config.prod.yaml        # Production environment configuration
│   ├── config.test.yaml        # Test environment configuration
│   ├── cdf.toml                # CDF toolkit configuration
│   └── pyproject.toml          # Python project dependencies
└── poetry.lock                  # Poetry lock file
```

## Features

### Data Extraction
- Automated extraction of time series datapoints from the Ice Cream Factory API
- Support for multiple factory sites (Houston, Oslo, Kuala Lumpur, Hannover, Nuremberg, Marseille, São Paulo, Chicago, Rotterdam, London)
- Incremental data loading with backfill capabilities
- Extraction pipeline monitoring and status reporting

### Data Modeling
- Custom data model space (`icapi_dm_space`) for ice cream factory data
- Asset hierarchy modeling with parent-child relationships
- Time series contextualization with asset associations
- OEE-specific data model space (`oee_ts_space`)

### Transformations
- **Create Asset Hierarchy**: Builds asset hierarchy from raw database tables
- **Contextualize Time Series and Assets**: Links time series to their associated assets

### Analytics
- **OEE (Overall Equipment Effectiveness)**: Calculates and tracks equipment efficiency metrics
- Time series analysis for production monitoring

### Workflows
- Automated data pipeline workflows
- Scheduled execution via cron expressions
- Trigger-based workflow execution

## Prerequisites

- Python 3.10 or higher (but less than 4.0)
- [Cognite Toolkit](https://github.com/cognitedata/cognite-toolkit) (>=0.6.97,<0.7.0)
- Cognite SDK (>=7.89.0,<8.0.0)
- Access to a Cognite Data Fusion project
- Poetry (for dependency management)

## Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   ```

2. **Install dependencies**
   ```bash
   cd ice-cream-dataops
   poetry install
   ```

3. **Configure CDF connection**
   - Update `cdf.toml` with your CDF project details
   - Configure environment-specific settings in `config.test.yaml` or `config.prod.yaml`
   - Set required environment variables:
     - `DATA_DEVELOPER_SOURCE_ID`
     - `ICAPI_EXTRACTORS_SOURCE_ID`
     - `IDP_TOKEN_URL`
     - `CDF_PROJECT`
     - `IDP_SCOPES`
     - `ICAPI_EXTRACTORS_CLIENT_ID`
     - `ICAPI_EXTRACTORS_CLIENT_SECRET`
     - `DATA_PIPELINE_OEE_SOURCE_ID`
     - `DATA_PIPELINE_OEE_CLIENT_ID`
     - `DATA_PIPELINE_OEE_CLIENT_SECRET`

4. **Deploy modules to CDF**
   ```bash
   cd ice-cream-dataops
   cdf build
   cdf deploy
   ```

## Configuration

### Environment Configuration

The project supports multiple environments configured via YAML files:

- **Test Environment**: `config.test.yaml`
- **Production Environment**: `config.prod.yaml`

Each configuration file includes:
- CDF project settings
- Module selection
- Environment-specific variables
- Authentication credentials

### Module Configuration

Key modules include:

- `bootcamp/ice_cream_api`: Main ice cream factory API integration module
- `bootcamp/oee`: OEE analytics use case module

## Usage

### Running Data Extraction

The data extraction function can be triggered manually or via scheduled workflows. It supports:

- **Sites**: Specify which factory sites to extract data from (defaults to all sites)
- **Backfill**: Enable/disable historical data backfill (default: enabled)
- **Hours**: Number of hours of data to extract (max: 336 hours, default: 336)

Example function invocation:
```python
{
  "sites": ["Houston", "Oslo"],
  "backfill": true,
  "hours": 168
}
```

### Running Transformations

Transformations can be executed via the CDF UI or using the CDF SDK:

1. **Create Asset Hierarchy**: Builds the asset hierarchy from raw data
2. **Contextualize Time Series**: Links time series to assets

### Monitoring

- Extraction pipeline runs are tracked via the `ep_icapi_datapoints` extraction pipeline
- Workflow execution status can be monitored in the CDF UI
- Function execution logs are available in CDF Functions

## Architecture

### Data Flow

1. **Raw Data Ingestion**: Data is extracted from the Ice Cream Factory API and stored in raw tables
2. **Data Modeling**: Raw data is transformed into structured data models (assets, time series)
3. **Contextualization**: Time series are linked to their associated assets
4. **Analytics**: OEE calculations and other analytics are performed on the contextualized data

### Key Components

- **Extraction Pipelines**: Monitor and track data extraction runs
- **Functions**: Python-based data extraction and processing functions
- **Transformations**: SQL-based data transformations
- **Workflows**: Orchestrate the data pipeline execution
- **Data Models**: Define the structure and relationships of industrial data

## Contributing

This is a bootcamp project for learning CDF data operations. For questions or issues, please refer to the [Cognite Documentation](https://docs.cognite.com/) or contact the project maintainers.

## License

This project is part of the Cognite Data Fusion bootcamp program.

## Resources

- [Cognite Data Fusion Documentation](https://docs.cognite.com/)
- [Cognite Toolkit Documentation](https://github.com/cognitedata/cognite-toolkit)
- [Cognite SDK Documentation](https://cognite-sdk-python.readthedocs.io/)

