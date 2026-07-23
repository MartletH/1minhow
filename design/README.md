# 1minHow Design

This directory contains implementation-ready design specifications and asset records.

Notion remains the authority for concise design philosophy, character personality, visual rules, and owner-approved decisions. GitHub stores detailed action tables, prompts, file manifests, hashes, export rules, and implementation evidence.

## Theme families

- `Doodle / 星空生态合唱` — small, distributed decorative characters with individual personalities and public-domain painting genes.
- `Linework / 宇宙` — restrained linework based on cosmic and natural imagery.
- `Ink / 山海` — mountain, sea, cloud, wind, birds, and living-flow imagery.

## Structure

```text
design/
  README.md
  characters/
    starry-ecosystem-choir-v0.1.md
  brand/
    logo/
      evidence-plan.md
      assets/          # source and export files, added after collection
      screenshots/     # dated public-use evidence
```

## Asset rules

1. Decorative assets are small and distributed, not one large illustration covering the page.
2. Eight named main characters receive complete personality, expression, and action sheets. Stars, moon, clouds, plants, mushrooms, water drops, light insects, and music marks are supporting elements.
3. Public-domain paintings provide cultural genes, not full-layout copies.
4. Every committed asset must have a clear source, license note, export size, and SHA-256 record.
5. Never commit licensed font binaries unless redistribution is explicitly permitted.
6. WordPress, Figma, and exported assets must point back to a canonical Git commit or manifest.
