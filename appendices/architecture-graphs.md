# گراف معماری و جریان داده

```mermaid
flowchart LR
  UI[Chart Terminal] --> API[FastAPI Inbound]
  API --> APP[Application]
  APP --> DOM[Domain]
  DOM --> PORT[Ports]
  PORT --> PG[(PostgreSQL)]
  PORT --> CH[(ClickHouse)]
  PORT --> BUS[NATS JetStream]
  PORT --> REDIS[(Redis Cache)]
  MD[Market Providers] --> AD[Adapters]
  AD --> BUS
  BUS --> W[Workers]
  W --> CH
  W --> PG
  CH --> ENG[Canonical Engines]
  ENG --> SIG[Signals/Consensus]
  SIG --> RISK[Risk]
  RESEARCH[Web/GitHub Research] --> FABRIC[Research Fabric]
  FABRIC --> ELY[Elyrava]
  ELY --> POLICY[Policy Gateway]
  POLICY --> TOOLS[Authorized Tools/Sandbox]
```

## گراف وابستگی معنایی
`Provider → Observation → Normalization → Instrument/Series → Structure → Feature → Signal → Evidence/Consensus → Risk → Presentation`

`Source → Provenance → Dataset Revision → PIT → Replay → Outcome → Calibration → Model Governance`

## گراف agent
`Intent → Policy → Tool Authorization → Action → Evidence → Verification → Health → Rollback/Escalation`

هیچ مسیر مستقیمی از UI یا agent به persistence حساس بدون application/policy boundary مجاز نیست.
