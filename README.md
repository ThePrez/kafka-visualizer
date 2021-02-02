# Kafka Visualizer (friendly fork)

A web client for visualizing your Kafka cluster. Developed using **Spring Boot**, **ReactJS** and **Bootstrap 4**.

![Screenshot](https://github.com/enthusiast94/kafka-visualizer/blob/master/screenshot_1.png)

**Why this fork?**
This fork exists only to host a codebase with lower minimum build/runtime requirements. Namely, it builds with a target of Java 11 and does not build the Docker target present in the main project.

## How to build?

Run the following command on the parent maven module `kafka-visualizer`:

`$ mvn package`

The executable jar will be generated under the `target` directory of the `kafkavisualizer/rest` module.

**Requirements:**

1.  Maven
2.  OpenJDK 11
3.  Node Package Manager (npm)

## How to run (locally)?

Run the executable jar using the following command and then navigate to `localhost:8080` on your browser:

`$ java -jar /path/to/kafka-visualizer-rest-1.0-SNAPSHOT.jar --zookeeper=hostname:port --kafka=hostname:port --env=<DEV,QA,UAT or PROD>`

## How to run (Dockerfile)?
The easiest way to deploy this visualizer, if you have Docker available, is to run the main project's dockerfile, like so:
```sh
$ docker pull kbhargava/kafka-visuals
$ docker run -p 8080:8080 --rm kbhargava/kafka-visuals <zookeeper IP:Host> <kafka IP:host> <DEV, PROD, UAT, QA>
```

Verify the deployment by navigating to your server address in your preferred browser.

```sh
localhost:8080
```

## Rest API endpoints

- **`GET /api/brokers`**: Returns a list of all brokers in the cluster.
- **`GET /api/topics`**: Returns a list of all topics in the cluster
- **`GET /api/consumers`**: Returns a list of all active consumers.
- **`GET /api/consumers/{topicName}/{partition}`**: Returns a list of active consumers for a certain topic-partition pair.
- **`GET /api/topics/{topicName}/{partition}`**: Returns a list of messages on a certain topic-partition pair.
- **`POST /api/topics/{topicName}`**: Accepts `text/plain` message with a `key` and a `value` (eg: key=1&value=2), and publishes it to a certain topic.
