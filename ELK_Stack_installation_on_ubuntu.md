# Step by step guide to install Elasticsearch-Logstash-Kibana Stack

### Add Elasticsearch public GPG Keys
> `curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elastic.gpg`

### Add Elastic package source list
> `echo "deb [signed-by=/usr/share/keyrings/elastic.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list`

### 1. Installing Elasticsearch
> `sudo apt update && sudo apt install elasticsearch`

#### Enable & Start Elasticsearch service
> `systemctl start elasticsearch.service`

> `systemctl enable elasticsearch.service`

#### Testing Elasticsearch
`curl -X GET 'http://localhost:9200/?pretty'`

### 2. Installing Kibana
> `sudo apt update && sudo apt install kibana`

#### Enable & Start Kibana service
> `sudo systemctl enable kibana.service`

> `sudo systemctl start kibana.service`

#### Allow access to Kibana from browser
> `sudo vim /etc/kibana/kibana.yml`

Change the line

`#server.host: "localhost"`

to

`server.host: "0"`

### 3. Installing Logstash
> `sudo apt update && sudo apt install logstash`

 #### Enable & Start Logstash service
> `sudo systemctl enable logstash.service`

> `sudo systemctl status logstash.service`

