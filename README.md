<div align="center">
<a href="https://inquery.io"><img src="https://svgshare.com/i/qHg.svg" alt="Inquery"></a>

<em>Real-time events platform for Postgres</em>

[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/inqueryio.svg?style=social&label=Follow%20%40inqueryio)](https://twitter.com/inqueryio) 
[![GitHub Repo stars](https://img.shields.io/github/stars/inqueryio/inquery?style=social)](https://github.com/inqueryio/inquery)

</div>


Inquery is a utility for Postgres that triggers webhooks when rows are inserted, updated, or deleted. It uses
database triggers that send low-latency websocket messages to a Go application. This application then calls
the configured webhook(s) with a JSON payload that includes specified values from the database row.

![DB Webhooks Flow](https://i.imgur.com/BgR5lbo.png)

## Use Cases

* **Send notifications:** Slack, Email, Text Message, Push Notification
* **Call serverless functions:** AWS Lambda, Google Cloud Functions, Azure Functions
* **Trigger analytics events:** Segment, Mixpanel, Amplitude
* **Stream data real-time:** Snowflake, BigQuery, Clickhouse, Redshift

![Inquery Create Slack Notification](https://i.imgur.com/Nv7MfQV.gif)

## Steps

1. Data modified in Postgres table (INSERT, UPDATE, DELETE)
2. Postgres trigger notifies DB Webhooks web server via websocket message
3. DB Webhooks formats data and sends webhook(s)

## Get Started

### Run Inquery locally

You can run Inquery locally with Docker.

```bash
git clone --depth 1 https://github.com/inqueryio/inquery.git
cd inquery
docker-compose up -d
```

Then open [http://localhost:3000](http://localhost:3000) to access Inquery.\
NOTE: When connecting your database, if your Postgres host is `localhost`, you must use `host.docker.internal` instead to access it when running with Docker.

### Run Inquery on AWS (EC2)

NOTE: Make sure this instance is only accessible within your VPC.\
NOTE: These instructions are for Amazon Linux 2 AMI (HVM).

1. To install Docker, run the following command in your SSH session on the instance terminal:
```bash
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker $USER
```
2. To install `docker-compose`, run the following command in your ssh session on the instance terminal:
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-$(uname -s)-$(uname -m)"  -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
docker-compose version
```
3. Install and run Inquery
```bash
mkdir inquery && cd inquery
wget https://raw.githubusercontent.com/inqueryio/inquery/main/{.env,docker-compose.yml,.dockerignore}
sudo docker-compose up -d
```

## Roadmap

- Filters and mapping options the row data to the POST request

Let us know your feedback or feature requests! You can submit a GitHub issue or contact us at hello@inquery.io
