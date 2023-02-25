# URL Shortener

## What is a URL Shortener?

A URL shortener is a service that takes a long URL and returns a short URL. 

For example,

```
Long URL: https://www.google.com/search?q=system+design+interview+questions
Short URL: https://bit.ly/3fQZQ9w
```

## Functional requirements

* Users should be able to create a short URL for a long URL.
* Users should be able to access the long URL using the short URL.
* Link expiration after a certain time.

## Non-functional requirements

* The system should be highly available.
* The system should be scalable.

## Extended requirements

* Users should be able to access the statistics of the short URL.
* Prevent abuse of the system.

## Estimation and Calculation

Let's start with the following assumptions:

> Ask the interviewer for the assumptions about scale or traffic.

### Traffic

This is read heavy and write light system. Assume that the read to write ratio is 100:1 with 100 million urls 
created per month.

* Reads per month: 100 million * 100 = 10 billion per month
* Writes per month: 100 million * 1 = 100 million per month

* Write pequests per second: 100 million / (30 days * 24 hrs * 60 min * 60 secs) ~= 40 URLs per second
* Read requests per second: 10 billion / (30 days * 24 hrs * 60 min * 60 secs) ~= 4000 URLs per second

### Bandwidth

Assume that each URL is 200 bytes.

* Incoming bandwidth: 40 * 200 bytes ~= 800 KB per second
* Outgoing bandwidth: 4000 * 200 bytes ~= 8 KB per second

### Storage

We assumed that each URL is 200 bytes. Then, we need to store 100 million URLs per month.

* Storage per month: 100 million * 200 bytes ~= 20 GB per month
* Storage per year: 20 GB * 12 months ~= 240 GB per year
* Storage per 10 years: 240 GB * 10 years ~= 2.4 TB per 10 years

### Cache Memory

We assumed that each URL is 200 bytes. We have 4000 read requests per second.

Daily read requests: 4000 * 60 minutes * 60 seconds * 24 hours ~= 350 million per day

According to the 80-20 rule [Pareto Principle](https://en.wikipedia.org/wiki/Pareto_principle), 20% of the URLs are accessed 80% of the time. 
So, we need to cache 20% of the URLs.

* Cache memory: 350 million * 0.2 * 200 bytes ~= 14 GB per day

Estimation and calculation is done. Finally, we have the following estimates:

- Writes: 40/s
- Reads: 4000/s = 4 KB/s
- Incoming bandwidth: 800 KB/s
- Outgoing bandwidth: 8 KB/s
- Storage for 10 years: 2.4 TB
- Cache memory: ~14 GB/day

## Data Models

* URL
    * id
    * long_url
    * short_url
    * expires_at
    * user_id
    * num_of_clicks

* User
    * id
    * name
    * email

(�) What kind of database should we use? (SQL or NoSQL)

Data does not need to be relational. So, we can use a NoSQL databases such as DynamoDB, MongoDB, Cassandra, etc.

## API Design

* Create a short URL
    * Request
        * long_url
        * expires_at
        * api_key
    * Response
        * short_url

* Get a long URL
    * Request
        * short_url
        * api_key
    * Response
        * long_url

* Delete a short URL
    * Request
        * short_url
        * api_key
    * Response
        * status

(�) Why do we need an API key?

* To track and control how the API is being used by client applications.
* Limit the number of requests per second or minute.
* This is a standard security measure to prevent abuse of the system.

## High-Level Design







