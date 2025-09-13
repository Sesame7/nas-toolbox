# 🛠️ NAS Toolbox – Maintenance Checklist

This checklist helps maintain and expand the repository in a consistent way.

---

## 1. Adding a New Tool

- Create a new subdirectory under the root (e.g., `camera-calibration/`).
- Inside the directory:
  - Add a `README.md` with **step-by-step usage instructions**.
  - Add a `scripts/` or `examples/` folder if code or screenshots are needed.
- Update the top-level `README.md`:
  - Add a link to the new subdirectory under **Contents**.
  - Keep descriptions short (1–2 lines).

---

## 2. Updating Documentation

- When fixing or improving instructions:
  - Keep the **history** in Git (no need for inline changelogs).
  - Use meaningful commit messages, e.g.,  
    ```
    docs(net-monitor): clarify interface selection step
    ```
- If the change is significant (new tool, major rewrite), tag a new release (e.g., `v0.2.0`).

---

## 3. Keeping Things Consistent

- **Structure**: Every tool has its own folder + `README.md`.  
- **Style**: Use the same Markdown style:
  - Headings (`## 📖 Section`)
  - Lists (`-` for bullets, `1.` for ordered steps)
  - Code blocks with language tags (e.g., \`\`\`bash).
- **Scope**: Keep this repo focused on **NAS operations & maintenance**.  
  Don’t mix in unrelated tools.

---

## 4. Contribution Guidelines

- When someone adds content:
  - Ensure **clear instructions** (assume reader has basic Docker/Linux skills).  
  - Add **troubleshooting** if applicable.  
  - Provide **examples** (commands, screenshots, configs).  
- Keep PRs or commits small and scoped to one tool.

---

## 5. Long-Term Ideas

- Add a **`docs/`** folder for general troubleshooting, FAQs, or references.  
- Consider a **Quick Start page** at the top-level README for non-technical users.  
- If repo grows big, split into categories (e.g., `network/`, `storage/`, `monitoring/`).

---
