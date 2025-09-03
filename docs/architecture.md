
## Overview

The Data Dashboard is a lightweight analytics platform designed to:
  - Load data from **CSV files** or **SQL databases**
  - Clean, filter, and aggregate the data
  - Display interactive visualizations via **Streamlit** (primary) or **Dash** (alternative)
  - Export processed results to **CSV, Excel, or HTML reports**


## Architecture Diagram
```mermaid
   flowchart TD
      A[CSV/SQL Data Source] --> B[Data Loader (pandas/SQLAlchemy)]
      B --> C[Data Processing Layer (filters, aggregations)]
      C --> D[Visualization Layer (Plotly/Matplotlib)]
      D --> E[Web App Layer (Dash/Streamlit)]
      E --> F[User Browser]
      C --> G[Exporters (CSV/Excel/HTML)]
```

## Key Components
  - **Data Loader (core/data_loader.py**:
    - Reads data from CSV (via pandas.read_csv) or SQL (via SQLAlchemy)
    - Normalizes column names, infers datetime types
    - Provides a cached `load_dataframe` function for performance
  - **Processing Layer (core/processing.py)**: 
    - **Filtering**: Date-based filters using a given column
    - **Aggregation**: Group by categorical columns, compute sum/mean/count/etc.
    - **Top N selection**: Limit results by sorting and slicing
  - **Visualization Layer (core/visuals.py**: 
    - **Bar, Line, Pie** charts (Plotly Express)
    - **Table** view (Plotly Graph Objects)
    - Designed for **interactive exploration** in Streamlit or Dash
  - **Web App Layer**:
    - **Steamlit App (app_streamlit.py)**: Primary user interface, with sidebar filters, chart display, and export buttons
    - **Dash App (app_dash.py)**: Minimal alternative for environments preferring Dash
  - **Exporters (core/exporters.py)**: 
    - Export current dataset or aggregated view to:
      - CSV (UTF-8 text)
      - Excel (multi-sheet, via XlsxWriter)
      - HTML (basic report templates)
  - **Utilities (core/utils.py)**:
    - Auto-detect **numeric, categorical, and date columns**
    - Assist UI elements in pre-populating filter options

## Tech Stack
  - **Language**: Python 3.10+
  - **Libraries**:
    - Data: `pandas`, `SQLAlchemy`
    - Visualization: `plotly`, `dash`, `streamlit`
    - Export: `xlsxwriter`
  - **Environment**: `.env` support for config (datasource kind, paths, DB connection)
  - **Tests**: `pytest` unit tests for processing layer


## Design Principles


## Data Flow


## Security

## Testing & Quality Assurance
  - **Unit Tests**: Cover `processing.py` functions
  - **Integration Tests**: Validate CSV/SQL ingestion
  - **Manual Tests**: Verify UI, uploads, chart interactions, and exports

## Future Improvements
  - Authentication for private dashboards (OAuth, SSO).
  - PDF export
  - Deploy on Heroku/Render for client access.
