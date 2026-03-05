# CLAUDE.md — Project Notes for AI Assistants

## Project Overview

This is a personal academic website built with **HugoBlox Kit v2** (academic-cv template).
It uses Hugo modules (not a local theme directory) and deploys via GitHub Pages.

- Hugo module: `github.com/HugoBlox/kit/modules/blox`
- Template: `academic-cv`
- Author schema: `hugoblox/author/v1`

## Critical: Dual Author Data Sources

HugoBlox Kit v2 has TWO locations for author data. **Only `data/` is the primary source.**

| File | Purpose | Read by templates? |
|------|---------|-------------------|
| `data/authors/me.yaml` | **Primary author data** — all profile fields go here | **YES** |
| `content/authors/me/_index.md` | Author content page (body text only, frontmatter is NOT the primary data source) | Partially (page content only) |

### Mistake Log: Editing the Wrong File

**Commit 5d73ca9** added `work`, `skills`, `languages`, `social` fields to
`content/authors/me/_index.md` frontmatter instead of `data/authors/me.yaml`.

**Commit 8b69eb6** fixed field names (`social` -> `links`, `percent` -> `level`)
but still in `content/authors/me/_index.md` — the wrong file.

**Result**: Experience page showed no work history, no skills, no social links,
because the templates read from `data/authors/me.yaml` which had none of this data.

**Rule**: Always edit `data/authors/me.yaml` for profile data in this project.

## HugoBlox v2 Field Name Reference

These are the correct YAML field names as read by the HugoBlox Kit templates.
Do NOT use field names from older HugoBlox / Academic versions.

### Social Links (`links:` in data/authors/me.yaml)

```yaml
# CORRECT (HugoBlox Kit v2):
links:
  - url: "mailto:email@example.com"
    icon: "hero/envelope"
    label: Email
  - url: "https://github.com/username"
    icon: "brands/github"
    label: GitHub

# WRONG (old Academic / Wowchemy format — do NOT use):
social:
  - icon: envelope
    link: "mailto:email@example.com"
  - icon: github
    link: "https://github.com/username"
```

Mistakes made:
- Used `social:` instead of `links:` (template reads `$profile.links`)
- Used `link:` instead of `url:` per item
- Used bare icon names like `orcid` instead of prefixed `ai/orcid`
- Icon prefixes: `hero/` for Heroicons, `brands/` for brand icons, `ai/` for Academicons

### Skills (`skills:` in data/authors/me.yaml)

```yaml
# CORRECT:
skills:
  - name: Category Name
    items:
      - name: Skill Name
        description: "..."
        level: 4          # 0-5 integer scale

# WRONG:
skills:
  - name: Category Name
    items:
      - name: Skill Name
        description: "..."
        percent: 80       # template does NOT read 'percent' for skills
```

Mistake: Used `percent: 80` instead of `level: 4`. The `resume-skills` template
reads `level` (0-5 scale), validates it as numeric, and converts to percentage.

### Work Experience (`work:` in data/authors/me.yaml)

```yaml
# CORRECT — template accepts both field name variants:
work:
  - position: "Job Title"        # or: role
    company_name: "Company"      # or: org
    start: '2023-01-01'          # or: date_start
    end: '2024-01-01'            # or: date_end (omit for current)
    summary: |
      Description here
```

Template reads from `profile.experience` or `profile.work`.

### Education (`education:` in data/authors/me.yaml)

```yaml
# CORRECT (v2 data schema):
education:
  - degree: PhD in Something
    institution: University Name
    start: '2023-01-01'
    end: ''

# WRONG (old content frontmatter format):
education:
  - degree: PhD in Something
    institution: University Name
    startDate: '2023-01-01'     # 'startDate' is NOT the schema field
    endDate: ''                  # 'endDate' is NOT the schema field
```

Note: `content/authors/me/_index.md` frontmatter used `startDate`/`endDate`
but the `data/authors/me.yaml` schema uses `start`/`end`.

### Languages (`languages:` in data/authors/me.yaml)

```yaml
languages:
  - name: Chinese
    percent: 100       # 0-100 percentage (unlike skills which use 0-5 level)
```

## Homepage Content

The `resume-biography-3` block in `content/_index.md` has a `text:` field that
**overrides** the `bio:` field from `data/authors/me.yaml`. If the homepage bio
text needs updating, edit `content/_index.md` sections[0].content.text.

## Build & Deploy

- Site builds via GitHub Actions (`.github/workflows/build.yml` + `deploy.yml`)
- Hugo is NOT installed locally in this environment
- To test changes, push and check the GitHub Pages deployment
