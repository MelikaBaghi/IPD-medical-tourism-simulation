# Releasing and archiving

This repository is already public, so the Zenodo archive can be set up now. There is
nothing to wait for.

A DOI is the thing that actually protects authorship. A licence header can be edited by
anyone who opens the file, but a DOI is a dated, third-party record that the model existed,
in this form, under these names, on a specific day. That is what you point at if attribution
is ever disputed, and it is what makes the model properly citable in other people's papers.

`.zenodo.json` supplies the deposit metadata, so the record comes out right without filling
in a web form.

## Step 1. Connect Zenodo to GitHub

1. Go to https://zenodo.org and sign in with GitHub. Zenodo asks for permission to read your
   repositories and add a webhook. It does not get write access to your code.
2. Go to https://zenodo.org/account/settings/github/
3. Find **IPD-medical-tourism-simulation** and switch the toggle **on**.

Use **Sync now** if it does not appear. Zenodo caches the repository list.

Do this before step 2. Zenodo only archives releases created after the toggle is on.

## Step 2. Cut the release

```bash
git tag -a v1.0.0 -m "IPD medical tourism hybrid simulation v1.0.0"
git push origin v1.0.0
gh release create v1.0.0 --title "v1.0.0" --notes "First archived release of the hybrid ABS+DES medical-tourism hospital model."
```

The DOI is minted within a minute or two.

## Step 3. Put the DOI where people will see it

Zenodo issues two DOIs. The **concept DOI** always points at the newest version and is the
one to publish. The version DOI points only at v1.0.0.

Add the badge at the top of `README.md`, under the title:

```markdown
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
```

Add it to `CITATION.cff` so the "Cite this repository" button shows it:

```yaml
doi: 10.5281/zenodo.XXXXXXX
```

And add it to the licence header inside `IPD27_hybrid.alp`, on the line under `Source:`, so
the DOI travels with the file itself rather than only with the repository.


## Later versions

Tag `v1.0.1` and release again. Zenodo files it as a new version under the same concept
DOI. Nothing needs reconnecting.

## Optional

**ORCID.** If you have one, add it to the author entries in both `.zenodo.json` and
`CITATION.cff`. It ties the model to you across every research index and survives changes of
institution and email. Registering takes about two minutes at https://orcid.org/register
