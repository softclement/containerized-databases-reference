# Free and Community Containerized Databases

> A practical reference of free, open-source, Community Edition, and developer/free-tier databases available as container images — for local labs, PoCs, learning, and training.

![Docker](https://img.shields.io/badge/Docker-Compatible-2496ED?logo=docker&logoColor=white)
![Podman](https://img.shields.io/badge/Podman-Compatible-892CA0?logo=podman&logoColor=white)
![License](https://img.shields.io/badge/Repo%20License-MIT-brightgreen)

The repository covers relational, document/key-value, wide-column, graph, time-series, search/analytics, vector, embedded, and cloud-service emulator categories.

> [!IMPORTANT]
> **"Free" does not always mean "open source."** Licensing, image names, registry locations, availability, resource requirements, and usage restrictions can change over time. Always verify the vendor's current documentation and license before using an image in production or commercial environments.

### What you'll find

- Container image name and tag
- Source or container registry
- Database category
- Short product description
- Licensing / Community Edition classification
- Approximate resource footprint (Low / Medium / High)
- Quick Podman **and** Docker pull examples
- Container lab best practices
- WSL2-oriented guidance
- Notes on vendor registries and authentication

The **README is the detailed, maintained reference**. The accompanying presentation (`Containerized_Databases_Community_Editions.pptx`) is a **curated visual overview** of the same material — it doesn't try to list every entry here.

---

## Purpose

This repository is a practical reference for discovering databases and database-related services that can be run locally using containers. It focuses on free, open-source, Community Edition, developer/free-tier, and local-emulator offerings suitable for learning, experimentation, PoCs, and training.

## Scope & Classification

Not every entry below is "open source" in the OSI sense. To avoid that confusion, every database is tagged with one of four categories:

| Tag | Meaning | Examples |
|---|---|---|
| **OSS** | Open source under an OSI-approved license (Apache 2.0, MIT, BSD, GPL, etc.) | PostgreSQL, MariaDB, Cassandra, OpenSearch |
| **CE** | Vendor-labeled "Community Edition" — free to use, but not always under an OSI license | Db2 CE, MongoDB Community, Couchbase CE, ArangoDB CE |
| **Free/SA** | Free to use but proprietary or source-available (non-OSI license, e.g. BSL, SSPL) | CockroachDB, Elasticsearch, Oracle Database Free |
| **Emulator** | A local emulator for a cloud-hosted service, not a standalone database product | LocalStack, Azure Cosmos DB Emulator |

Each table below also shows an approximate **Resource** footprint (**L**ow / **M**edium / **H**igh) — a rough sizing guide for laptop-scale labs, not an exact RAM/CPU spec, since real requirements vary by configuration and version.

A ✅ in the **Tested** column means the author has personally run that image in a local lab — everything else is catalogued from public vendor/community registries but not personally verified end-to-end. See [Reference vs. Tested](#reference-vs-tested) below.

## Disclaimer

Licensing, image names, registry locations, availability, resource requirements, and usage restrictions can change at any time. Image tags (including `:latest`) are not guaranteed to remain stable between pulls. Always verify the vendor's current documentation and license — including for commercial or production use — before relying on any image listed here.

This repository's own license (MIT, see [`LICENSE`](./LICENSE)) applies **only to this README, the presentation, and any original documentation/scripts in this repository** — it does **not** change or override the license of any database software or container image listed below.

> [!IMPORTANT]
> Every image below is referenced by its **`:latest`** tag for discovery and quick-start purposes. **For reproducible labs, CI/CD pipelines, training material, or shared PoCs, pin an explicit version tag instead** — `:latest` can change (sometimes with breaking changes) without notice.

---

## Relational (RDBMS)

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| PostgreSQL | `postgres:latest` | [hub.docker.com/_/postgres](https://hub.docker.com/_/postgres) | Advanced open-source relational database known for standards compliance and strong ACID guarantees. | OSS | L | ✅ | No separate CE needed |
| MySQL | `mysql:latest` | [hub.docker.com/_/mysql](https://hub.docker.com/_/mysql) | Widely used open-source relational database, commonly paired with web applications. | OSS | L | | GPL license |
| MariaDB | `mariadb:latest` | [hub.docker.com/_/mariadb](https://hub.docker.com/_/mariadb) | Community-driven MySQL fork with additional storage engines and replication features. | OSS | L | | Drop-in MySQL compatible |
| IBM Db2 Community Edition | `icr.io/db2_community/db2:latest` | [github.com/IBM/Db2CommunityEdition](https://github.com/IBM/Db2CommunityEdition) | IBM's enterprise relational engine with advanced analytics and HA/DR features. | CE | H | ✅ | IBM Container Registry login required; rootful Podman recommended on WSL2 |
| Oracle Database Free | `container-registry.oracle.com/database/free:latest` | [container-registry.oracle.com](https://container-registry.oracle.com/) | Full-featured Oracle Database engine, free for development and small production use. | Free/SA | H | ✅ | No license key required; proprietary license applies |
| CockroachDB | `cockroachdb/cockroach:latest` | [hub.docker.com/r/cockroachdb/cockroach](https://hub.docker.com/r/cockroachdb/cockroach) | Distributed SQL database built for resilience and horizontal scale-out. | Free/SA | M | ✅ | BSL license; free for most non-production / PoC use |

## Document / Key-Value

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| MongoDB Community | `mongodb/mongodb-community-server:latest` | [hub.docker.com/r/mongodb/mongodb-community-server](https://hub.docker.com/r/mongodb/mongodb-community-server) | Leading document database storing flexible, JSON-like BSON documents. | CE | M | ✅ | SSPL-licensed; legacy `mongo` image deprecated for new major versions |
| Couchbase Community Edition | `couchbase/server:community` | [hub.docker.com/r/couchbase/server](https://hub.docker.com/r/couchbase/server) | Distributed NoSQL database combining document storage, caching, and SQL-like N1QL querying. | CE | M | ✅ | Use the `community` tag explicitly |
| Redis | `redis:latest` | [hub.docker.com/_/redis](https://hub.docker.com/_/redis) | In-memory data structure store used for caching, sessions, and pub/sub messaging. | OSS | L | | BSD-3 licensed as of Redis 8 |
| Valkey | `valkey/valkey:latest` | [hub.docker.com/r/valkey/valkey](https://hub.docker.com/r/valkey/valkey) | Linux Foundation-governed, fully open-source continuation of Redis. | OSS | L | | Drop-in API compatible with Redis |

## Wide-Column / NewSQL

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| Apache Cassandra | `cassandra:latest` | [hub.docker.com/_/cassandra](https://hub.docker.com/_/cassandra) | Highly available wide-column store for large-scale, write-heavy workloads. | OSS | M | ✅ | Docker Hub official image |
| ScyllaDB Open Source | `scylladb/scylla:latest` | [hub.docker.com/r/scylladb/scylla](https://hub.docker.com/r/scylladb/scylla) | Cassandra/DynamoDB-compatible database rewritten in C++ for lower latency. | OSS | M | | Drop-in Cassandra alternative |
| TiDB | `pingcap/tidb:latest` | [hub.docker.com/r/pingcap/tidb](https://hub.docker.com/r/pingcap/tidb) | MySQL-compatible NewSQL/HTAP database for combined transactional + analytical workloads. | OSS | H | | Typically needs a multi-container cluster setup |

## Graph

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| Neo4j Community Edition | `neo4j:latest` | [hub.docker.com/_/neo4j](https://hub.docker.com/_/neo4j) | Native graph database optimized for traversing connected relationship data. | OSS | M | | GPLv3; Enterprise needs an explicit tag + license |
| ArangoDB Community Edition | `arangodb/arangodb:latest` | [hub.docker.com/r/arangodb/arangodb](https://hub.docker.com/r/arangodb/arangodb) | Multi-model database combining document, graph, and key-value in one engine. | CE | M | | Business Source License on recent versions — verify current terms |

## Time-Series

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| InfluxDB OSS | `influxdb:latest` | [hub.docker.com/_/influxdb](https://hub.docker.com/_/influxdb) | Purpose-built time-series database for metrics and real-time monitoring. | OSS | L | | v1 and v2 APIs differ significantly — confirm which the tag resolves to |
| TimescaleDB | `timescale/timescaledb:latest` | [hub.docker.com/r/timescale/timescaledb](https://hub.docker.com/r/timescale/timescaledb) | PostgreSQL extension adding scalable time-series capabilities with full SQL. | OSS | L | | Community edition; some features are Timescale-licensed |

## Search / Analytics

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| OpenSearch | `opensearchproject/opensearch:latest` | [hub.docker.com/r/opensearchproject/opensearch](https://hub.docker.com/r/opensearchproject/opensearch) | Search and analytics suite forked from Elasticsearch, with visualization tooling. | OSS | M | | Apache 2.0, fully OSI-approved |
| Elasticsearch | `docker.elastic.co/elasticsearch/elasticsearch:latest` | [docker.elastic.co](https://www.docker.elastic.co/) | Distributed search and analytics engine widely used for log analytics. | Free/SA | H | | SSPL-licensed since 7.11; OpenSearch is the OSS alternative |
| Apache Solr | `solr:latest` | [hub.docker.com/_/solr](https://hub.docker.com/_/solr) | Enterprise search platform built on Apache Lucene. | OSS | M | | Docker Hub official image |
| ClickHouse | `clickhouse/clickhouse-server:latest` | [hub.docker.com/r/clickhouse/clickhouse-server](https://hub.docker.com/r/clickhouse/clickhouse-server) | Column-oriented OLAP database built for fast aggregate queries. | OSS | M | | |
| Apache Druid | `apache/druid:latest` | [hub.docker.com/r/apache/druid](https://hub.docker.com/r/apache/druid) | Real-time analytics database for sub-second OLAP queries. | OSS | H | | Typically needs a multi-container Compose setup |

## Vector Databases (AI/ML workloads)

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| Milvus | `milvusdb/milvus:latest` | [hub.docker.com/r/milvusdb/milvus](https://hub.docker.com/r/milvusdb/milvus) | Purpose-built vector database for similarity search over large embedding sets. | OSS | M | | Standalone mode fits single-node labs |
| Qdrant | `qdrant/qdrant:latest` | [hub.docker.com/r/qdrant/qdrant](https://hub.docker.com/r/qdrant/qdrant) | Vector similarity search engine with a simple REST/gRPC API. | OSS | L | | |
| Weaviate | `semitechnologies/weaviate:latest` | [hub.docker.com/r/semitechnologies/weaviate](https://hub.docker.com/r/semitechnologies/weaviate) | Vector database with built-in modules for hybrid keyword + semantic search. | OSS | M | | BSD-3 licensed |
| pgvector | `pgvector/pgvector:latest` | [hub.docker.com/r/pgvector/pgvector](https://hub.docker.com/r/pgvector/pgvector) | PostgreSQL extension enabling native vector storage and similarity search. | OSS | L | | Good fit alongside existing PostgreSQL labs |

## Embedded / Lightweight

| Database | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| H2 Database | `oscarfonts/h2:latest` | [hub.docker.com/r/oscarfonts/h2](https://hub.docker.com/r/oscarfonts/h2) | Java-embedded SQL database, mostly used for testing and lightweight local dev. | OSS | L | | Community-maintained, not an official image |

## Cloud-Service Local Emulators
*Free, containerized local emulators — not standalone databases, but commonly paired with the categories above for offline development.*

| Service | Container Image | Source / Repository | What it is | License | Resource | Tested | Notes |
|---|---|---|---|---|---|---|---|
| LocalStack | `localstack/localstack:latest` | [hub.docker.com/r/localstack/localstack](https://hub.docker.com/r/localstack/localstack) | Local cloud emulator mimicking AWS services (S3, DynamoDB, and more). | Emulator | M | ✅ | Updates frequently — verify compatibility after pulling |
| Azure Cosmos DB Emulator | `mcr.microsoft.com/cosmosdb/linux/azure-cosmos-emulator:latest` | [MS Container Registry](https://mcr.microsoft.com/en-us/product/cosmosdb/linux/azure-cosmos-emulator) | Local emulator for Azure Cosmos DB, supporting NoSQL, Mongo, and Cassandra APIs. | Emulator | H | | Linux emulator supports Mongo & Cassandra APIs |

---

### Reference vs. Tested

- **Reference** — catalogued from public vendor/community registries; image name, repo link, and description are accurate as of this writing but not personally re-verified.
- **Tested (✅)** — personally pulled and run in the author's local Podman/WSL2 lab as part of a hands-on PoC.

---

## ⚡ Quick Pull Reference

Examples default to **Podman** (the author's primary tooling), with **Docker** equivalents alongside — most images here work identically under either.

```bash
# ── Podman ──────────────────────────────────────────
podman pull docker.io/library/postgres:latest
podman pull icr.io/db2_community/db2:latest
podman pull docker.io/mongodb/mongodb-community-server:latest
podman pull docker.io/couchbase/server:community

# ── Docker ───────────────────────────────────────────
docker pull docker.io/library/postgres:latest
docker pull icr.io/db2_community/db2:latest
docker pull docker.io/mongodb/mongodb-community-server:latest
docker pull docker.io/couchbase/server:community
```

> [!TIP]
> The examples above use Podman, but any Docker-compatible image (which is nearly all of them) can be pulled the same way with `docker pull` instead of `podman pull`. For rootful Podman on WSL2, prefix with `sudo podman` where an image bakes in root-owned data directories (Db2, Oracle Free).

---

## WSL2 Lab Environment

These container images run identically under Docker or Podman on native Linux. For Windows users, **WSL2** provides a convenient Linux environment for running database containers locally without a separate VM.

```text
Windows
   |
   +-- WSL2 (Ubuntu)
        |
        +-- Podman / Docker
              |
              +-- PostgreSQL
              +-- Db2
              +-- MongoDB
              +-- Couchbase
              +-- ...
```

Most of the "Tested" entries above were run this way — rootful Podman on WSL2 Ubuntu — which is a reasonable default for labs that need root-owned data directories (e.g. Db2, Oracle Free).

---

## ✅ Best Practices for Container DB Labs

A few habits that save time once you move past a single quick-start container:

- **Persist data with named volumes** — container filesystems are ephemeral by default; mount a named volume so data survives a container restart or rebuild.
- **Use a dedicated network per lab** — put related containers (DB + app + cache) on their own Podman/Docker network instead of relying on host networking.
- **Change default credentials immediately** — most images ship with well-known default users/passwords; rotate them before exposing any port beyond localhost.
- **Right-size memory limits** — Db2, Elasticsearch, and Cassandra images assume generous defaults; set explicit memory limits for laptop-scale labs (see the Resource column above).
- **Keep secrets out of Compose files** — use an `.env` file or a secrets manager rather than hardcoding passwords directly into `docker-compose.yml`.
- **Snapshot before major upgrades** — take a logical backup (`pg_dump`, `mongodump`, etc.) before pulling a new major version tag over an existing volume.

---

## Notes & Caveats

- **Vendor registries differ** — Db2, Oracle Free, and Couchbase pull from vendor registries (`icr.io`, `container-registry.oracle.com`) rather than Docker Hub — separate login/auth steps apply.
- **MongoDB** — the classic `mongo` image is deprecated for new major versions; use `mongodb/mongodb-community-server` instead.
- **Elasticsearch licensing** — changed to SSPL in 7.11; if a fully OSI-approved license matters, OpenSearch is the safer pick.
- **CockroachDB license** — BSL, not pure open source, but free to use for most non-production/PoC purposes.
- **`:latest` tags move** — this reference uses `:latest` throughout for simplicity, but registries update it over time. A handful of images (e.g. LocalStack) have introduced breaking changes between releases — re-test after any pull, and pin an explicit version tag once a lab moves toward something repeatable or shared with others.
- **Licenses can change** — several vendors (MongoDB, Elasticsearch, ArangoDB, HashiCorp-style products generally) have changed licensing terms in recent years. Don't assume today's classification in this README will hold indefinitely — check before production or commercial use.

---

## Want to contribute another database?

This repository intentionally stays curated rather than exhaustive — it's easy for a reference like this to balloon into hundreds of rows and become unmaintainable. If there's a free, open-source, Community Edition, or emulator-based database image you think belongs here, open a pull request or an issue with:

- Database name and container image (`image:tag`)
- Link to the official source/registry
- A one-sentence description
- License classification (OSS / CE / Free-SA / Emulator)

---

## License

This repository is licensed under [MIT](./LICENSE). That license covers the README, presentation, and any original documentation/scripts here — it does **not** apply to, or change, the license of any database software or image listed above.

---

## ✍️ Author

**Mariyan Clement**
[linkedin.com/in/mariyanclement](https://www.linkedin.com/in/mariyanclement/)

*Compiled for local lab, PoC, and training reference use.*
