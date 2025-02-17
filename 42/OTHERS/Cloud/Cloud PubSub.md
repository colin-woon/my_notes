- a messaging service
- mainly used for event-driven systems + real time data-processing
- handles communication between different parts of a distributed system

**4 key terms**
- Topics (message channel/category)
- Publishers (sends messages to topic, eg: application, services, devices)
- Messages (contains data)
- Subscribers (receive messages from topic, eg: cloud functions, application, services)

**Types of processes**
- **push**
	- **Definition:** sends messages to predefined endpoint (usually when creating a subscription, an endpoint that can receive requests is specified)
	- **Endpoint**
		- endpoint must be reachable via DNS
		- have SSL certificate
	- **Load Balancing**
		- the push endpoint itself can be the load balancer which distributes the request to the backend
		- use case usually in frontend with multiple subscriptions pointing to 1 endpoint, as you add new topics, no need to modify subscriber
	- **Flow Control**
		- when endpoint returns error or takes long time to respond, Pub/Sub will automatically send less messages
		- client can also send HTTP error if they cannot handle the message load
	- **Efficiency and Throughput**
		- scale to zero serverless pattern by cloud run, functions, app engine is supported
		- useful when request rate is low or very uneven
		- delivers one message per request, limits maximum outstanding messages
	- **Factors for choosing**
		- multiple topics to be processed by the same webhook (webhooks are typically used for push-processes)
		- app engine standard, and cloud function subscribers
		- using an environment where GCP cant be setup

- **pull**
	- **Definition:** actively request messages from topic
	- **Endpoint**
		- calls the Cloud Pub/Sub API with authorized credentials for pulling
	- **Load Balancing**
		- multiple subscribers can make pull requests to the same shared subscription
		- but each subscriber only can have 1 subscription at a time
	- **Flow Control**
		- client has control of the ackDeadline
	- **Efficiency and Throughput**
		- high throughput per CPU and bandwidth
		- allows batch delivery processing and acknowledgement
		- must always have application running to make requests
	- **Factors for choosing**
		- large volume of messages (>1/s)
		- critical efficiency and throughput 
		- public https endpoint without SSL, cant setup


**Summary of a pubsub process**
- Publishers send a message to a topic, a topic must have a subscription that a subscriber can subscribe to, typically will be created right after a topic is created. Then the subscriber can either actively pull the message from the topic, or pubsub server can push the message to the subscriber.
- Each subscriber is limited to 1 subscription/topic at a time, the subscription will expire after 31 days of inactivity 
- Publisher can specify an **ordering key** to make sure messages are published to a topic **in order**




