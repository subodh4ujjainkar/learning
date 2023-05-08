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

#### Testing Kibana
> `http://localhost:5601/status`

Change the line

`#server.host: "localhost"`

to

`server.host: "0"`

### 3. Installing Logstash
> `sudo apt update && sudo apt install logstash`

#### Enable & Start Logstash service
> `sudo systemctl enable logstash.service`

> `sudo systemctl status logstash.service`

### 4. Installing FileBeat
> `sudo apt update && sudo apt install filebeat`

#### Enable & Start Filebeat service
> `sudo systemctl enable filebeat`

> `sudo systemctl status filebeat`

#### Configure Filebeat to push data to logstash instead of elasticsearch
> Open config file `/etc/filebeat/filebeat.yml` and Comment the below lines

>  `output.elasticsearch:`

>  `hosts: ["localhost:9200"]`

> Now uncomment the below lines

> `#output.logstash:`

> `#hosts: ["localhost:5044"]`

> To list predefined filebeat modules run the below command

> `sudo filebeat modules list`

> To enable a pre-defined modules run the below command

> `sudo filebeat modules enable <module_name>`

> Setup Ingestion pipelines

> `sudo filebeat setup --pipelines --modules system`

> Setup Kibana Dashboard

> `sudo filebeat setup -E output.logstash.enabled=false -E output.elasticsearch.hosts=['localhost:9200'] -E setup.kibana.host=localhost:5601`
