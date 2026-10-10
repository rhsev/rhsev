## Three ideas tie these tools together

- **Markdown as data**: plain text with YAML blocks as a queryable source of truth.
- **Durable file identity**: files are referenced by a permanent id instead of a path, so metadata survives renaming, moving, and transfer.
- **Actionable URLs**: a URL is not a link but an instruction that something receives and acts on.

The tools are small portable engines and CLIs, with the macOS-specific work kept separate. Everything is plain text first, so the data stays readable without these tools.

---

### Markdown as data

**[grubber](https://github.com/rhsev/grubber)** is the query layer. It reads YAML blocks and frontmatter out of Markdown and JSONL files and answers field queries in JSON or TSV. Use your Markdown files like a database. **[matterbase](https://github.com/rhsev/matterbase)** builds an interactive table view and query builder on it, **[mark-twin](https://github.com/rhsev/mark-twin)** a config sync between machines that is defined in Markdown. The fileregister index is grubber-readable too.

### Durable file identity

A file gets a permanent id that survives rename, move, iCloud, and a different file system. The source of truth is a plain-text JSONL index, a kind of yellow pages for files. On macOS the bookmark is the main anchor that finds the file again, and it can be restored on another machine. Finder tags and other xattrs are a derived cache that can be rebuilt. **[fileanchor](https://github.com/rhsev/fileanchor)** is the macOS module that reads and writes bookmarks, Finder tags, comments, and xattrs. **[fileregister](https://github.com/rhsev/fileregister)** is the record CLI on top, called `register`. It keeps the index, groups files into binders without moving them, resolves and repairs references, and takes files with their records to another machine.

### Actionable URLs

**[dy.lan](https://github.com/rhsev/dy.lan)** is a URL router for the local network with plugin-based automation. It runs as a container. **[mi.lan](https://github.com/rhsev/mi.lan)** is the agent on the receiving machine, macOS or Linux. A URL arrives and a script runs, on a Mac also a Shortcut. Together they are a local RPC layer. **[ticker](https://github.com/rhsev/ticker)** is an LED dot-matrix ticker in the menu bar, driven from the command line. It also handles the `ref://` scheme, so `ref://id/<aka>` opens a file by its durable id.
