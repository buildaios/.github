## Summary

<!-- Provide a clear, concise summary of the proposed changes. Include the system or component being impacted (e.g., mcp-gateway, runtime-agent, or docs). -->

## Related Issue

<!-- Link the active GitHub tracking issue this pull request addresses. -->
Closes #

## Type of Change

Please tick the box that applies:

- [ ] `fix` (non-breaking bug fix addressing a system or engine fault)
- [ ] `feat` (non-breaking feature adding a new capability)
- [ ] `refactor` (code restructuring with zero functional or interface changes)
- [ ] `test` (adding or improving test suites)
- [ ] `docs` (technical documentation or architecture references)
- [ ] `chore` (updating environment packaging, dependencies, or tools)

---

## Testing

<!-- Describe how these changes were tested. Detail custom pytest modules, chaos injection parameters, or browser validation steps. -->

### Test Checklist
- [ ] Local unit tests pass cleanly: `pytest`
- [ ] Isolation verified: Flock, file constraints, or database locks are maintained
- [ ] Rollback safety: The `compensate()` routine completes successfully on failures (if applicable)

---

## Documentation

- [ ] Technical documentation updated (if modifying components described in structural files)
- [ ] Layout formatting rules followed (ParagraphStyle fontSize matched with `leading = fontSize * 1.25`)
- [ ] Non-markdown fallback platforms verified for text-rendering targets (if applicable)

---

## Checklist

- [ ] My code follows the code style and formatting standards of this project
- [ ] I have performed a self-review of the code changes before submitting
- [ ] My commits conform to the Conventional Commits specification
- [ ] No temporary debug spheres, mock lines, or unverified endpoints remain in production files
- [ ] I have verified that my changes do not introduce new warnings or compilation errors

---

## Reviewer Notes

<!-- Use this section to provide review guidance, coordinate system-level parameters, or draw attention to specific aspects of the implementation. -->
