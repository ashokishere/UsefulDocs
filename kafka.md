

## Kafka Index.

The topic name is like a table name in the database. But partition and offset are just numbers. In databaseapplications,
we may want to access data on some critical columns such as invoice_number, customer_name, or customer_id.
However you cannot do that in Kafka because messages are not structured into column names that why arrangement is based
on Topic name, partition number, and then the offset number 

In a stream processing application, the requirement is different. A stream processing application wants to read all 
messages in a sequence.Let's assume that you have a stream processing application that computes loyalty points for the customer
in real-time. The application should read each invoice and calculate loyalty point.While computing loyalty points, 
you need customer_id and the amount, but you must read all the events.
 
The application connects to the broker and asks for the messages is starting from the offset zero.Let's assume the broker send
ten messages to the application.The application takes a few milliseconds to compute loyalty points on those 10 invoices.
Now it is again ready to process a few more messages. So, it goes back to the broker and requests formore messages starting from offset 0010.
The broker provides another batch of 15 messages. Next time the application requests for another set of messages
This process continues for the life of the application. the consumer application is requesting messages based on the offset.
Kafka allows consumers to start fetching messages from a given offset number.

example:  if consumer demands for messages beginning at offset hundred, the broker must be able to locate
the message for offset hundred. To help brokers rapidly find the message for a given offsetKafka maintains an index of offsets. 
The index files are also segmented for easy management, and they arealso is stored in the partition directory along with the log file segments.
The time index. Kafka allows consumers to start fetching messages based on the offset number.

We can also seek messages based on timestamp. all the events that are created after a specific timestamp. To support such needs,
Kafka also maintains the timestamp for each message builds a time index to quickly seek the first message that arrived after the given timestamp.

The time index is like the offset index, and it is also segmented and stored in the partition directory
along with the offset index and log final segment.

There are other types of files in the partition directory. But those files have nothing to do with the data.
Kafka creates those files to keep some control information and clean them from time to time.

### Kafka Cluster

scalability side of Apache Kafka  
 
Kafka Brokers are often configured to form a cluster. A cluster is nothing but a group of brokers that work together to share the workload, 
and that's how Apache Kafka becomes are distributed and scalable system. 

We can have  a single broker in our development environment and deploy a cluster of three or five brokers in your production environment.
Later, as the workload grows you can increase the number of brokers in the cluster. It can grow up to hundreds of brokers in a single cluster.

 Who manages cluster membership?  
 Who performs the routine administrative tasks in the cluster?   

In a typical distributed system, master node that 
  maintains a list of active cluster members.
  knows the state of the other members.  
  manages the list of active brokers
  maintains who joined the cluster?
  reassign that work to an active broker to ensure that the cluster continues to function.

## Zookeeper Role in Kafka

