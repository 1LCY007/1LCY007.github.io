# Hide Publications During Double-Blind Review

## Goal

Prevent the public homepage and linked CV from exposing the publication list while a conference double-blind review is in progress.

## Scope

- Remove the `Publications` item from the homepage primary navigation.
- Remove the homepage `#publications` section and its publication entries.
- Remove the publications input from `Curriculum Vitae/cv-llt.tex`, so regenerated CV PDFs do not include the publication index.
- Keep the CV available, but move its homepage link out of the prominent hero action group to a less prominent location near the contact area.
- Do not modify the CV's other sections, the CV source bibliography, or unrelated navigation pages.

## Design

`index.html` remains the only homepage presentation file. Its navigation will omit the publication anchor, and the existing publications section will be deleted rather than hidden so the content is not left in the homepage source. The hero action group will retain Email, GitHub, and Research; the CV link will be placed in the Contact section or immediately adjacent to it using the existing link/button styling.

`Curriculum Vitae/cv-llt.tex` will stop including `publications.tex`. The source bibliography and publication files remain untouched so the publication list can be restored after the review period without reconstructing content.

## Verification

- Search tracked HTML and CV source files to confirm the homepage has no `Publications` navigation or section and the CV source no longer inputs `publications`.
- Confirm the CV link still exists exactly once on the homepage and points to `ChunyangLuo_CV.pdf`.
- Run a local HTML sanity check by inspecting the changed regions; if a LaTeX toolchain is available, rebuild the CV and confirm the generated PDF no longer contains a publications heading or entries.
