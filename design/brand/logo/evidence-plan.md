# 1minHow Logo Evidence Plan v0.1

## Current decision

Keep the current `1minHow` logo unchanged for now. First freeze the current design, record its origin and public-use history, and connect it to the upcoming Blog typography and theme work.

This record is evidence of creation and use. It is not a substitute for trademark registration or legal clearance.

## Required files

```text
design/brand/logo/
  evidence-plan.md
  logo-record.md
  usage-rules.md
  CHANGELOG.md
  checksums.sha256
  assets/
    source/
    svg/
    png/
    webp/
    monochrome/
  screenshots/
    YYYY-MM-DD-homepage-desktop.png
    YYYY-MM-DD-homepage-mobile.png
    YYYY-MM-DD-blog-desktop.png
```

## First freeze procedure

1. Locate the actual source currently used by WordPress and any Figma/design source.
2. Preserve the highest-quality editable source without destructive conversion.
3. Export SVG where the design is vector-compatible.
4. Export PNG and WebP at documented sizes.
5. Create black, white, and one-color variants only if they are visually reviewed.
6. Record SHA-256 for every canonical source and export.
7. Commit all approved records in one dated Git commit.
8. Save dated screenshots of the public homepage and Blog page using the logo.
9. Record public URLs, WordPress object/media IDs, Figma URL, and commit SHA in `logo-record.md`.

## `logo-record.md` fields

- Canonical name: `1minHow`
- Asset version: e.g. `logo-current-v0.1`
- Design description
- Original creator or generation method
- Creation/first-known-use date
- First public-use date and URLs
- Source file path
- Export file paths
- WordPress media ID and URL
- Figma/design-source URL
- Font or lettering source
- Modification notes
- Commit SHA
- SHA-256 values
- Review status

## Usage rules to document

- minimum size;
- safe clear space;
- approved light/dark backgrounds;
- no stretching, skewing, recoloring, outlining, or rearranging;
- whether the mark may be combined with the three theme systems;
- favicon/app-icon cropping behavior;
- bilingual lockup rules if Chinese text is added later.

## Font evidence

Record font name, version, source, and license separately from the logo art. Confirm permission for commercial use, web embedding, logo use, and modification. Do not commit font binaries unless redistribution is explicitly licensed.

If the logo lettering was modified from a font, preserve:

- the font identity and version;
- an outline/vector copy of the final lettering;
- a short description of modifications;
- the license evidence URL or document reference.

## Name and trademark screening plan

Before filing, document dated searches for:

- `1minHow`
- `1 Min How`
- `One Minute How`
- visually or phonetically similar names

Check search engines, domains, social handles, app stores, and the trademark databases for target markets. Record jurisdiction, date, classes searched, and results. A clear search is time-bounded and not a legal guarantee.

Likely business areas to evaluate include digital publishing/content, education/information services, software, and downloadable digital products. Final classes and conflict analysis should be reviewed by a qualified trademark professional in the target jurisdiction.

## Filing sequence recommendation

1. Freeze and document current use now.
2. Complete name/near-match screening.
3. Stabilize Blog typography and theme integration.
4. Consider a word-mark application for `1minHow` once the name and business scope are stable.
5. Consider a combined or graphic-mark application after the logo shape is unlikely to change.

## Change control

Every logo adjustment must create a new asset version and changelog entry. Do not overwrite historical source files. The website may point to `current`, but the manifest must resolve `current` to one immutable version and commit.
