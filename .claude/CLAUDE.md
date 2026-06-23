# CLAUDE.md — Writing

## About

This repository serves as a central location for developing, collecting and publishing write-ups.

A write-up is any standalone text that may be published as, for example, an article.

## Directory structure

```
drafts/     # Work-in-progress write-ups
finished/   # Finished write-ups
```

Each write-up in `drafts/` or `finished/` is a directory with the following structure:

```
write-up-title/  # Title of the write-up in kebab-case
  index.md       # Main content of the write-up
  diagram.png    # Assets used by the write-up
  ...
```

Notes:

- When a write-up is finished and ready for publishing, it is moved from the `drafts/` directory to the `finished/` directory.
- The directory name of a write-up may still change while it's in the `drafts/` directory, but it shouldn't change anymore when it's in the `finished/ directory.
- The directory name of a write-up ideally corresponds to the write-up's title (as defined in `index.md`) in kebab-case. However, this is not a strict requirements, if, for example, the title is very long or the directory name differs just slightly from the title.

## Structure of `index.md`

- Pure Markdown, no YAML frontmatter
- Starts with a `#` heading with the title of the write-up
- References assets with relative paths (e.g. `./diagram.png`)

## Write-up ideas

Ideas for future write-ups are tracked in GitHub Issues, not in repository files.

## Future work

- Publishing pipeline: use this repoitory as the source for a publishing pipeline that publishes finsished write-ups to one or more destinations, like a website (e.g. through an SSG) or a platform like Medium. The publishing pipeline is read-only and the single source of truth of the write-ups remains in this repository.
- Metadata extraction: extract metadata about write-ups, in particular the 'created' date and the 'last edited' date from the Git history (if necessary, use `git log --follow` to track directory renames)
