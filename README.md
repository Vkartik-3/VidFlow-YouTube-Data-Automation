## ⚠️ IMPORTANT NOTICE ⚠️

<h2 style="color: red;">
PROJECT FILES ARE TEMPORARILY UNAVAILABLE AS I'M CURRENTLY WORKING ON RESOLVING SOME IMPLEMENTATION ISSUES. THE COMPLETE CODEBASE WILL BE UPLOADED SOON. PLEASE REFER TO THE README FOR THE PROJECT ARCHITECTURE AND TECHNICAL DETAILS.
</h2>


# VidFlow: YouTube Data Automation

## Project Overview

VidFlow is a comprehensive data engineering project that builds an ETL (Extract, Transform, Load) pipeline for YouTube trending videos data. The pipeline extracts data using the YouTube API, processes it with Apache Spark, stores it in AWS S3, and makes it available for analysis through AWS Athena and visualization in Tableau.



## Table of Contents

- [Architecture](#architecture)
- [Technologies Used](#technologies-used)
- [Data Source](#data-source)
- [Project Structure](#project-structure)
- [Setup and Installation](#setup-and-installation)
  - [Prerequisites](#prerequisites)
  - [Environment Setup](#environment-setup)
  - [Configuration](#configuration)
- [Running the Pipeline](#running-the-pipeline)
- [Data Schema](#data-schema)
- [Analytics Capabilities](#analytics-capabilities)
- [Visualizations](#visualizations)
- [Future Enhancements](#future-enhancements)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Architecture

This project follows a modern data engineering architecture:

1. **Data Extraction**: YouTube API is used to fetch trending videos data
2. **Data Processing**: Apache Spark processes and transforms the raw data
3. **Data Storage**: Processed data is stored in AWS S3 in Parquet format
4. **Data Cataloging**: AWS Glue Crawler catalogs the data for querying
5. **Data Querying**: AWS Athena provides SQL querying capabilities
6. **Data Visualization**: Tableau connects to Athena for creating dashboards

## Technologies Used

- **Apache Spark**: For distributed data processing
- **Python**: Core programming language
- **AWS Services**:
  - S3: Object storage for data lake
  - EC2: Compute for data processing
  - Glue: Data catalog service
  - Athena: Serverless query service
  - IAM: Identity and access management
- **Tableau**: Data visualization and dashboards
- **Git**: Version control
- **Docker**: Containerization (optional)

## Data Source

The project uses the YouTube Data API v3 to collect trending videos data. The API provides access to various YouTube resources including:

- Video metadata (title, description, publish date, etc.)
- Channel information
- Video statistics (views, likes, comments, etc.)
- Video categories
- Geographic trending data

## Project Structure

```
youtube-data-analysis/
│
├── config/
│   ├── config.ini              # Configuration file for API keys and AWS settings
│
├── src/
│   ├── extraction/             # Data extraction scripts
│   │   ├── youtube_api.py      # YouTube API connector
│   │   └── extract_data.py     # Main extraction script
│   │
│   ├── transformation/         # Data transformation scripts
│   │   ├── spark_jobs/         # Spark transformation jobs
│   │   └── transform_data.py   # Main transformation script
│   │
│   ├── loading/                # Data loading scripts
│   │   └── load_to_s3.py       # Script to load data to S3
│   │
│   └── utils/                  # Utility functions
│       ├── s3_utils.py         # S3 utility functions
│       └── logging_utils.py    # Logging utility functions
│
├── notebooks/                  # Jupyter notebooks for exploration and testing
│   ├── data_exploration.ipynb  # Data exploration notebook
│   └── spark_testing.ipynb     # Spark testing notebook
│
├── scripts/                    # Shell scripts for automation
│   ├── setup.sh                # Setup script
│   └── run_pipeline.sh         # Script to run the full pipeline
│
├── sql/                        # SQL queries for Athena
│   ├── create_tables.sql       # Table creation queries
│   └── analysis_queries.sql    # Analysis queries
│
├── terraform/                  # Infrastructure as Code (Optional)
│   └── main.tf                 # Terraform configuration
│
├── docs/                       # Documentation
│   └── images/                 # Images for documentation
│
├── .gitignore                  # Git ignore file
├── requirements.txt            # Python dependencies
├── Dockerfile                  # Docker configuration (Optional)
├── LICENSE                     # License file
└── README.md                   # Project README
```

## Setup and Installation

### Prerequisites

- AWS Account with appropriate permissions
- Python 3.8+
- Apache Spark 3.1+
- YouTube Data API key
- Tableau Desktop (for visualization)

### Environment Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/Youtube-Data-Analysis---Data-Engineering-Project.git
   cd Youtube-Data-Analysis---Data-Engineering-Project
   ```

2. Install the required Python packages:
   ```bash
   pip install -r requirements.txt
   ```

3. Set up AWS CLI and configure credentials:
   ```bash
   pip install awscli
   aws configure
   ```

### Configuration

1. Create a `config.ini` file in the `config` directory with the following structure:
   ```ini
   [youtube_api]
   api_key = YOUR_YOUTUBE_API_KEY

   [aws]
   region = YOUR_AWS_REGION
   s3_bucket = YOUR_S3_BUCKET_NAME
   ```

2. Create the S3 bucket if it doesn't exist:
   ```bash
   aws s3 mb s3://YOUR_S3_BUCKET_NAME
   ```

## Running the Pipeline

### Manual Execution

1. Run the extraction script:
   ```bash
   python src/extraction/extract_data.py
   ```

2. Run the transformation script:
   ```bash
   python src/transformation/transform_data.py
   ```

3. Run the loading script:
   ```bash
   python src/loading/load_to_s3.py
   ```

### Using the Pipeline Script

Run the entire pipeline with a single command:
```bash
./scripts/run_pipeline.sh
```

## Data Schema

After processing, the data follows this schema in the data lake:

**Videos Table**:
- video_id (string): Unique identifier for the video
- title (string): Video title
- channel_id (string): Channel identifier
- channel_title (string): Channel name
- publish_time (timestamp): When the video was published
- tags (array<string>): Video tags
- category_id (string): Category identifier
- trending_date (date): Date when the video was trending
- view_count (long): Number of views
- likes (long): Number of likes
- dislikes (long): Number of dislikes
- comment_count (long): Number of comments
- thumbnail_link (string): Link to the thumbnail
- comments_disabled (boolean): Whether comments are disabled
- ratings_disabled (boolean): Whether ratings are disabled
- description (string): Video description
- region (string): Region where the video is trending

## Analytics Capabilities

With this pipeline, you can perform various analyses:

1. **Trending Videos Analysis**:
   - Most viewed videos by category
   - Videos with highest engagement (likes/views ratio)
   - Trending patterns over time

2. **Content Creator Analysis**:
   - Top channels by trending videos
   - Channel performance metrics

3. **Regional Analysis**:
   - Region-specific trending patterns
   - Content preferences by region

4. **Temporal Analysis**:
   - Day of week/time of day trends
   - Seasonal trending patterns

## Visualizations

Example visualizations you can create with Tableau:

1. **Trending Dashboard**:
   - Heatmap of trending videos by category and region
   - Time series of trending video metrics

2. **Engagement Analysis**:
   - Comparison of engagement metrics across categories
   - Correlation between video attributes and performance

3. **Content Creator Insights**:
   - Top channels by region and category
   - Channel growth and performance metrics

## Future Enhancements

- Implement real-time data processing with Kafka and Spark Streaming
- Add sentiment analysis on video comments
- Develop ML models to predict video performance
- Create an automated recommendation system
- Implement API for accessing processed data

## Troubleshooting

**Common Issues:**

1. **YouTube API Quota Exceeded**:
   - Solution: Implement rate limiting or use multiple API keys

2. **Spark Job Failures**:
   - Solution: Check logs in the Spark UI and ensure sufficient resources

3. **AWS Athena Query Issues**:
   - Solution: Verify that the AWS Glue Crawler has correctly cataloged the data

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

*VidFlow: YouTube Data Automation*
