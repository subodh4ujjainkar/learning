# Step by step guide to install Elasticsearch-Logstash-Kibana Stack

### Add Elasticsearch public GPG Keys
> `curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic.gpg`

### Add Elastic package source list
> `echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list`

### Installing Elasticsearch
> `sudo apt update && sudo apt install elasticsearch`

#### Enable & Start Elasticsearch service
> `systemctl start elasticsearch.service`

> `systemctl enable elasticsearch.service`

#### Testing Elasticsearch
`curl -X GET 'http://localhost:9200/?pretty'`
