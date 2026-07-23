# 1minHow Character Provenance and Rights Registry

## Purpose

This registry records when each character design was created, what public-domain cultural references informed it, which parts are original, who or what produced each source asset, and which immutable files were publicly used.

It is evidence and change control. It is not a legal opinion, copyright registration certificate, trademark clearance, or guarantee that no third party can make a claim.

## Registration rule

A character is not `frozen` until all of the following exist:

1. approved name and aliases;
2. fixed appearance memory points;
3. canonical front / 3/4 / side / back reference sheet;
4. approved palette and silhouette sheet;
5. source files and exported files;
6. prompt, human-edit, model/tool and contributor record;
7. public-domain source-art record with author, title and death/public-domain rationale;
8. SHA-256 for canonical assets;
9. one dated Git commit on `main`;
10. first-public-use URL and screenshot when published.

## Character registry

| ID | Character | Status | Public-domain painting gene | Original 1minHow contribution to record | Canonical commit | Public use |
|---|---|---|---|---|---|---|
| SEC-01 | Mona Meow / 萌娜丽猫 | concept-fixed; visual-sheet pending | Leonardo da Vinci, *Mona Lisa* | cat species, silhouette, shawl landscape motif, ambiguous-smile behavior, ecosystem role, action language and relationships | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |
| SEC-02 | Vincent Owl / 星夜鸮 | concept-fixed; visual-sheet pending | Vincent van Gogh, *The Starry Night* | owl anatomy, spiral-eye system, star-feather chest, observation behavior and action language | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |
| SEC-03 | Pearl Bun / 珍珠耳兔 | concept-fixed; visual-sheet pending | Johannes Vermeer, *Girl with a Pearl Earring* | rabbit anatomy, unequal listening ears, dew-drop pearl, listening role and action language | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |
| SEC-04 | Sunny Vulp / 向阳狐 | concept-fixed; visual-sheet pending | Vincent van Gogh, *Sunflowers* | fox anatomy, sunflower-tail system, petal ears, light-seeking behavior and action language | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |
| SEC-05 | Monet Frog / 睡莲蛙 | concept-fixed; visual-sheet pending | Claude Monet, *Water Lilies* | frog anatomy, lily-pad marker, reflection spots, rhythm-keeper role and action language | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |
| SEC-06 | Hoku / 浪浪鱼 | concept-fixed; visual-sheet pending | Katsushika Hokusai, *The Great Wave off Kanagawa* | crescent fish anatomy, wave-fin system, current-respecting behavior and action language | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |
| SEC-07 | Millet / 拾穗鼠 | concept-fixed; visual-sheet pending | Jean-François Millet, *The Gleaners* | field-mouse anatomy, wheat backpack, resource-care role and action language | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |
| SEC-08 | Luna Leo / 月眠狮 | concept-fixed; visual-sheet pending | Henri Rousseau, *The Sleeping Gypsy* | lion anatomy, crescent mane, night-guardian role and action language | `1223c9f566a21d2ef48f28085260a70fa96d0626` | pending |

## Asset manifest fields

Every canonical character asset must record:

- registry ID;
- character and state;
- asset version;
- filename and repository path;
- creator/contributor;
- generation model/tool and version, if applicable;
- complete prompt or source brief;
- human edits and editing software;
- source painting reference and public-domain note;
- creation date;
- review date and reviewer;
- dimensions and format;
- SHA-256;
- first public-use URL/date;
- replacement or superseded-by link.

## Public-domain reference boundary

- Use old public-domain paintings as cultural genes, not as copied full compositions or traced character assets.
- Record the exact historical work and artist for every reference.
- Do not use a modern museum photograph, scan, color restoration, derivative illustration, or contemporary artist's reinterpretation unless its license permits the intended use.
- Prefer self-created studies or verified open-access/public-domain reproductions when a source image is needed.
- Character names, anatomy, silhouette, behavior, palette system, scene use and relationships must be developed as original 1minHow material.

## External registration strategy

- Git history and dated public-use evidence should be created for every finalized character.
- Copyright protection may arise automatically when an original visual work is fixed, but optional government registration can create a stronger public record and additional remedies in some jurisdictions.
- Consider formal visual-art copyright registration after the eight canonical model sheets and first approved scene set are stable, rather than registering unfinished concepts repeatedly.
- Consider trademark screening/registration later for character names or character marks that become recurring commercial source identifiers. Copyright and trademark protect different interests.
- Jurisdiction, authorship, AI-generation disclosure and filing strategy should be reviewed with a qualified professional before filing.

## Change control

- Never overwrite a frozen character sheet.
- Major silhouette or face changes create a new asset version.
- Clothing and scene variations remain linked to the same character version only when all fixed memory points remain intact.
- Rejected generations may be retained privately for process evidence but do not belong in the canonical public asset set.
