# CLAUDE.md — Nightingale

## Current task

- Combine my-journey-to-the-ideal-note-taking-app and the-desk-drawer-shelf-note-taking-method to a unified story about "My Personal Knowledge Management Saga/Odysee". Additional content is currently being prepared in the Owl project.

## About

Currently, Nightingale serves as a central location for developing, collecting and publishing stories.

A story is any standalone text that may be published as, for example, an article.

## Directory structure

```
drafts/     # Work-in-progress stories
finished/   # Finished stories
```

Each story in `drafts/` or `finished/` is a directory with the following structure:

```
story-title/  # Title of the story in kebab-case
  index.md       # Main content of the story
  diagram.png    # Assets used by the story
  ...
```

Notes:

- When a story is finished and ready for publishing, it is moved from the `drafts/` directory to the `finished/` directory.
- The directory name of a story may still change while it's in the `drafts/` directory, but it shouldn't change anymore when it's in the `finished/ directory.
- The directory name of a story ideally corresponds to the story's title (as defined in `index.md`) in kebab-case. However, this is not a strict requirements, if, for example, the title is very long or the directory name differs just slightly from the title.
- Some stories in `drafts/` do additionally contain a `metadata.legacy.yaml` file containing a "created" and "last updated" date. These dates have been taken from the previous legacy file format and are just included for completeness. It's not yet sure if these dates will be used at all, but in any case, these `metadata.legacy.yaml` should eventually be deleted.

## Structure of `index.md`

- Pure Markdown, no YAML frontmatter
- Starts with a `#` heading with the title of the story
- References assets with relative paths (e.g. `./diagram.png`)

## Story ideas

Ideas for future stories are tracked in GitHub Issues, not in repository files.

## Future work

- Merging in legacy notes content: there is a set of old notes repositories (see the [Notes Repository Consolidation](https://github.com/users/weibeld/projects/69?pane=issue&itemId=202722447) project). There may be content that can be moved from these notes repositories to the files about the same topic in this repository. Also check whether other content may be transformed into a story in this repository.
- Publishing pipeline: use this repoitory as the source for a publishing pipeline that publishes finsished stories to one or more destinations, like a website (e.g. through an SSG) or a platform like Medium. The publishing pipeline is read-only and the single source of truth of the stories remains in this repository.
- Metadata extraction: extract metadata about stories, in particular the 'created' date and the 'last edited' date from the Git history (if necessary, use `git log --follow` to track directory renames)
