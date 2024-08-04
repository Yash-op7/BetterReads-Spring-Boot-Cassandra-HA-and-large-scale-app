# BetterReads-Spring-Boot-Cassandra-HA-and-large-scale-app
Built an enterprise grade application that is highly available, scalable to millions of users, can handle large amounts of data and is highly performant with low latency.

This is a end-to-end Spring Boot book tracking application with a vast database on all the books built using Java Spring Boot and Cassandra which allows the user to track the book they are currently reading or have read, give ratings and reviews, have access to a vast catalog of all published books and more.

### Technologies used:
- Cassandra
    - Motivation: To build for scalability, performance and reliability that Cassandra provides, this app is supposed to be highly performant even with a large number of users, therefore I used Cassandra because:
        - its a NoSQL DB so we don't have to do sacrifice performance in expenisve joins as our dataset is vast, suppots key-based lookup
        - store metadata on millions of books
        - very flexible, document store
        - scales up or down elastically based on the load
        - a distributed database, bunch of nodes in a cluster which makes it reliable, fault tolerant and scalable
    - using a hosted Cassandra instance via AstraDB by DataStacks
- Spring Boot
- Spring Security:
    - For a OAuth login via Github functionality
- ThymeLeaf
- Spring Data for Apache Cassandra:
    - To get the use of model based interactions, repository patterns similar to Spring JPA

### Data source
https://openlibrary.org/developers/dumps
https://openlibrary.org/developers/api

# HDD
## 1. User Experience
Let's first identify the UX, because it gives a good idea about:
- overall flow of the app
- the type of data that we will deal with, how will we retrieve them in common usage patterns, common queries that we need to perform efficiently so we need to optimize the structure of the data model (because unlike a RDBMS where we can have normalized tables and we can focus on the app first and not worry about efficieny of queries, here in a NoSQL document datastore we have more flexibiity of data schemas so we must identify optimal structure then build the application around the data structure for efficient querying)

**What functionality should the app provide to the users?**
- Home page for logged out users:
    - A search bar to browse the book catalog
    - A login via Github button
- Home page for logged in users:
    - A list of last 50 books read in reverse chronological order
- Book page which provides:
    - An image of the book cover
    - Title and Description of the book
    - A link to the Author's page for this book
    - Information related to the user such as:
        - Start date
        - End date
        - Rating
        - Status
- Author page which provides:
    - Profile of the author
    - A list of books in reverse chronological order that the author has published
- Search page:
    - search by title
    - search by author


## 2. System Design
**Some non-functional requirements/goals that we want to achieve in our application:**
1. Should be performant
2. Can handle large data
3. Reliable, HA
4. Backend Focussed (personal goal, not wasting time with CSS for now, will do that later in free time)

**Architecture:**
- **Spring Boot** backend with Spring MVC to serve HTML pages to users
- **Spring Security** for login
- A non relational database for high performance and reliablity as RDBMS are single store so no fault tolerance, so we use **Apache Cassandra** a reliable NoSQl, performant database for large data.
- **Spring Data for Apache Cassandra** to connect to DB
- **Open Library API** for search functionality (Apache is not meant to be used for full table searches, it allows lookup of data but not fast 'like' queries similar to RDBMS, to search in Cassandra we can use Apache Lucene for indexes but I will make one exception and implement it later(maybe) as it will add lot of complexity)

## 3. Application Architecure and Data Model Architecture
![architecture_diagram](assets/architecture_diagram.png)

{{< caption >}}The [Amazon Rainforest](https://en.wikipedia.org/wiki/Amazon_rainforest) contains a multitude of species.{{< /caption >}}