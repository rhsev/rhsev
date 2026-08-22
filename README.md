# What's here?

It's all about three ideas:

**Markdown as data** — plain text with YAML blocks as a queryable source of truth.
**Durable file identity** — metadata that survives renaming, moving, and transfer; recorded in plain text, not in the path.
**Actionable URLs** — a URL is not a link but an instruction: something receives it and acts.

The tools are small and composable: portable engines and CLIs (Go, Ruby), with the macOS-specific work isolated in one place. Everything is plain text first, built to outlive the apps that read it.

---

## Markdown as data

**[grubber](https://github.com/rhsev/grubber)** is the query layer: it reads YAML blocks and frontmatter out of Markdown (and JSONL) and answers field queries — JSON or TSV out. Think Dataview without Obsidian.

Consumers build on it: **[matterbase](https://github.com/rhsev/matterbase)** (interactive table view + query builder) and **[mark-twin](https://github.com/rhsev/mark-twin)** (Markdown-defined config sync between Macs); the fileregister records are grubber-readable too.

---

## Durable file identity

A file gets a permanent id, stamped into an xattr that survives rename, move, iCloud, and AirDrop. The source of truth is a plain-text JSONL index — the yellow pages; macOS metadata (Spotlight, bookmarks) is just a derived, regenerable cache.

**[fileanchor](https://github.com/rhsev/fileanchor)** is the swappable macOS module — the one place the platform-specific work lives: bookmarks, Finder tags, comments, and xattrs. Everything above it is portable. **[fileregister](https://github.com/rhsev/fileregister)** is the record CLI on top (`register`): the index, named collections as sets on the record, resolve/repair, and portable transfer with payload.

---

## Actionable URLs

**[dy.lan](https://github.com/rhsev/dy.lan)** is a URL router for the local network with plugin-based automation; it runs as a container. **[mi.lan](https://github.com/rhsev/mi.lan)** is the macOS side: a URL arrives, a script or Shortcut runs. Together they are a lightweight local RPC layer. `milan://<aka>` resolves a file by its durable id and opens it, on whatever machine holds it.

**[ticker](https://github.com/rhsev/ticker)** is an LED dot-matrix ticker in the menu bar, driven from the command line or by URL — it registers handlers for `milan://` and `ref://`.

---

| Repo | What it does | Idea | Builds on |
|---|---|---|---|
| [grubber](https://github.com/rhsev/grubber) | Query YAML in Markdown/JSONL — JSON/TSV out | Markdown data | — |
| [matterbase](https://github.com/rhsev/matterbase) | Table view + query builder on those records (TUI) | Markdown data | grubber |
| [mark-twin](https://github.com/rhsev/mark-twin) | Sync config folders between Macs from Markdown rules | Markdown data | grubber |
| [fileanchor](https://github.com/rhsev/fileanchor) | macOS file-metadata engine | Identity | — |
| [fileregister](https://github.com/rhsev/fileregister) | Durable ids + plain-text collections | Identity | fileanchor, grubber |
| [dy.lan](https://github.com/rhsev/dy.lan) | URL router for the LAN, plugin automation | URLs | — |
| [mi.lan](https://github.com/rhsev/mi.lan) | Trigger macOS scripts and Shortcuts via URL | URLs | fileregister |
| [ticker](https://github.com/rhsev/ticker) | LED ticker for the menu bar, CLI + URL handler | URLs | — |

