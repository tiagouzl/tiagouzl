# Tiago Rodrigues de Brito

**Software Developer · Independent contractor (MEI) · Mossoró/RN, Brazil**

Coding Technology degree from UNINASSAU. I work on software development,
maintaining my own projects in production alongside experimental ones.

Some of the projects below started as academic exercises and continued after
them. They share an approach: implement parts of the system from scratch to
understand the internals, measure behavior, and validate the decision before
trusting an off-the-shelf abstraction.

## In production

### Sistema T2 — Home Care Management ERP

A vertical healthcare management platform for T2 Empreendimentos Médicos
Ltda., used across multiple municipalities in Rio Grande do Norte. I was the
sole developer responsible for its implementation and maintenance.

The product integrates operational, administrative, and financial workflows:
municipal contracts and service rules, care production, attendance guides,
shifts and schedules, field time tracking, patient and professional records,
home visits, payments, and management reports. Its accurate category is a
**vertical healthcare ERP specialized in Home Care** — not a CRM or a standalone
BI product.

A central engineering challenge was field operation in municipalities with
unreliable connectivity. I implemented an offline synchronization queue with
IndexedDB, allowing time records to be retained locally and synchronized when
connectivity returns. The platform also applies municipality-specific
presentation rules to reports while preserving internal operational data as
the source of truth.

Closed source under contract. The public case-study repository documents
architecture and engineering decisions:
[t2-case-study](https://github.com/tiagouzl/t2-case-study).

### Garbos-CRM

Management system for a graduation photography company, in production since
March 2026. Built during my work as a full-time employee (CLT) at Garbos.
Closed source.

---

## Featured projects

### [little-hawk](https://github.com/tiagouzl/little-hawk)

Streaming LLM inference engine in Python/NumPy, no PyTorch or CUDA. Started
as a way to study attention, KV-cache, and autoregressive generation
directly.

More important than the engine working was the validation methodology. I
implemented an alternative KV-cache eviction policy (nexus-salience); the
first result looked like a win over baseline, I found a state-contamination
bug between calls inflating the number, fixed it, and reran the comparison
paired — only accepting the result once it was statistically significant
(p=0.0156).

I also tested speculative decoding: technically functional, but
verification cost wiped out the gain (0.995×, no real improvement). Kept
that negative result documented instead of omitting it.

### [sosia](https://github.com/tiagouzl/sosia)

File deduplicator in Rust, with a four-stage pipeline — size → 4 KiB
partial hash → full BLAKE3 → output — designed to never read bytes it
doesn't need.

The benchmark measures true cold cache (drops kernel pages between rounds)
and cross-checks the optimized pipeline's duplicate groups against a naive
baseline — divergence is treated as a bug, not just speed; correctness is
measured too. Result: ~9× faster than hashing everything, with methodology
and limitations documented in the README.

### [pingenty](https://github.com/tiagouzl/pingenty)

Async network monitor in Rust: ICMP/ICMPv6 with TCP fallback, passive
capture with 802.1Q/QinQ VLAN support, TUI dashboard.

The decision most worth reading: I compared a global lock vs. a 16-shard
map for the flow registry under real contention from 1 to 8 threads. The
global lock collapses at 8 threads — but the current architecture uses one
capture thread per interface, so that contention doesn't exist today. I kept
the global lock and documented the exact trigger (N concurrent captures)
that would justify switching.

---

## Stack

Python (NumPy, FastAPI) · Rust (Tokio, Rayon, BLAKE3) · TypeScript (Next.js,
React) · Java (Spring Boot, Spring AI) · Bash · PostgreSQL/Supabase

---

## Contact

- GitHub: [@tiagouzl](https://github.com/tiagouzl)
- E-mail: tiago.uzl@gmail.com
- LinkedIn: [tiago-rodrigues-63a63383](https://www.linkedin.com/in/tiago-rodrigues-63a63383/)
