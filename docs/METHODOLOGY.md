# Audit Methodology

## Framework Overview

My audit approach combines traditional internal audit standards with modern data analytics, enabling continuous control assurance at scale. Rather than periodic manual sampling, I build systems that test controls in real time and generate findings automatically.

---

## The 7-Phase Cycle

### Phase 1: Scope Definition

Every audit engagement begins with clearly defining:
- **Risk areas** to be assessed (vendor performance, regulatory compliance, operational efficiency)
- **Control objectives** (what should be happening if controls are working)
- **Assessment criteria** (measurable thresholds that distinguish compliant from non-compliant)
- **Data sources** required for testing
- **Stakeholders** who own the controls being tested

**Key principle**: Scope must be specific enough to produce actionable findings, broad enough to capture systemic issues.

### Phase 2: Risk Assessment

Before testing controls, I assess inherent risk to prioritize effort:

| Risk Factor | Assessment Approach |
|-------------|-------------------|
| Financial impact | Historical cost data, penalty exposure |
| Frequency | How often the process executes (daily, weekly) |
| Complexity | Number of handoffs, jurisdictions, systems involved |
| History | Prior findings, repeat issues, known weaknesses |
| Regulatory exposure | Applicable regulations, compliance requirements |

**Output**: Risk-ranked list of controls to test, with effort allocated proportionally to risk.

### Phase 3: Control Testing

This is where data analytics transforms the audit. Instead of sampling 30 transactions manually, I build automated tests that validate every transaction:

**Manual approach** (traditional):
- Sample 30 vendor invoices
- Manually verify SLA compliance
- Extrapolate findings to population
- Result: statistical inference with uncertainty

**My approach** (data-driven):
- Build Python pipeline that processes ALL transactions
- Automated SLA calculation against contractual thresholds
- 100% population coverage with zero sampling error
- Real-time alerting when controls fail

```python
# Example: Control test logic (simplified)
def test_vendor_sla_compliance(vendor_data, sla_thresholds):
    """
    Tests whether vendor performance meets contractual SLAs.
    Returns findings for any breaches with severity classification.
    """
    findings = []
    for vendor in vendor_data:
        actual_performance = calculate_performance(vendor)
        threshold = sla_thresholds[vendor.category]
        
        if actual_performance < threshold:
            severity = classify_severity(threshold - actual_performance)
            findings.append({
                'vendor': vendor.name,
                'metric': actual_performance,
                'threshold': threshold,
                'gap': threshold - actual_performance,
                'severity': severity,
                'evidence': vendor.raw_data_reference
            })
    return findings
```

### Phase 4: Findings Documentation

Every finding follows a structured format:

| Element | Description |
|---------|-------------|
| **Finding ID** | Unique identifier for tracking |
| **Severity** | HIGH / MEDIUM / LOW (based on impact + likelihood) |
| **Condition** | What IS happening (factual, data-supported) |
| **Criteria** | What SHOULD be happening (standard, regulation, policy) |
| **Cause** | WHY the gap exists (root cause, not symptom) |
| **Effect** | What IMPACT this has (financial, operational, compliance) |
| **Evidence** | Data supporting the finding (specific, verifiable) |
| **Recommendation** | Proposed corrective action |

**Key principle**: Findings must be objective, evidence-based, and actionable. Never subjective opinions or unsubstantiated claims.

### Phase 5: Management Actions

For each finding, a management action is agreed:

- **Owner**: Who is responsible for remediation
- **Action**: Specific steps to address the finding
- **Deadline**: Target completion date
- **Success criteria**: How we verify the action was effective
- **Escalation path**: What happens if the deadline is missed

### Phase 6: Validation

After management actions are completed, I validate:
- Was the action actually implemented? (not just claimed)
- Does the control now pass the original test? (re-test)
- Is the fix sustainable? (not a one-time patch)

**Validation is non-negotiable.** A finding is not closed until the control demonstrably works.

### Phase 7: Continuous Monitoring

After validation, the control enters ongoing monitoring:
- Automated tests continue running (daily/hourly)
- Trend tracking identifies regression
- Threshold alerts trigger re-investigation if performance degrades
- Quarterly review of all active monitors for relevance

---

## Design Principles

### Correlation Over Thresholds

I avoid arbitrary percentage thresholds. Instead, I look for correlation:
- Did a control failure occur? (truck cancelled, SLA breached, deadline missed)
- Were business outcomes affected? (shipments delayed, costs incurred, compliance violated)
- Is there a causal link between the two?

If yes, that's a finding. If the control failed but nothing was affected, it's a risk observation (monitor, don't action).

### Data Completeness Checks

Before any control test executes, the system validates:
- Is source data fresh? (timestamp check)
- Is source data complete? (row count vs expected)
- Are all required fields populated? (null check)

If data quality fails, the audit pauses and raises a data integrity finding rather than testing on unreliable data.

### Structured Escalation

Not all findings are equal. Escalation follows severity:

| Severity | Response Time | Escalation To |
|----------|--------------|---------------|
| HIGH | Same day | Senior leadership + corrective action plan |
| MEDIUM | Within 1 week | Direct manager + action plan |
| LOW | Within 1 month | Process owner + improvement suggestion |

### Continuous Improvement Loop

```
Findings → Root Cause Analysis → System Improvement → Re-test → Monitor
    ↑                                                              |
    └──────────────────── Regression detected ─────────────────────┘
```

Every finding should make the system better. If the same finding recurs, it means the corrective action was insufficient, and a stronger intervention is needed.

---

## Tools & Techniques

| Technique | Application |
|-----------|-------------|
| Python automation | Building control tests that run continuously |
| SQL analysis | Querying large datasets for pattern detection |
| Statistical sampling | When 100% testing is not feasible (rare) |
| Root cause analysis (5-whys) | Understanding why controls failed |
| Process mapping | Identifying control points in workflows |
| Trend analysis | Detecting gradual degradation before it becomes critical |
| Benchmarking | Comparing performance across markets/vendors |
| Exception reporting | Flagging outliers for investigation |

---

## Regulatory Context

My audit work operates within regulated environments requiring:
- EU transport regulations (driving hours, rest periods, weekend bans)
- Multi-jurisdictional compliance (DE, UK, FR, ES, IT each have specific rules)
- Carrier certification standards
- SLA contractual obligations
- Data protection requirements (GDPR considerations in reporting)

This regulatory complexity means audits must consider not just "did the process work?" but "did it comply with applicable law in each jurisdiction?"
