# Wirehound

*Track network conversations in real time.*

> Rust rover, Rust rover... send Wirehound right over.

Wirehound is a network debugging tool written in Rust that captures TCP traffic, reconstructs conversations, and decodes plaintext REST API interactions into clean request/response flows.

It is built for one purpose: to make it easy to see exactly what your services are doing on the wire—without drowning in packet-level noise.

---

## Status

Wirehound is in early development.

Initial goals:

- Capture TCP traffic on selected interfaces and ports
- Group traffic into distinct flows and conversations
- Detect and decode plaintext HTTP/1.1 (REST) traffic
- Output readable request/response exchanges

Planned:

- JSON pretty-printing
- Improved TCP stream reconstruction
- Filtering by method, path, host, and port
- HTTP/2 support
- gRPC decoding

---

## Why Wirehound Exists

Packet capture tools are powerful—but often too low-level for day-to-day debugging.

Wirehound focuses on what developers actually care about:

**the conversation**

Instead of raw packets, Wirehound aims to show:

- What request was sent
- What response was returned
- Which services communicated
- How long it took
- What happened across the full exchange

---

## Design Goals

- **Readable** — prioritize clarity over raw packet detail  
- **Focused** — REST first, then expand  
- **Incremental** — build in layers  
- **Useful** — designed for real debugging work  
- **Extensible** — gRPC and beyond later  

---

## Initial Scope

Version 1 is intentionally limited:

- Plaintext traffic only (no TLS)  
- TCP only  
- HTTP/1.1 (REST) first  
- Selected ports only  

This keeps the tool practical and usable early.

---

## Core Concept

Wirehound transforms raw network traffic into structured conversations:

Packet → Flow → Stream → HTTP → Conversation

---

## Example Output (Target)

```text
[conversation]
client: 10.0.0.25:51432
server: 10.0.0.10:8080
method: POST
path: /api/tickets
status: 200 OK
duration: 34ms

request headers:
  content-type: application/json

request body:
  {
    "title": "Printer offline"
  }

response body:
  {
    "id": 1842,
    "status": "open"
  }
```

---

## Roadmap

### Phase 1
- CLI setup  
- Interface selection  
- Packet capture proof of concept  

### Phase 2
- TCP filtering  
- Flow tracking  
- Payload accumulation  

### Phase 3
- HTTP parsing  
- Conversation reconstruction  
- Readable output  

### Phase 4
- Formatting improvements  
- Filtering options  
- JSON pretty-printing  

### Phase 5
- HTTP/2 exploration  
- gRPC decoding  

---

## Philosophy

Wirehound is not trying to replace Wireshark.

It is built to do something narrower and more developer-focused:

**Track conversations and make them readable.**

---

## License

MIT
