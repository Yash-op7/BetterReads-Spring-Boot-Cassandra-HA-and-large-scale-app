# BetterReads-Spring-Boot-Cassandra-HA-and-large-scale-app
Built an enterprise grade application that is highly available, scalable to millions of users, can handle large amounts of data and is highly performant with low latency.

This is a end-to-end Spring Boot book tracking application with a vast database on all the books built using Java Spring Boot and Cassandra which allows the user to track the book they are currently reading or have read, give ratings and reviews, have access to a vast catalog of all published books and more.

### Technologies used:
- Cassandra
    - Motivation: To build for scalability, performance and reliability that Cassandra provides, this app is supposed to be highly performant even with a large number of users, therefore I used Cassandra because:
        - its a NoSQL DB so we don't have to do sacrifice performance in expenisve joins as our dataset is vast
        - store metadata on millions of books
        - very flexible, document store
        - scales up or down elastically based on the load
    - using a hosted Cassandra instance via AstraDB by DataStacks
- Spring Boot
- Spring Security:
    - For a OAuth login via GitHub functionality
- ThymeLeaf
- Spring Data for Apache Cassandra:
    - To get the use of model based interactions, repository patterns similar to Spring JPA
