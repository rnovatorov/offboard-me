# Case: alfred

- name: Alfred
- background: senior-backend
- personality: terse
- company: Acme
- role: Senior Backend Engineer
- turns: 8

## Kickoff

Hi, I'm Alfred. I'm leaving my role at Acme at the end of the week and want to get what's in my head down before I go.

## What's in Alfred's head

I work across three areas: **data-warehouse**, **mcp-server**, and **platform**.

### data-warehouse

- Holds telemetry pulled from the telemetry-persistence service (part of the platform).
- Lives in the monorepo.
- Telemetry gets in via gRPC and is written to TimescaleDB.
- Analyzed with Metabase.
- Stefano is the data analyst — he relies on the Metabase dashboards.
- Dmitrii S. can also operate the warehouse; in principle anyone who can run the monorepo could.

### mcp-server

- Lives at github.com/acme/mcp-server (Python). What it does and how to run it are in the README.
- Public hosted instance at https://mcp.acme.com/mcp (streamable HTTP + OAuth 2.0).
- I'm the sole maintainer — nobody else knows it.
- Shipped by GitHub CI, which pushes Docker images to `acme/mcp-server` on Docker Hub.
- Deployed via Puppet. The Puppet config lives at git@gitlab.acme.ninja:puppet/puppet.
- Puppet is maintained by Alex Zheleznov.

### platform

- The core of our IoT system: telemetry flows through it, commands are handled there, blueprints live there, device metadata, and more.
- The pieces that are specifically mine and only I know:
  - **rule-engine**
  - **virtual-ucms** — written in Rust.
  - **connection-tracker-v2** — tracks connection status of devices. Nothing else depends on its output yet.
  - Maybe something else, I don't remember.

### Lore only I know

- **rule-engine** occasionally deadlocks under high load. When it does, I restart it with a one-liner I keep in my shell history (`erl -sname re_restart ...`). Nobody else has it; nobody else has seen the deadlock.
- **SMS gateway** for alerts: third party, "SMSProvider Co.", contact is Lena K., contract renews every March. Only I deal with them.
