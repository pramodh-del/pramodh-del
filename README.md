<a href="https://pramodh-del.github.io">
  <img src="assets/header.svg" width="100%" alt="Kadam Pramodh. Backend engineer, Java 21, Spring Boot, AWS. Hyderabad, 2 years 4 months at Accenture, AWS Certified, open to backend roles." />
</a>

<p align="center">
  <a href="https://pramodh-del.github.io"><img src="https://img.shields.io/badge/Portfolio-pramodh--del.github.io-14161F?style=flat-square" alt="Portfolio" /></a>
  <a href="https://pramodh-del.github.io/#/resume"><img src="https://img.shields.io/badge/Resume-view_online-6DB33F?style=flat-square" alt="Resume" /></a>
  <a href="https://www.linkedin.com/in/kadam-pramodh-88975432a"><img src="https://img.shields.io/badge/LinkedIn-Kadam_Pramodh-0A66C2?style=flat-square" alt="LinkedIn" /></a>
  <a href="mailto:pramodhkadam222@gmail.com"><img src="https://img.shields.io/badge/Email-pramodhkadam222%40gmail.com-C74634?style=flat-square" alt="Email" /></a>
</p>

### The 30-second version

- **Backend engineer at Accenture** for 2 years 4 months on a Fortune 500 US insurance platform. Joined as an Associate in May 2024 and was **promoted to Analyst in June 2026**.
- I build **Java 21 / Spring Boot** services end to end. That covers the API design, the SQL tuning, the **AWS infrastructure in Terraform**, and the production defect when something breaks.
- **Looking for** backend engineering roles at product companies and GCCs, in Hyderabad or remote. I reply within a day.

### Shipped in production

| Project | What I did | Result |
| --- | --- | --- |
| **SOAP → Spring Boot** | Moved a 26-operation SOAP service off WebLogic and Ant onto Spring Boot 4 and Apache CXF on Java 21, including the javax → jakarta move, across three Oracle datasources. | Published WSDL **byte-for-byte identical** (SHA-256 checked). **Zero** client changes. |
| **IBM MQ → AWS** | Rebuilt an event and acknowledgement API, then provisioned API Gateway, VPC Link, an internal ALB, ECS Fargate, SQS FIFO with a DLQ, and an S3 claim-check in Terraform. | IBM MQ dispatch **retired**. Failed messages retry 5 times, then wait 14 days in the DLQ. |
| **Oracle Forms → 14 services** | Moved business rules out of Oracle Forms and PL/SQL into 5 experience-layer and 9 domain-layer Spring Boot services on Spring JDBC. | **20–40%** faster on frequently used APIs, with **80%+** test coverage. |
| **A 3-minute timeout** | Traced a production gateway timeout with HAR files and per-hop timing to an unbounded result set. Rebuilt the query path with paging and indexed lookups. | **3+ min → under 60 s.** |
| **GenAI defect triage** | Built an agent that drafts root-cause summaries from recurring defect patterns. A person reviews every draft before anyone acts on it. | Triage went from **about a day to minutes** across 25+ defects. |

> The client owns this code, so none of it is public. The [portfolio](https://pramodh-del.github.io/#/work) walks through each project with a diagram and explains the trade-offs.

### How one of them works

This is the event pipeline from the IBM MQ → AWS project. A message is deleted from SQS only after the database commit, so a crash causes a retry instead of a lost event.

```mermaid
flowchart LR
    caller(["Upstream systems"]) --> apigw["API Gateway (private)"]
    apigw --> link["VPC Link"] --> alb["Internal ALB"] --> svc["ECS Fargate<br/>Spring Boot · Java 21"]
    svc -- "large payloads" --> s3[("S3 claim-check")]
    svc -- "publish" --> sqs[["SQS FIFO"]]
    sqs -- "consume, ack after commit" --> svc
    sqs -- "after 5 failed tries" --> dlq[["Dead-letter queue<br/>kept 14 days"]]
    svc --> db[("Oracle")]
```

### What I work with

<p>
  <img src="https://skillicons.dev/icons?i=java,spring,aws,terraform,docker,maven,jenkins,git,linux" alt="Java, Spring, AWS, Terraform, Docker, Maven, Jenkins, Git, Linux" />
</p>

| Area | Tools |
| --- | --- |
| **Backend** | Java 21 · Spring Boot 4 · Spring MVC · Spring JDBC · Spring Data JPA · Hibernate · REST · SOAP / Apache CXF |
| **Cloud** | AWS (SQS FIFO, ECS Fargate, S3, API Gateway, Lambda) · Terraform · Docker · AWS Certified Cloud Practitioner |
| **Data** | Oracle · SQL tuning · indexing · pagination · UCP connection pooling |
| **Quality** | JUnit 5 · Mockito · integration tests · global exception handling · Splunk |
| **Delivery** | Maven · Jenkins CI/CD · Git · SAFe Agile |

### Right now

- **Building** an HTTP server from raw sockets in plain Java 21. The goal is to see exactly what Tomcat and Spring Boot do for me: thread pools, virtual threads, and what happens when the queue fills up. It will be pinned here once it ships.
- **Learning** Kafka, and what Spring Cloud does under the hood.

### Hiring for a backend role?

The quickest way to reach me is the [contact form on my portfolio](https://pramodh-del.github.io/#/contact) or [email](mailto:pramodhkadam222@gmail.com). My [resume](https://pramodh-del.github.io/#/resume) opens in the browser, and there is a PDF if you need one.
