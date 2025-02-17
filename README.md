# Simple Elastic SIEM Lab

Hey there! I'm going to walk you through setting up your own **Elastic SIEM Lab** from scratch. This guide is perfect for anyone who wants to learn about Elasticsearch, Kibana, and Logstash in a hands-on way. I'll break it down step by step so you can follow along easily.

## Table of Contents
- [Introduction](#introduction)
- [What You Need](#what-you-need)
- [Step-by-Step Setup](#step-by-step-setup)
  - [1. Installing Elasticsearch](#1-installing-elasticsearch)
  - [2. Setting Up Kibana](#2-setting-up-kibana)
  - [3. Installing Logstash](#3-installing-logstash)
  - [4. Adding Beats for Log Collection](#4-adding-beats-for-log-collection)
  - [5. Creating Dashboards in Kibana](#5-creating-dashboards-in-kibana)
- [Wrapping Up](#wrapping-up)

## Introduction
Elastic SIEM is a powerful tool for detecting and responding to security threats using Elastic Stack. In this guide, I’ll show you how to set up a simple lab so you can experiment with it yourself.

## What You Need
Before we get started, make sure you have:
- A computer running **Windows or Linux**
- **Docker and Docker Compose** (optional, but makes life easier)
- **Internet access**
- A basic understanding of how logs work

## Step-by-Step Setup

### 1. Installing Elasticsearch
First, we need to install **Elasticsearch**, the backbone of Elastic Stack. Run the following command to download and extract it:

```bash
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.x.x-linux-x86_64.tar.gz
tar -xzf elasticsearch-8.x.x-linux-x86_64.tar.gz
cd elasticsearch-8.x.x
./bin/elasticsearch
```

#### Configuring Elasticsearch
Now, open `elasticsearch.yml` and tweak these settings:

```yaml
network.host: 0.0.0.0
xpack.security.enabled: false
```

_(Add an image here if you want to show the setup process)_

### 2. Setting Up Kibana
Kibana is the UI for Elastic Stack. Here's how you get it running:

```bash
wget https://artifacts.elastic.co/downloads/kibana/kibana-8.x.x-linux-x86_64.tar.gz
tar -xzf kibana-8.x.x-linux-x86_64.tar.gz
cd kibana-8.x.x
./bin/kibana
```

#### Configuring Kibana
Edit `kibana.yml` and set:

```yaml
server.host: "0.0.0.0"
elasticsearch.hosts: ["http://localhost:9200"]
```

_(Insert an image here to show the Kibana UI)_

### 3. Installing Logstash
Logstash processes logs and sends them to Elasticsearch. Download and set it up like this:

```bash
wget https://artifacts.elastic.co/downloads/logstash/logstash-8.x.x-linux-x86_64.tar.gz
tar -xzf logstash-8.x.x-linux-x86_64.tar.gz
cd logstash-8.x.x
./bin/logstash -f logstash.conf
```

#### Logstash Configuration
Create a `logstash.conf` file:

```plaintext
input {
  beats {
    port => 5044
  }
}
output {
  elasticsearch {
    hosts => ["localhost:9200"]
  }
}
```

_(Insert an image of the Logstash config here)_

### 4. Adding Beats for Log Collection
Now we need to install **Filebeat** to collect logs.

```bash
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-8.x.x-linux-x86_64.tar.gz
tar -xzf filebeat-8.x.x-linux-x86_64.tar.gz
cd filebeat-8.x.x
./filebeat -e -c filebeat.yml
```

#### Configuring Filebeat
Modify `filebeat.yml`:
```yaml
filebeat.inputs:
  - type: log
    paths:
      - /var/log/*.log
output.logstash:
  hosts: ["localhost:5044"]
```

_(Insert an image here to show logs being collected)_

### 5. Creating Dashboards in Kibana
Now that everything is running, open Kibana at `http://localhost:5601` and:

- Go to **Management > Index Patterns** and create a pattern.
- Open **Discover** to explore your logs.
- Use **Visualizations** to create awesome charts.

_(Insert an image here of a sample dashboard)_

## Wrapping Up
Congrats! 🎉 You just built a fully functional **Elastic SIEM Lab**! From here, you can:
- Add more Beats for different log sources.
- Experiment with **ElastAlert** for alerts.
- Try **Machine Learning** features in Kibana.


