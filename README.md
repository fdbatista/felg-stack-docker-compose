**DESCRIPTION:**

Each service has its own folder with configuration and data folders. Explore and adjust to make them meet your own needs.
This setup uses Elastic Stack components' Filebeat, Logstash and ElasticSearch, and visualizes data in a Grafana dashboard which is being fed by ElasticSearch.

- Configuration file `filebeat\config\filebeat.yml` tells Filebeat to read the contents of `filebeat\data\misc.log` file and forward them to Logstash instance.
- Logstash pipeline definition in `logstash\pipeline\misc.conf` reads the input from Filebeat on port 5044, separates the content into fields via the `dissect` filter and uses the `date` field as the timestamp field for the log entry (using `date` filter).
- The resulting output is shipped to ElasticSearch instance running on port 9200 using index `filebeat-misc`.

**TESTED ENVIONMENT:**
- Docker 19.03.6 and Docker Compose 1.21.0.

**INSTRUCTIONS:**
- Clone the repository.
- Execute `docker-compose up`. It may take some time to start the services if you do not have the docker images on your system.
- Navigate to `http://localhost:9200/filebeat-misc/_search` to see the ElasticSearch endpoint or to `http://localhost:3000` to see the Grafana dashboard in action.
