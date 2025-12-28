---
description: Documentation generation workflow for code, APIs, and projects
---

# Docs Workflow

## Description
Use this workflow when creating or updating documentation. It covers code documentation (JSDoc/TSDoc), API references, user guides, README files, and changelogs.

---

## Steps

1. **Analyze the documentation task** - Determine if the user needs code documentation (JSDoc/TSDoc comments), API reference documentation, user guides/tutorials, README files, or changelog documentation.

2. **Load documentation rule** - Activate the @documentation rule to apply documentation standards and best practices.

3. **Perform relevant documentation based on task type**:
   - **For code documentation**: Add JSDoc/TSDoc comments to all public functions, classes, and modules including parameter descriptions, return types, examples, and error conditions.
   - **For API documentation**: Document all endpoints with HTTP methods, path parameters, query parameters, request bodies, response formats, error codes, and usage examples in multiple languages (cURL, JavaScript, Python).
   - **For user guides**: Create step-by-step tutorials with clear objectives, prerequisites, quick start section, detailed explanations, troubleshooting section, and FAQ.
   - **For README**: Include project title, description, features list, installation instructions, usage examples, development setup, API reference link, contributing guidelines, and support information.
   - **For changelog**: Follow Keep a Changelog format with sections for Added, Changed, Deprecated, Removed, Fixed, and Security, organized by version number and date.

4. **Apply documentation standards** - Use clear, concise language, provide working code examples, include diagrams for complex concepts, add table of contents for long documents, link related topics, include troubleshooting sections, and add version information and dates.

5. **Review documentation quality** - Verify completeness (all public APIs documented), clarity (technical jargon explained), accuracy (code examples tested), accessibility (searchable, linkable sections), and maintenance (up-to-date, deprecated items marked).

6. **Generate deliverable** - Provide documented code files, complete API reference, user guide with examples, project README, or version changelog based on the task.

7. **Recommend maintenance strategy** - Suggest documentation update schedule, version control practices, and review process for keeping documentation current.

---

## Related Workflows
- Call `/review` to review documentation before publishing
- Call `/implement` to document new features
