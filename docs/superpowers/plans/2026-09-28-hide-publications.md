# Hide Publications During Double-Blind Review Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Remove public publication listings from the homepage and generated CV while keeping the CV link available in a less prominent footer location.

**Architecture:** Keep the existing single-file homepage structure and CV LaTeX source. Remove publication markup from `index.html`, relocate the existing CV link into the footer, remove the publication input from the CV source, and rebuild the checked-in PDF from that source.

**Tech Stack:** Static HTML/CSS, LaTeX via `latexmk`, PDF text inspection via `pdftotext`, Git.

---

### Task 1: Remove the homepage publication exposure and reduce CV prominence

**Files:**
- Modify: `index.html:764-768` (primary navigation)
- Modify: `index.html:804-809` (hero action links)
- Modify: `index.html:847-866` (publication section)
- Modify: `index.html:1225-1229` (footer links)

- [ ] **Step 1: Remove the primary navigation publication link**

Delete this line from the `nav-links` element:

```html
<a href="#publications">Publications</a>
```

- [ ] **Step 2: Remove the prominent hero CV link**

Delete this line from the hero `.actions` element:

```html
<a class="button" href="ChunyangLuo_CV.pdf" target="_blank" rel="noopener">CV</a>
```

- [ ] **Step 3: Delete the complete homepage publications section**

Delete the section beginning with `<section id="publications"` and ending after its closing `</section>`, including the MemoSync title, author list, submission status, and project link.

- [ ] **Step 4: Add the CV link to the footer**

Change the footer inner content to:

```html
<footer>
    <div class="shell footer-inner">
        <span>&copy; 2026 Chunyang Luo</span>
        <span><a href="ChunyangLuo_CV.pdf" target="_blank" rel="noopener">CV</a></span>
        <span><a href="#top">Back to top</a></span>
    </div>
</footer>
```

- [ ] **Step 5: Search the homepage for forbidden publication exposure**

Run:

```powershell
rg -n -i 'id="publications"|href="#publications"|>Publications<|Baiqiao Zhang.*Chunyang Luo|Submitted to ACM CHI' index.html
```

Expected: no output.

- [ ] **Step 6: Verify the homepage still has one CV link**

Run:

```powershell
rg -n "ChunyangLuo_CV\.pdf" index.html
```

Expected: exactly one result, in the footer.

### Task 2: Remove publications from the CV source and rebuild the public PDF

**Files:**
- Modify: `Curriculum Vitae/cv-llt.tex:103-105`
- Regenerate: `ChunyangLuo_CV.pdf`

- [ ] **Step 1: Remove the publication input from the CV source**

Delete the explanatory comments and `\input{publications}` so the document proceeds from `\makerubric{education}` directly to `\input{skills}`. Leave `Curriculum Vitae/publications.tex` and `Curriculum Vitae/own-bib.bib` unchanged for later restoration.

- [ ] **Step 2: Rebuild the CV PDF from its source directory**

Run:

```powershell
latexmk -pdf -interaction=nonstopmode -halt-on-error cv-llt.tex
```

Working directory: `Curriculum Vitae`.

Expected: exit code 0 and an updated `Curriculum Vitae/cv-llt.pdf`.

- [ ] **Step 3: Copy the rebuilt PDF to the public homepage path**

Run:

```powershell
Copy-Item -LiteralPath 'Curriculum Vitae\cv-llt.pdf' -Destination 'ChunyangLuo_CV.pdf' -Force
```

Expected: `ChunyangLuo_CV.pdf` is updated and remains the file referenced by the homepage footer.

- [ ] **Step 4: Verify the generated PDF has no publication list**

Run:

```powershell
pdftotext 'ChunyangLuo_CV.pdf' - | Select-String -Pattern 'Publications|MemoSync|Submitted to ACM CHI'
```

Expected: no matching output.

### Task 3: Final consistency checks

**Files:**
- Verify: `index.html`
- Verify: `Curriculum Vitae/cv-llt.tex`
- Verify: `ChunyangLuo_CV.pdf`

- [ ] **Step 1: Confirm the source and homepage contain no publication index references**

Run:

```powershell
rg -n -i 'id="publications"|href="#publications"|>Publications<|Baiqiao Zhang.*Chunyang Luo|Submitted to ACM CHI' index.html 'Curriculum Vitae\cv-llt.tex'
```

Expected: no output.

- [ ] **Step 2: Confirm only intended files changed**

Run:

```powershell
git status --short
```

Expected: changes are limited to `index.html`, `Curriculum Vitae/cv-llt.tex`, `ChunyangLuo_CV.pdf`, and the workflow documentation files already created.

- [ ] **Step 3: Inspect the final diff**

Run:

```powershell
git diff --check
git diff -- index.html 'Curriculum Vitae/cv-llt.tex'
```

Expected: no whitespace errors; the diff removes publication exposure, moves the CV link to the footer, and does not modify unrelated CV content.
