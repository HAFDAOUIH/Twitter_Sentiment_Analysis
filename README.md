# Twitter Sentiment Analysis

This project analyzes real-time Twitter data to determine sentiment (positive, negative, neutral) using Apache Kafka, Spark, and a pre-trained logistic regression model. The results are stored in a MongoDB database and visualized using a Streamlit web application.

## Project Structure

```markdown
├── Consumer
│ └── Consumer.py
├── Producer
│ └── Dockerfile
├── Webapp
│ ├── MongoDB.py
│ ├── main.py
│ ├── Visualisation.py
│ └── VisualisationTest.py
├── .gitignore
└── requirements.txt
'''


**Important Note:** The `Producer.py` script and the `twitter_validation.csv` file are located within the `kafka1` Docker container and are accessed using Docker volumes. 

## Getting Started

### Prerequisites

* **Docker:** [https://www.docker.com/](https://www.docker.com/)
* **Python 3.9:** [https://www.python.org/](https://www.python.org/)
* **Git:** [https://git-scm.com/](https://git-scm.com/)

### Installation

1. **Clone the Repository:**
  ```bash
  git clone https://github.com/YOUR_GITHUB_USERNAME/Twitter_Sentiment_Analysis.git
  cd Twitter_Sentiment_Analysis
  
  # Install Python Dependencies:
  pip install -r requirements.txt
  
  # Set Up Kafka and Zookeeper:
  
  # Start Zookeeper:
  docker run -d --name zookeeper -p 2181:2181 zookeeper:3.4.14
  
  # Start Kafka:
  docker run -d --name kafka -p 9092:9092 --link zookeeper:zookeeper wurstmeister/kafka:2.12-2.2.1
  
  # Prepare the Kafka Container with Producer.py and Data:
  # You'll need to copy Producer.py and twitter_validation.csv into your kafka1 Docker container.
  # The exact method for doing this might vary depending on your setup, but here are two common approaches:
  #   - Using docker cp: Copy the files from your host machine to the container.
  #   - Mounting Volumes: Mount a volume from your host machine that contains the files into the kafka1 container.
  
  # Build the Producer Docker Image:
  docker build -t twitter-producer ./Producer
  
  # Run the Producer Container:
  # Make sure the kafka1 container is running.
  # Run the producer container, mounting kafka1's volumes to access the files:
  docker run -it --rm --name twitter-producer-container --volumes-from kafka1 twitter-producer
  
  # Start the Spark Consumer:
  # Open a new terminal and navigate to the Consumer directory.
  # Execute Consumer.py using Spark:
  spark-submit --packages org.apache.spark:spark-streaming-kafka-0-10_2.12:3.0.0 ./Consumer.py

 # Run the Streamlit Web App:
 # Open another terminal and navigate to the WebApp directory.
 # Run the Streamlit app:
 streamlit run main.py
  ### Usage

The producer (running inside the kafka1 container) continuously streams Twitter data from the `twitter_validation.csv` file into a Kafka topic. The Spark consumer subscribes to the Kafka topic, analyzes tweet sentiment using a pre-trained Logistic Regression model, and stores the results in MongoDB. The Streamlit web app visualizes the sentiment analysis data retrieved from MongoDB.

### Configuration

Modify the Kafka topic name and other settings in the `Producer.py` script (inside the kafka1 container). Configure your MongoDB connection details in the `WebApp/MongoDB.py` file.

### Contributing

Feel free to contribute to the project by submitting issues or pull requests.
