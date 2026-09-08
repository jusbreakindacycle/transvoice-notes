# Future Cloud Architecture

Last updated: 2026-09-09

## Status

`OUT_OF_SCOPE` for the local MVP.

This document exists to prevent improvised backend architecture later.

No cloud resources should be created during early local phases.

## Cloud product boundary

The first cloud feature should be:

**Improve Transcript**

Cloud is not a silent fallback.

The user explicitly selects:

- Improve this section;
- Improve entire transcript.

## Minimal future flow

```text
Mobile app
  ↓
authenticated/entitled request
  ↓
rate + quota + cost check
  ↓
create idempotent improve job
  ↓
signed temporary upload
  ↓
queue or direct worker/provider call
  ↓
result validation
  ↓
proposed improved transcript
  ↓
user accept/reject
  ↓
temporary cloud audio cleanup
```

## Managed-first principle

A managed service such as Supabase may be evaluated for:

- Auth;
- Postgres;
- RLS;
- object storage;
- lightweight server orchestration.

It is not a binding platform decision.

Heavy speech inference should run in an environment suitable for sustained inference workloads or through a dedicated provider—not merely because a function runtime exists.

## Early backend requirements

When cloud begins, implement before scale theater:

- authentication;
- authorization/RLS;
- signed private storage access;
- rate limiting;
- quotas;
- request-size limits;
- timeouts;
- bounded retries;
- exponential backoff with jitter;
- idempotency;
- schema migrations;
- indexes;
- secrets management;
- structured redacted logs;
- metrics;
- cost monitoring;
- backups;
- restore validation;
- health checks;
- rollback.

## Retry rule

Do not blindly retry non-idempotent mutations.

Cloud processing jobs require stable identifiers and explicit state transitions.

## Cost safety

Before a costly job starts:

- verify entitlement;
- verify quota/credit;
- reject excessive duration;
- prevent duplicates;
- cap concurrency;
- record cost estimate/actual cost where available.

Prefer segment-level improvement because it reduces:

- cost;
- latency;
- privacy exposure;
- bandwidth.

## Scale ladder

### Stage A — Local product
No backend required.

### Stage B — First cloud users
Managed auth/database/storage + simple job processing.

### Stage C — Growing workload
Dedicated queue, dead-letter handling, autoscaling workers, provider circuit breaker, stronger observability if metrics justify it.

### Stage D — Large workload
Read replicas, partitioning, regional workers, API gateway, additional caching where bottlenecks exist.

### Stage E — Very large/global
Consider sharding, multi-region active-active, sophisticated distributed coordination, or orchestration only with real production evidence.

## Explicit non-goals before evidence

Do not introduce early:

- Kubernetes;
- Kafka;
- microservices;
- Saga pattern;
- distributed locks;
- sharding;
- service mesh;
- multi-region active-active.

Knowing those concepts is not a reason to deploy them.
