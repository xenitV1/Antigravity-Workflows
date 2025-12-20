---
description: Python kütüphanelerindeki (dependencies) güvenlik açıklarını (CVE) ve eski versiyonları tarar.
---

Act as a Supply Chain Security Expert.
1. **Tooling:** Use `uvx pip-audit` to scan the current environment or `requirements.txt` file ephemeral. Do NOT install the tool permanently.
2. **Execute:** Run the command `uvx pip-audit`.
3. **Analyze:** Look for vulnerabilities (CVEs) in the output.
4. **Report:** If vulnerabilities are found, summarize them in Turkish (Package Name, Severity, Fix Version).
5. **Advise:** Suggest the command to upgrade the vulnerable packages (e.g., `uv pip install package@new-version`).