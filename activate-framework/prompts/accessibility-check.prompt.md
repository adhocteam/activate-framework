---
description: "Evaluate the selected code for accessibility compliance using WCAG 2.2 AA. User may choose strict audit mode or developer coaching mode."
agent: "agent"
---

# Accessibility Check — Hybrid (Audit + Optional Coaching)

Analyze the provided code or snippet for accessibility compliance against **WCAG 2.2 AA**, using an **artifact‑driven review** approach.

The user may choose:
- **Strict Mode** → Only identify issues with severity, WCAG mapping, and fixes  
- **Coaching Mode** → Include explanations, rationale, and best‑practice guidance  

If the user does not specify, default to **Strict Mode**.

---

## Check Categories

### 1. Semantic Structure & Name/Role/Value
- Proper heading hierarchy  
- Meaningful landmark regions  
- Lists/tables used appropriately  
- Correct use of `<button>` vs `<a>`  
- Accurate accessible name/role/value  
- ARIA used only when necessary  
- **Custom components expose correct semantics**  

### 2. Keyboard & Focus
- Keyboard operability  
- No traps  
- Logical focus order  
- Visible focus indicators  
- Custom widgets follow expected keyboard patterns  
- **Custom components support tab, enter, space, arrow keys as appropriate**  

### 3. Images, Media & Non‑Text Content
- Meaningful alt text  
- Extended descriptions when needed  
- Accessible icon labeling  
- Captions and alternatives  
- Autoplay controls  

### 4. Forms & Validation
- Programmatic labels  
- Required indicators  
- Accessible error messages  
- Validation announcements  
- Clear instructions  

### 5. Color, Contrast & Visual Presentation
- Text contrast  
- UI component contrast  
- No color‑only communication  
- Text resize support  
- Reflow at 320px  

### 6. Dynamic Content, ARIA & Live Regions
- Appropriate live regions  
- Announced updates  
- Accessible loading states  
- Modal focus trapping  
- Avoid ARIA misuse  

### 7. Pointer, Motion & Interaction Safety
- Adequate pointer targets  
- No complex gestures  
- Motion alternatives  
- Accessible hover/focus content  

---

## Severity Rubric

Use this rubric consistently:

- **Critical**: Blocks completion of a core task for assistive technology users or creates severe legal/compliance risk.  
- **Major**: Creates a substantial barrier, but users may have a workaround.  
- **Minor**: Reduces accessibility quality or clarity with limited functional impact.  

---

## Output Format (Strict Mode)

For **each issue**, output:

1. **Severity**: Critical / Major / Minor  
2. **WCAG Criterion**  
3. **Location**  
4. **Issue**  
5. **Impact**  
6. **Evidence** (exact element/attribute/state observed)  
7. **Fix** (with code example)  

---

## Output Format (Coaching Mode)

Include all strict‑mode fields **plus**:

8. **Developer Coaching**  
   - Why this matters  
   - How assistive tech interprets it  
   - Best practices  
   - Tips to avoid similar issues  

---

## No-Findings Contract

If no issues are found, output exactly:

No accessibility issues found in the provided snippet based on available evidence.

Then include residual risks that could not be verified from the snippet alone.

---

## Example (Strict Mode)

```
Severity: Critical
WCAG Criterion: 4.1.2 Name, Role, Value
Location: <button class="icon-button"><svg>...</svg></button> in component FooterActions
Issue: Icon-only button lacks an accessible name.
Impact: Screen reader users cannot identify the purpose of the control.
Evidence: The control is icon-only and has no visible text or accessible name in markup.
Fix:
Add an accessible name and hide decorative icon markup from assistive tech.

<button class="icon-button" type="button" aria-label="Save changes">
  <svg aria-hidden="true" focusable="false">...</svg>
</button>
```

---

## Example (Coaching Mode)

```
Severity: Major
WCAG Criterion: 4.1.3 Status Messages
Location: <div class="alert">Your session is about to expire</div> in ProfilePage
Issue: Visual warning is not exposed as a programmatic status message.
Impact: Screen reader users may not be notified when the warning appears.
Evidence: The warning is presented visually, but status semantics are not reliably declared for announcement.
Fix:
Use an appropriate live region role and provide clear message text.

<div class="alert alert-warning" role="status" aria-live="polite">
  <h2 class="h4">Session timeout warning</h2>
  Your session will expire in 2 minutes.
</div>

Developer Coaching:
Status messages must be announced when they appear without forcing focus changes. Assistive technologies monitor live regions like role="status" and announce updates automatically. Use role="alert" only for urgent, interruptive content; for non-critical warnings, role="status" with clear text is usually the better choice.
```

---

## Summary Requirements

At the end of the report, include:

- **Count of findings by severity**  
- **Overall compliance posture**  
- **Top risks**  
- **(If coaching mode)** Developer learning opportunities  
- **Assumptions and limitations** (what could not be validated from static snippet review)  

---

## References

Use the following authoritative sources when providing explanations, rationale, or coaching:


- **Web Content Accessibility Guidelines (WCAG) 2.2**  
  https://www.w3.org/TR/WCAG22/

- **Understanding WCAG 2.2 (W3C)**
  https://www.w3.org/WAI/WCAG22/Understanding/

- **W3C ARIA Authoring Practices Guide (APG)**  
  https://www.w3.org/WAI/ARIA/apg/

- **Mozilla Developer Network (MDN) – Accessibility Documentation**  
  https://developer.mozilla.org/en-US/docs/Web/Accessibility

- **VA's Accessibility Testing Manual** (Comprehensive testing guidance) 
  https://depo-platform-documentation.scrollhelp.site/collaboration-cycle/accessibility-testing-manual

- **Techniques for WCAG 2.2 (W3C)**
  https://www.w3.org/WAI/WCAG22/Techniques/

- **ARIA in HTML (W3C)**
  https://www.w3.org/TR/html-aria/

- **Accessible Name and Description Computation 1.2**
  https://www.w3.org/TR/accname-1.2/

- **HTML Accessibility API Mappings (HTML-AAM)**
  https://www.w3.org/TR/html-aam-1.0/

- **Section 508 ICT Testing Baseline (Trusted Tester)**
  https://ictbaseline.access-board.gov/

- **USWDS Accessibility Guidance**
  https://designsystem.digital.gov/accessibility/
---

## Review Target
${selection}
