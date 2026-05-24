# Stressor Analysis Template

**System:** [System Name]  
**Date:** YYYY-MM-DD  
**Iteration:** [Number]  
**Analyst:** [Name/Team]

## Architecture Components

List the major components of your system:

1. [Component 1]
2. [Component 2]
3. [Component 3]
4. [Component 4]
5. [Component 5]
...

## Stressor List

Generate 20-50 diverse stressors. Include at least one absurd stressor!

### Business Stressors
- [ ] [Business change/pressure]
- [ ] [Market shift]
- [ ] [Customer behavior change]

### Technical Stressors
- [ ] [System failure]
- [ ] [Performance issue]
- [ ] [Integration break]

### Natural/Physical Stressors
- [ ] [Natural disaster]
- [ ] [Infrastructure failure]

### Regulatory/Legal Stressors
- [ ] [Regulation change]
- [ ] [Compliance requirement]

### Social/Economic Stressors
- [ ] [Economic shift]
- [ ] [Social movement]

### Absurd Stressors 🐉
- [ ] Fire breathing Lizards (the worst kind)
- [ ] [Your absurd stressor here]

## Impact Matrix

For each stressor, mark which components are affected (1 = affected, 0 = not affected)

| # | Stressor | Comp 1 | Comp 2 | Comp 3 | Comp 4 | Comp 5 | TOTAL |
|---|----------|--------|--------|--------|--------|--------|-------|
| 1 | [Stressor name] | 0 | 1 | 1 | 0 | 1 | 3 |
| 2 | [Stressor name] | 1 | 1 | 0 | 1 | 0 | 3 |
| 3 | [Stressor name] | 1 | 0 | 1 | 1 | 1 | 4 |
| ... | ... | ... | ... | ... | ... | ... | ... |
| **TOTAL** | **Component Vulnerability** | **X** | **Y** | **Z** | **A** | **B** | **TOTAL** |

## Vulnerability Analysis

### Most Vulnerable Components
(Components affected by the most stressors)

1. **[Component Name]** - Affected by X stressors
   - Why vulnerable: [Analysis]
   - Stressors affecting it: [List]

2. **[Component Name]** - Affected by Y stressors
   - Why vulnerable: [Analysis]
   - Stressors affecting it: [List]

### Highest Impact Stressors
(Stressors that affect the most components)

1. **[Stressor Name]** - Affects X components
   - Components impacted: [List]
   - Cascade effects: [Analysis]

2. **[Stressor Name]** - Affects Y components
   - Components impacted: [List]
   - Cascade effects: [Analysis]

## Detailed Stressor Analysis

For key stressors, document:

### Stressor #[N]: [Name]

**Business Impact:** [What happens if this occurs]  
**Detection:** [How we'd detect this]  
**Business Reaction:** [How business would respond]  
**Residue (Architectural Change):** [What persists after responding]  
**Components Affected:** [List with reasoning]

## Recommended Residues

Based on vulnerability analysis, prioritized architectural improvements:

### Priority 1: [High-Leverage Residue]
- **Target Component:** [Component]
- **Protects Against:** [List of stressors this residue neutralizes]
- **Impact Reduction:** [Number of stressors neutralized]
- **Implementation:** [Brief description]
- **Effort:** [High/Medium/Low]

### Priority 2: [High-Leverage Residue]
- **Target Component:** [Component]
- **Protects Against:** [List of stressors]
- **Impact Reduction:** [Number]
- **Implementation:** [Description]
- **Effort:** [H/M/L]

### Priority 3: [High-Leverage Residue]
- **Target Component:** [Component]
- **Protects Against:** [List of stressors]
- **Impact Reduction:** [Number]
- **Implementation:** [Description]
- **Effort:** [H/M/L]

## Iteration Results

### Before This Iteration
- Total stressor count: [N]
- Total impact score: [Sum of all stressor impacts]
- Most vulnerable component: [Name] (affected by X stressors)
- Average component vulnerability: [Total impacts / components]

### After This Iteration
(Re-analyze after implementing residues)
- Total stressor count: [N]
- Total impact score: [New sum]
- Most vulnerable component: [Name] (affected by Y stressors)
- Average component vulnerability: [New average]

### Improvement
- **Impact reduction:** [%] (from X to Y)
- **Stressors neutralized:** [Number]
- **Most improved component:** [Name]

## Patterns Observed

### Common Failure Modes
- [Pattern 1]
- [Pattern 2]
- [Pattern 3]

### Cascade Effects
- [Component A failure] → [Component B affected] → [Component C affected]

### Resilience Gaps
- [Gap 1]
- [Gap 2]
- [Gap 3]

## Learning Notes

### Surprising Vulnerabilities
- [What surprised you about vulnerabilities discovered]

### High-Leverage Insights
- [Residues that protect against many stressors]

### Absurd Stressors That Revealed Real Issues
- [How ridiculous scenarios showed actual architectural gaps]

### Next Iteration Focus
- [Where to focus next round]

## Action Items

- [ ] Implement residue: [Description]
- [ ] Implement residue: [Description]
- [ ] Re-run stressor analysis after changes
- [ ] Update architecture documentation
- [ ] Create ADRs for major residues
- [ ] Schedule next iteration

## Related Documentation

- **ADRs:** [Links to ADRs documenting residues]
- **Architecture Docs:** [Links to updated architecture docs]
- **Previous Iterations:** [Links to prior stressor analyses]

---

## Notes on Usage

**Stressor Generation Tips:**
- Aim for 20-50 stressors for comprehensive analysis
- Mix realistic and absurd (absurd ones reveal unknown unknowns)
- Think across time scales (immediate, 6 months, 2 years)
- Consider different failure modes (slow, fast, partial, complete)
- Don't self-censor - write down even "silly" stressors

**Impact Mapping Tips:**
- Be honest about impacts (don't minimize for comfort)
- Consider cascade effects (one component failing affects others)
- Think about direct AND indirect impacts
- Mark 1 even if impact is "could possibly affect"

**Residue Identification Tips:**
- Look for patterns in vulnerabilities
- Prioritize residues that protect against MANY stressors
- Consider implementation effort vs impact reduction
- Think about architectural patterns (caching, redundancy, decoupling)
- Document WHY each residue protects against listed stressors

**Iteration Tips:**
- Don't try to fix everything at once
- Implement 2-3 high-leverage residues per iteration
- Re-analyze completely after changes
- Celebrate vulnerability reduction
- Keep iterating until marginal improvements diminish

---

**Remember: Fire breathing Lizards are not a joke. They represent the unknown unknowns your system must handle.** 🐉
