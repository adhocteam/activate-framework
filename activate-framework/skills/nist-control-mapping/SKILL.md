---
name: nist-control-mapping
description: Add traceable NIST SP 800-53 control annotations to source code, infrastructure-as-code, and other technical files, then roll them up into control and evidence documents. Use when mapping implementation artifacts to controls or preparing code-level evidence for an ATO package.
inputs:
  - name: scope
    description: Files, directories, changes, or system boundary to annotate or roll up
    required: true
  - name: control_baseline
    description: Applicable NIST SP 800-53 revision, impact baseline, tailoring, and agency overlays, if known
    required: false
  - name: output_artifacts
    description: Requested outputs, such as a control traceability matrix, OSCAL Component Definition, implementation statements, or evidence register
    required: false
outputs:
  - name: annotations
    description: Minimal source annotations or sidecar mappings with control references and implementation context
  - name: control_matrix
    description: Control-to-artifact mapping with coverage statements and evidence references
  - name: evidence_register
    description: Inventory of supporting implementation artifacts and validation evidence
  - name: limitations
    description: Unconfirmed applicability, missing evidence, and review required before ATO use
---

## Purpose

Create consistent, reviewable links between technical implementation and specific NIST SP 800-53 controls. Aggregate those links into traceability artifacts that can inform an SSP or other ATO documentation. Keep the workflow usable across programming languages, Terraform and other infrastructure-as-code, configuration files, and documentation.

## Inputs

- **Scope:** Files, directories, changes, or system boundary to annotate or roll up.
- **Control baseline:** Applicable NIST SP 800-53 revision, impact baseline, tailoring, and overlays, if known. The organization must supply these decisions.
- **Output artifacts:** Requested outputs, such as a traceability matrix, OSCAL Component Definition, implementation statements, or evidence register.

## Outputs

- **Annotations:** Inline source annotations or sidecar mappings with control references and implementation context.
- **Control matrix:** Control-to-artifact mappings with coverage statements and evidence references.
- **Evidence register:** Inventory of supporting implementation artifacts and validation status.
- **Limitations:** Unconfirmed applicability, missing evidence, and review required before ATO use.

## Preconditions

- The user identifies the system or artifact scope.
- Use the organization's specified NIST catalog revision, impact baseline, tailoring decisions, and overlays when available.
- If the control baseline or applicability is unknown, ask for it. You may produce a clearly labeled provisional inventory, but do not select a baseline or claim applicability on the organization's behalf.

## Annotation Format

