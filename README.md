# go_rabbitmq_example
Basic RabbitMQ Example working with Go

# Prerequisites

RabbitMQ should be running locally, you should be able to do this using brew install rabbitmq and then starting rabbitmq.
  - check /usr/local/sbin/ for rabbitmq-server

# new_task.go

This file will attach to an channel, bind to a queue (or create it), and publish a message to it to be consumed.

```
go run new_task.go
2017/08/07 08:27:23  [x] Sent hello
```
Or for a different payload:
```
go run new_task.go different task payload
2017/08/07 08:29:23  [x] Sent different task payload
```

# worker.go

This script will attach to the queue generated previously and being consuming messages from the queue.
The worker will echo out the content of the message and then ack the message as complete.

```
go run worker.go
2017/08/07 08:29:39  [*] Waiting for messages. To exit press CTRL+C
2017/08/07 08:29:39 Received a message: hello
2017/08/07 08:29:39 Done
```

# worker_nack.go

This script will attach to the queue generated previously and being consuming messages from the queue.
The worker will echo out the content of the message and then nack the message and return it to the queue.
The worker will wait 10s then try again.

```
go run worker.go
2017/08/07 08:35:04  [*] Waiting for messages. To exit press CTRL+C
2017/08/07 08:35:04 Received a message: hello
2017/08/07 08:35:04 Unable to process message.  Adding back to queue.
2017/08/07 08:35:14 Received a message: hello
2017/08/07 08:35:14 Unable to process message.  Adding back to queue.
```
