# Threat model

## What this project does and where untrusted input enters
An in-memory data store (C). Untrusted input: the RESP protocol (commands and arguments),
persistence (RDB/AOF) files, and Lua scripts. The protocol parser and command handlers are the
core untrusted surfaces.

## Components that matter most / least
- most: the RESP protocol parser and the command handlers (especially those touching
  user-provided keys/arguments), plus the Lua engine boundary.
- less: modules, tests.

## How to exercise it
Send crafted RESP commands to a running server; load crafted RDB/AOF files; run edge-case Lua.

## How you rate severity
- Memory-safety bugs (overflow/UAF) reachable via the protocol: critical (RCE).
- Logic bugs enabling privilege issues: high. DoS: medium.

## Anything to leave alone
- Do not report issues only reachable via privileged (admin) commands as high severity.
