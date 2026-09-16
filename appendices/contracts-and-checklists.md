# قراردادهای مرجع

## Evidence Record
```text
id
capability
source_type
source_ref
retrieved_at
observed_at
content_hash
claim
verification_method
status
owner
```

## API contract
```text
request_id
actor
resource
operation
input_schema
authorization_policy
entitlement_requirement
idempotency_policy
response_schema
error_schema
telemetry_fields
```

## Event contract
```text
event_id
aggregate_type
aggregate_id
event_type
schema_version
occurred_at
published_at
correlation_id
causation_id
producer_version
payload
```

## Dataset identity
```text
dataset_id
revision
source
schema_version
ingestion_run
normalization_version
effective_from
effective_to
availability_policy
checksum
```

## Agent action
```text
actor_id
capability
intent
scope
policy_decision
tool
input_hash
action_at
evidence_refs
verification
rollback_ref
```

این قراردادها باید به schema اجرایی تبدیل شوند. وجود این markdown به تنهایی evidence implementation نیست.
