# 🌟 **Welcome to TweetStream Analytics Hub** 🌟  
Where tweets meet technology! 🚀  

---

## 🌍 **Our Mission**  
We’re here to decode the world of Twitter, one tweet at a time! By harnessing real-time streaming, big data processing, and intuitive visualization, we bring Twitter analytics to life. Whether it’s hashtags, sentiment, or trends, we’ve got it all mapped—literally. 🗺️✨  

---

## 🛠️ **What We’re Building**  
Our TweetStream Analytics Pipeline has a touch of magic and a dash of science:  
- **💬 Real-time Tweet Ingestion**: Capturing the pulse of the world as it happens.  
- **🔍 Intelligent Processing**: Extracting meaning, hashtags, and sentiment.  
- **🗂️ Smart Storage**: Keeping data searchable and ready for exploration.  
- **🌟 Stunning Visualizations**: Beautiful maps, trends, and sentiment scores at your fingertips.  

---

## 🗃️ **Our Projects**

| 📂 Repository            | 📝 Description                                                                                     |  
|--------------------------|-------------------------------------------------------------------------------------------------|  
| **ElasticSearchManager** | Indexes tweets for lightning-fast queries and scalable storage.                                  |  
| **StreamProducer**        | Streams tweets live from Twitter or simulates them for testing.                                   |  
| **StreamConsumer**        | Transforms tweets with hashtags and sentiment analysis for actionable insights.                   |  
| **Website**               | A stunning web app for interactive maps, trends, and sentiment gauges.                            |  
| **APIServices**           | RESTful APIs powering the frontend with meaningful data.                                          |  
| **DocsAndReadme**         | Your one-stop shop for documentation, diagrams, and task tracking.                                |  

---

## Project Overview
The Twitter Stream Processing Pipeline is designed to handle real-time streaming tweets, process and transform the data for efficient querying, and visualize results in an interactive web application. This pipeline integrates multiple components, leveraging scalable tools and technologies like Apache Kafka, Elasticsearch, Apache Spark, and React to ensure seamless ingestion, processing, storage, and visualization of Twitter data.

## Main Components

### 1. Stream Ingestion
- Collects a continuous stream of tweets using the Twitter API or a simulated tweet generator.
- Maintains the incoming tweet stream in an Apache Kafka topic for intermediate storage and scalability.

### 2. Processing Components
#### Data Transformation
- Prepares tweet data for efficient searching over text, time, and space.

#### Hashtag Extraction
- Extracts hashtags from tweet text and stores them as a nested array.

#### Sentiment Analysis
- Uses Spark NLP or TextBlob to classify tweet sentiments as "Positive," "Negative," or "Neutral."

### 3. Storage
- Stores processed tweets and their metadata in an Elasticsearch database.
- Designed with a schema to support querying by text, time, hashtags, and geo-coordinates.

### 4. Web Application
- Provides an input field where users can search for tweets by keyword.
- Visualizes results with:
  - **Map View**: Displays tweets containing the keyword on an interactive map using Leaflet, based on geo-coordinates (longitude/latitude).
  - **Trend Diagram**: Shows the temporal distribution of tweets (hourly and daily aggregation).
  - **Sentiment Gauge**: Reflects the average sentiment score for tweets over a specified period of time.
 ### lets preview in Action :
 
#### home page :
<div style="text-align: center; width: 100%;">
  <img src="https://github.com/user-attachments/assets/16f14018-2bb2-494f-bce9-beb140af62ec" width="300" style="display: block; margin: 0 auto;" />
</div>
<br>


![Home-Page-Mac](https://github.com/user-attachments/assets/b7513261-2797-437d-b03e-0d22d8abd52c)

#### Map page :

![Map](https://github.com/user-attachments/assets/4ac9079c-3c39-437f-b655-49d5a3fcadde)


## System Components

### 1. Kafka Producer for Batched Tweet Data Streaming
- Reads geolocated tweet data from JSON files using Apache Spark.
- Sends data to a Kafka topic (`tweets`) in batches (default size: 1000 records).
- Simulates real-time streaming with a configurable delay (default: 30 seconds).

### 2. Kafka Consumers for Processing and Sentiment Analysis
#### a. Filter Consumer
- Consumes tweet data from the Kafka `tweets` topic.
- Filters geolocated tweets and extracts relevant fields (text, hashtags, time, coordinates).
- Sends filtered data to the Kafka topic `processedTweets`.

#### b. Sentiment Analysis Consumer
- Consumes data from the Kafka `processedTweets` topic.
- Performs sentiment analysis using Spark NLP.
- Classifies tweets as "Positive," "Negative," or "Neutral."
- Sends enriched data to Elasticsearch for visualization.

### 3. Elasticsearch Manager
- Stores and indexes processed tweet data for querying and analytics.
- Configures Elasticsearch index with fields like text, hashtags, sentiment, coordinates, and timestamp.

### 4. Sentiment Analysis API
- Built with FastAPI to query Elasticsearch for tweet data and sentiment insights.
- Features include:
  - Sentiment scores and geo-based trends.
  - Hashtag ranking and temporal analysis.
  - Custom date range filtering.

### 5. Web Application
- React.js-based frontend for visualizing tweet data.
- Features include:
  - Latest tweets and sentiment distribution.
  - Trending hashtags and topics.
  - Sentiment by location (interactive maps).
  - Daily/hourly sentiment trends.

## 🛠️ Prerequisites
To run the system, ensure the following tools are installed:

- Apache Kafka
- Apache Spark
- Elasticsearch (v7.x or higher)
- Python 3.8+
- React.js
- Docker (optional, for Elasticsearch setup)

## ⚡ Quick Start Guide

### 1. Set Up Kafka
Start a Kafka server and create required topics: `tweets` and `processedTweets`.

### 2. Run the Kafka Producer
Use Apache Spark to read tweet data and send it to the Kafka `tweets` topic.

### 3. Start Kafka Consumers
- Deploy the Filter Consumer to process tweets and forward to `processedTweets`.
- Deploy the Sentiment Analysis Consumer to classify sentiments and store them in Elasticsearch.

### 4. Set Up Elasticsearch
Use Docker for a quick setup:
```bash
docker run -p 9200:9200 -d docker.elastic.co/elasticsearch/elasticsearch:7.9.3
```

Create an Elasticsearch index for storing tweet data:
```bash
curl -X PUT "localhost:9200/tweet" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 1
  },
  "mappings": {
    "properties": {
      "created_at": {"type": "date", "format": "EEE MMM dd HH:mm:ss Z yyyy"},
      "text": {"type": "text", "analyzer": "standard"},
      "hashtags": {"type": "nested", "properties": {"text": {"type": "keyword"}}},
      "coordinates": {"type": "geo_point"},
      "sentiment": {"type": "float"}
    }
  }
}
'
```

### 5. Run the Sentiment Analysis API
Start the FastAPI application to query tweet data from Elasticsearch.

### 6. Launch the Web Application
Deploy the React.js frontend to visualize tweets, sentiments, and trends.
