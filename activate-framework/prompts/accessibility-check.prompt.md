---
description: 'Run an accessibility check on the current file or selection against WCAG 2.1 AA standards.'
agent: 'agent'
---

# Accessibility Check

Evaluate the provided code for accessibility compliance against WCAG 2.1 AA standards. Focus on issues that affect users of assistive technologies.

## Check Categories

### Semantic HTML & Structure

- Proper heading hierarchy (`h1` → `h2` → `h3`, no skipped levels)
- Meaningful landmark regions (`nav`, `main`, `aside`, `footer`)
- Lists used for list content, tables used for tabular data
- Correct use of `<button>` vs `<a>` based on behavior

### Interactive Elements

- All interactive elements are keyboard accessible
- Focus order follows a logical reading sequence
- Focus indicators are visible and meet contrast requirements
- Custom components have appropriate ARIA roles and states

### Images & Media

- All images have meaningful `alt` text (or `alt=""` for decorative images)
- Complex images have extended descriptions
- Videos have captions and audio descriptions where needed

### Forms

- All form inputs have associated `<label>` elements
- Required fields are indicated programmatically (not just visually)
- Error messages are linked to their fields and announced to screen readers
- Form validation messages are accessible

### Color & Contrast

- Text meets minimum contrast requirements (4.5:1 normal text, 3:1 large text)
- Information is not conveyed by color alone
- UI components and graphical objects meet 3:1 contrast ratio

### Dynamic Content

- Status messages use appropriate ARIA live regions
- Content changes are announced to screen readers
- Loading states are communicated accessibly
- Modal dialogs trap focus correctly

## Output Format

For each finding:

1. **Severity**: Critical / Major / Minor
2. **WCAG Criterion**: The specific success criterion (e.g., 1.1.1 Non-text Content)
3. **Location**: File and line or component
4. **Issue**: What the problem is
5. **Impact**: Who is affected and how
6. **Fix**: Specific remediation with code example

Summarize with a count of findings by severity and the overall compliance posture.

Review: ${selection}
