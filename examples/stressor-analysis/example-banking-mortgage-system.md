# Example: Banking Mortgage System Stressor Analysis

**System:** Mortgage Comparison Platform  
**Date:** 2024-11-XX (from original analysis)  
**Iteration:** 1  
**Analyst:** Solution Architect Team

## System Overview

A banking platform that helps customers compare mortgage rates from multiple banks, evaluate offers, and make lending decisions.

## Architecture Components

1. **Customer Request** - Frontend/API entry point
2. **Cloud MQ** - Message queue for async processing
3. **Collect Customer Information** - Customer data gathering
4. **Collect Ledger Information** - Financial records integration
5. **Request Evaluation** - Credit/risk evaluation
6. **Request Energy Class** - Property energy rating
7. **Request External Offer** - Get offers from external banks
8. **External Offer Sanity Check** - Validate external offers
9. **Calculate Mortgage** - Core calculation engine
10. **Internal Offer Sanity Check** - Validate internal calculations
11. **Alternate Return Pipeline** - Fallback processing path

## Stressor List (Selected Examples)

### Business Stressors
1. Increased expectation of personal contact
2. External bank presents lower rates than us
3. Business analysts want to track customer churn
4. Voluntary rate decrease due to sustainability incentives

### Technical Stressors
5. Internal banking systems unavailable (Lizards!)
6. Traffic to our API for external banks increase 10-fold
7. Customer base triples
8. Calculation returns faulty high rates

### Natural/Physical Stressors
9. Earthquake
10. Fire breathing Lizards (the worst kind) 🐉

### Regulatory/Legal Stressors
11. Sustainability constraints on rates
12. Riksbanken requires higher security for loans
13. GDPR regulation changes

### Social/Economic Stressors
14. Housing market crashes
15. Higher unemployment

### Absurd Stressors
16. **Fire breathing Lizards** (the worst kind) 🐉
17. Competitors contact customers directly

## Impact Matrix (Partial)

| # | Stressor | Cust Req | MQ | Cust Info | Ledger | Eval | Energy | Ext Offer | Ext Check | Calc | Int Check | Alt Pipeline | TOTAL |
|---|----------|----------|-----|-----------|--------|------|--------|-----------|-----------|------|-----------|--------------|-------|
| 1 | Personal contact expectation | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | **1** |
| 3 | Sustainability constraints | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 1 | 0 | **3** |
| 4 | Outsourcing Ledger | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | **1** |
| 6 | Track customer churn | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | **1** |
| 7 | External banks lower rates | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | **2** |
| 8 | Systems unavailable (Lizards!) | 0 | 0 | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 0 | 0 | **5** |
| 9 | Sustainability infra constraints | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 1 | 0 | 0 | **7** |
| 10 | Sustainability rate decrease | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | 0 | **4** |
| 11 | Fake competitor offers | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | **2** |
| 12 | Faulty high rates | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | **1** |
| 14 | Customer base triples | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | **2** |
| 15 | Competitor direct contact | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | **1** |
| 17 | Higher security requirements | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | **2** |
| 18 | Evaluation provider bankrupt | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | **2** |
| 19 | Properties outside Sweden | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 0 | 1 | 1 | 0 | **5** |
| **TOTAL** | **Component Vulnerability** | **2** | **2** | **4** | **3** | **6** | **4** | **3** | **2** | **8** | **4** | **1** | **39** |

## Vulnerability Analysis

### Most Vulnerable Components

1. **Calculate Mortgage** - Affected by **8 stressors**
   - Why vulnerable: Core business logic, central to all calculations
   - Stressors: Sustainability constraints, rate changes, security requirements, international properties, system unavailability, faulty calculations, external competition
   - **Critical component that needs resilience!**

2. **Request Evaluation** - Affected by **6 stressors**
   - Why vulnerable: Depends on external services, regulatory changes affect it
   - Stressors: System unavailability, sustainability changes, security requirements, provider bankruptcy, international properties

3. **Collect Customer Information** - Affected by **4 stressors**
   - Why vulnerable: Data quality and availability issues
   - Stressors: Churn tracking needs, system unavailability, sustainability infrastructure

4. **Request Energy Class, Internal Offer Sanity Check** - Each affected by **4 stressors**

### Highest Impact Stressors