Use the same field names in comments across file types. Adapt the comment prefix to the language (`#`, `//`, `/* */`, or the file format's supported comment syntax) and place the block immediately before the smallest meaningful code or configuration section. Keep the control citation canonical, including the catalog revision and enhancement notation.

```text
# compliance-control: NIST SP 800-53 Rev. 5 AC-6(1)
# compliance-coverage: partial
# compliance-rationale: The deployment role is limited to the actions required by this service.
# compliance-evidence: tests/security/test_deployment_role.py::test_role_has_scoped_actions
```

Repeat the `compliance-control` field in separate annotation blocks when one section relates to multiple controls. Use only these coverage values:

- `implemented`: This artifact supports the stated control implementation; this does not establish that the full control is satisfied.
- `partial`: This artifact supports only part of the control implementation.
- `planned`: The implementation is intended but is not present yet.
- `inherited`: The implementation is supplied by an identified common control provider or external service.
- `not-applicable`: Use only when an authorized assessor has determined this; include the rationale and source of that determination.

For formats without comments (for example, strict JSON), use a sidecar mapping file in the repository's established compliance/evidence location. Each record must include the file path and a stable section locator such as a symbol, resource address, or JSON Pointer; include line numbers only as supplemental navigation because they can change. Record the same fields as inline annotations.

In Terraform or other declarative infrastructure, prefer a local comment annotation unless the team explicitly wants control metadata embedded in deployable resource attributes or tags. Do not add provider-specific tags or alter deployment behavior just to make the mapping machine-readable.

## Procedure

1. **Confirm authority and scope.** Identify the system boundary, files or change set, authoritative NIST catalog revision, selected baseline, tailoring, overlays, and any organization-specific annotation convention. Distinguish NIST SP 800-53 controls from NIST AI RMF categories and other frameworks. If required inputs are unavailable, record the gap and keep mappings provisional.
2. **Inspect before editing.** Find existing annotations, sidecar inventories, control catalogs, SSP language, tests, and evidence references. Reuse established conventions. Determine which files support comments and avoid generated, vendored, or out-of-scope files unless requested.
3. **Select defensible mappings.** Map a code section only to a specific control or enhancement that it directly supports. Verify the control identifier and title against the selected catalog when available. Record a concise rationale and relevant evidence. Do not infer that a control is fully implemented from a resource tag, comment, test, or single code section.
4. **Annotate minimally.** Add the annotation block next to the relevant function, module, resource, policy, or configuration. For unsupported comment formats, add or update the sidecar record instead. Preserve behavior, formatting, and existing annotations; do not add speculative controls to make coverage appear broader.
5. **Build the roll-up.** Read annotations and sidecar records in the requested scope. Produce the requested control traceability matrix, implementation statements, and/or evidence register. Use `assets/control-traceability.template.csv` as a tool-neutral starting point. When OSCAL is requested, use `assets/oscal-component-definition.template.json` for reusable component-level implementation information. For each mapping, retain:
   - Control identifier, title, and catalog revision
   - Applicability or tailoring source, when supplied
   - Artifact path and stable section locator
   - Implementation rationale and coverage value
   - Evidence references and their validation status
   - Open questions, inherited-control provider, and assessor review needs
6. **Validate generated OSCAL.** The Component Definition model describes how a component may support controls; it is reusable input to an SSP, not a representation of the system's actual instantiated implementation. Keep system-specific control implementation, boundary, and inherited-control decisions in the organization's SSP process. Use control IDs exactly as defined by the selected OSCAL catalog or profile. Replace all template UUIDs with unique UUIDv4 values, update `last-modified` on each content change, and replace the example property namespace with a stable namespace owned by the organization. If available, use NIST's OSCAL CLI or the organization's approved OSCAL tooling to validate against the matching OSCAL model version and convert formats. Check the installed tool's help for current command syntax; do not treat JSON parsing alone as OSCAL schema validation.
7. **Check traceability.** Confirm every reported mapping points to an annotation or sidecar record, control identifiers match the supplied catalog, locators resolve, and evidence links are not represented as verified unless checked. Report unannotated scope separately; absence of an annotation is not evidence that a control is absent or unmet.
8. **Report limitations.** Summarize changed files, produced artifacts, unmapped or uncertain areas, missing evidence, and the reviews needed before the output is used in an authorization package.
9. **Preserve review state.** Leave implementation statements provisional until the system owner and control assessor validate applicability, evidence, and narrative. Never convert annotation presence or a successful schema check into a control-effectiveness or authorization claim.

## Roll-Up Guidance

Use the team's required document templates and terminology. If none are provided, the included CSV traceability template and a separate evidence register are suitable starting points for review. The OSCAL Component Definition template is for reusable component implementation information and can support, but cannot replace, the system-specific SSP. Generate an SSP, Assessment Results, or POA&M only when the organization supplies the required model-specific inputs and review process. A control implementation statement should describe only the implementation supported by the mapped artifacts and should distinguish system-specific mechanisms from inherited controls.

The roll-up can inform an SSP, control implementation matrix, or ATO evidence package; it is not a complete SSP, assessment result, authorization decision, or certification. Do not claim compliance, pass/fail, or control effectiveness based solely on annotations. A qualified system owner, control assessor, or authorizing organization must validate applicability, implementation, evidence sufficiency, and final language.

### Optional Tooling

- **NIST OSCAL CLI:** Use the official CLI to validate OSCAL model structure and convert supported OSCAL formats when it is available and approved. It is optional, is not bundled with this skill, and may require a supported Java runtime. Check the installed release's help and requirements before use.
- **OSCAL schemas:** When the CLI is unavailable, validate against the official schema matching the template's OSCAL version using an organization-approved JSON Schema, XML Schema, or YAML validation tool. Pin the schema version; do not validate against an unrelated `latest` schema and assume compatibility.
- **Repository-native checks:** Parse generated JSON/YAML/XML for syntax, then separately run OSCAL schema validation. Preserve validation output and tool/schema versions as evidence; a schema-valid document is not proof that its control claims are accurate.

Do not add a parser or dependency to the application repository solely to create a one-time roll-up. If teams repeat the process, define and test a repository-specific extractor against the agreed annotation/sidecar format before automating document generation.

## Completion Criteria

- [ ] Each added mapping has a canonical control citation, a specific locator, a rationale, and a coverage value.
- [ ] Unsupported file formats are represented in a sidecar mapping using stable locators.
- [ ] Requested roll-up artifacts preserve links back to implementation and evidence.
- [ ] OSCAL output uses the intended model, selected profile/catalog IDs, current UUIDs, and matching schema version.
- [ ] Unknown applicability, unverified evidence, and assessor review needs are explicit.
- [ ] No compliance or authorization claim is inferred from annotation presence.

## Graceful Degradation

When the catalog, baseline, tailoring, evidence, or parsing capability is unavailable, do not guess or silently omit the limitation. Produce only the supported inventory, label unresolved mappings as provisional, identify files or evidence that could not be checked, and request review from the responsible security or compliance authority.

## References

- NIST SP 800-53 Rev. 5, Security and Privacy Controls for Information Systems and Organizations: <https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final>
- NIST SP 800-53B, Control Baselines for Information Systems and Organizations: <https://csrc.nist.gov/pubs/sp/800/53/b/upd1/final>
- NIST OSCAL, machine-readable security and compliance data formats: <https://pages.nist.gov/OSCAL/>
- NIST OSCAL Component Definition model: <https://pages.nist.gov/OSCAL/learn/concepts/layer/implementation/component-definition/>
- NIST tutorial for creating a Component Definition: <https://pages.nist.gov/OSCAL/learn/tutorials/implementation/simple-component-definition/>
- NIST OSCAL CLI: <https://github.com/usnistgov/oscal-cli>
- NIST OSCAL validation concepts and schemas: <https://pages.nist.gov/OSCAL/learn/concepts/validation/>