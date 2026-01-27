# Compiled CVs

This directory placeholder exists for local development.

**Note:** Compiled PDFs are NOT stored in applications-repo (private). They are automatically pushed to the public cv-repo.

## Build Process

When you push changes to `main` that modify files in `curriculum_vitae/`:

1. GitHub Actions compiles the LaTeX files using XeLaTeX
2. Generated PDFs are pushed to `LevRoz630/cv-repo` (public repository)
3. PDFs are available at: https://github.com/LevRoz630/cv-repo/tree/main/docs

## Files Generated

- `swe-resume.pdf` - Software Engineering Resume
- `quant-resume.pdf` - Quantitative Finance Resume

## Local Compilation

To compile locally:
```bash
cd curriculum_vitae
xelatex swe-resume.tex
xelatex quant-resume.tex
```

PDFs will be generated in the `curriculum_vitae/` directory.