1. **Sustainability constraints on infrastructure (#9)** - Affects **7 components**
   - Shows how a single regulatory/infrastructure change cascades widely
   - Components: MQ, Customer Info, Ledger, Evaluation, Energy, External Offer, Calculate

2. **Internal banking systems unavailable (Lizards!) (#8)** - Affects **5 components**
   - Classic availability issue cascades through dependent services
   - Components: Customer Info, Ledger, Evaluation, External Offer, Calculate

3. **Issue mortgages to properties outside Sweden (#19)** - Affects **5 components**
   - Business expansion creates widespread architectural impact
   - Components: Evaluation, Energy, External Offer, Calculate, Internal Check

## Detailed Stressor Analysis (Selected)

### Stressor #8: Internal Banking Systems Unavailable (Lizards!)

**Business Impact:** Cannot process mortgages, service degradation  
**Detection:** Monitoring alerts, user complaints, timeout errors  
**Business Reaction:** Require resilience in the app  
**Residue:** Near client cache (ODL - Offline Data Layer)  
**Components Affected:**
- Collect Customer Information (needs customer data)
- Collect Ledger Information (can't get financial records)
- Request Evaluation (evaluation service down)
- Request External Offer (can't query external banks)
- Calculate Mortgage (depends on all above)

**Why This Matters:** This reveals that FIVE components have single points of failure on upstream banking systems. A cache/fallback strategy would protect against many failure modes.

### Stressor #9: Sustainability Constraints on Infrastructure

**Business Impact:** Cost increase, potential service limits  
**Detection:** Cost monitoring, performance degradation  
**Business Reaction:** Shift in platform  
**Residue:** Platform modernization, green computing  
**Components Affected:** Nearly everything (7 components!)

**Why This Matters:** Shows how infrastructure changes cascade. Addressing this creates platform resilience that helps with MANY other stressors (scale, cost, availability).

### Stressor #16: Fire Breathing Lizards 🐉

**Business Impact:** Unknown, unpredictable chaos  
**Detection:** Visual inspection, smoke alarms, screaming  
**Business Reaction:** ???  
**Residue:** Disaster recovery, geographic redundancy, chaos engineering culture  
**Components Affected:** Potentially ALL

**Why This Matters:** This absurd stressor forces you to think about:
- What if EVERYTHING fails at once?
- Do we have geographic redundancy?
- Can we fail over to another region?
- Is our DR plan actually tested?
- Do we have a plan for the truly unexpected?

The lizards teach us about **unknown unknowns** - if you can't conceptually handle lizards, you can't handle zero-days, black swans, or novel attack vectors.

## Recommended Residues

### Priority 1: Near-Client Cache / Offline Data Layer
**Target Component:** Calculate Mortgage, Request Evaluation, Collect Ledger  
**Protects Against:** 
- System unavailability (#8)
- External bank not responding
- Evaluation provider issues (#18)
- High latency under load
- Network failures

**Impact Reduction:** 5+ stressors neutralized  
**Implementation:** Implement caching layer with TTL, stale-while-revalidate pattern  
**Effort:** Medium  
**Why High-Leverage:** One cache protects against entire class of "upstream unavailable" failures

### Priority 2: Analytics Integration
**Target Component:** Collect Customer Information, External Offer Sanity Check  
**Protects Against:**
- Track customer churn (#6)
- External banks lower rates (#7)
- Fake competitor offers (#11)
- Faulty calculation detection (#12)

**Impact Reduction:** 4 stressors neutralized  
**Implementation:** Add analytics/monitoring layer, anomaly detection  
**Effort:** Medium  
**Why High-Leverage:** Analytics help detect AND respond to multiple business/technical issues

### Priority 3: Circuit Breakers + Graceful Degradation
**Target Component:** All external integrations  
**Protects Against:**
- External service failures
- Cascade failures
- Traffic spikes (#13, #14)
- Partner unavailability
- Timeout issues

**Impact Reduction:** 6+ stressors neutralized  
**Implementation:** Add circuit breaker pattern, fallback responses, partial service modes  
**Effort:** High (cross-cutting)  
**Why High-Leverage:** Prevents cascade failures, enables "limping mode" operation

### Priority 4: Geographic Redundancy / Multi-Region
**Target Component:** Entire system  
**Protects Against:**
- Earthquake (#2)
- Fire breathing Lizards (#16)
- National lights out (#46)
- Ransomware attack (#47)
- Data center failures

**Impact Reduction:** 8+ stressors neutralized  
**Implementation:** Deploy to multiple regions, active-active or active-passive  
**Effort:** Very High  
**Why High-Leverage:** Ultimate resilience for disaster scenarios

## Iteration Results

### Before This Iteration (Baseline)
- Total stressor count: 19 analyzed (64 total in list)
- Total impact score: 39 (from analyzed stressors)
- Most vulnerable component: Calculate Mortgage (8 stressors)
- Average component vulnerability: 3.5 stressors per component

### After Iteration 1 (Projected)
If we implement Priorities 1-3:
- Estimated stressors neutralized: 15+
- Projected impact score: ~20 (48% reduction!)
- Most vulnerable component: Would shift to different component
- Average vulnerability: ~1.8 per component

### Improvement (Projected)
- **Impact reduction:** ~48%
- **Stressors neutralized:** 15+ 
- **Most improved component:** Calculate Mortgage (8 → 3 stressors)

## Patterns Observed

### Common Failure Modes
1. **Upstream service unavailability** - Affects 5+ components
2. **Regulatory/compliance changes** - Cascade through business logic
3. **Scale/load issues** - Hit infrastructure and entry points
4. **Data quality/validation** - Affect calculation accuracy

### Cascade Effects
- System unavailability → Can't collect data → Can't evaluate → Can't calculate
- External competition → Rate pressure → Need analytics → Need flexibility
- Sustainability → Infrastructure → Multiple services → Business logic

### Resilience Gaps
1. **No caching strategy** - Every upstream failure causes service degradation
2. **No circuit breakers** - Failures cascade through system
3. **Limited monitoring/analytics** - Can't detect issues or anomalies
4. **Single region** - Geographic disasters take down entire service
5. **Tight coupling** - Changes propagate widely

## Learning Notes

### Surprising Vulnerabilities
- **Calculate Mortgage hit by 8 stressors** - Expected it to be more isolated
- **Sustainability impacts 7 components** - Regulatory changes cascade widely
- **Lizards reveal DR gaps** - We're not prepared for regional disasters

### High-Leverage Insights
- **Caching neutralizes entire failure class** - One change protects against many stressors
- **Circuit breakers prevent cascades** - Isolation is key to resilience
- **Analytics enable response** - Detecting issues is half the battle

### Absurd Stressors That Revealed Real Issues
- **Fire breathing Lizards** forced us to think about true disaster recovery
  - Revealed: We have NO geographic redundancy
  - Revealed: Our DR plan is untested
  - Revealed: We assume "everything works" in our region

- **Lizards made us realize:** If we can't survive lizards, we can't survive:
  - Ransomware locking entire datacenter
  - Regional power grid failure
  - Physical security breach
  - Novel attack vector we've never imagined

### Next Iteration Focus
1. Implement near-client cache (Priority 1)
2. Add basic circuit breakers to external calls
3. Re-run analysis to validate improvement
4. Consider geographic redundancy for Iteration 2

## Action Items

- [x] Complete initial stressor analysis
- [ ] Implement near-client cache / ODL
- [ ] Add analytics integration for sanity checks
- [ ] Implement circuit breaker pattern for external calls
- [ ] Re-run stressor analysis after changes (Iteration 2)
- [ ] Create ADR: Add caching layer for resilience
- [ ] Create ADR: Implement circuit breaker pattern
- [ ] Update architecture docs with resilience patterns
- [ ] Schedule chaos engineering exercise (test lizard-readiness 🐉)

## Related Documentation

- **ADRs:**
  - ADR-XXX: Add Near-Client Cache for Resilience (to be created)
  - ADR-XXX: Implement Circuit Breaker Pattern (to be created)
  
- **Architecture Docs:**
  - HLD to be updated with caching layer
  - Deployment guide to include DR procedures

- **Future Iterations:**
  - Iteration 2: After cache + circuit breakers
  - Iteration 3: After analytics integration

---

## Key Takeaways

1. **Calculate Mortgage is our most vulnerable component** - Needs immediate resilience work
2. **Sustainability regulations have wide impact** - Infrastructure changes cascade
3. **Fire breathing Lizards taught us** we're not ready for true disasters
4. **High-leverage changes:** Cache, circuit breakers, analytics
5. **Estimated 48% vulnerability reduction** from first 3 priorities

**Next Step:** Implement Priority 1 (caching) and re-analyze!

---

**Remember: This is iteration 1. Each iteration makes the system MORE resilient. Keep going until you can laugh at the lizards!** 🐉
