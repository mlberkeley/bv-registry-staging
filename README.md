# bv-registry-staging

Auto-generated draft manifests for [bv](https://github.com/mlberkeley/bv).

**Do not depend on this repo directly.** Manifests here are auto-generated from
Bioconda by `bv-ingest` and may be incomplete. Reviewed manifests are promoted
to [bv-registry](https://github.com/mlberkeley/bv-registry).

## Layout

```
tools/
  <tool-id>/
    <version>.toml    # draft manifest; may lack typed I/O
```

## Reviewer workflow

1. A nightly job opens one PR per tool to this repo (`ingest/<tool>-<version>` branch).
2. Open the PR, read the upstream README, fill in `[[tool.inputs]]` and `[[tool.outputs]]`.
3. Verify `[tool.entrypoint]` is correct.
4. Merge the PR.
5. Run `bv-ingest promote <tool> <version> --staging-dir <local-clone>` to open a PR against bv-registry.

A review should take under 5 minutes. If a tool's I/O is genuinely unclear, leave a comment on the PR.

## Available types

See [`bv-types/types.toml`](https://github.com/mlberkeley/bv/blob/main/bv-types/types.toml) for the full vocabulary.

Common ones:

| Type | Description |
|---|---|
| `fasta` | FASTA sequence file (`fasta[protein]`, `fasta[nucleotide]`) |
| `fastq` | FASTQ with quality scores |
| `bam` | Binary Alignment Map |
| `sam` | Sequence Alignment/Map (tabular) |
| `vcf` | Variant Call Format |
| `pdb` | Protein Data Bank structure |
| `blast_db` | BLAST database directory |
| `blast_tab` | BLAST tabular output (outfmt 6) |
| `hmm_profile` | HMMER profile |
| `dir` | Generic output directory |

## What bv-ingest fills in automatically

- `tool.id`, `tool.version`, `tool.description`, `tool.license`, `tool.homepage`
- `tool.image.reference` and `tool.image.digest` from quay.io/biocontainers
- `tool.entrypoint.command` (best-guess from recipe test commands)
- `tool.hardware` defaults (1 CPU, 2 GB RAM)

## What you fill in

- `[[tool.inputs]]` — typed input ports
- `[[tool.outputs]]` — typed output ports
- Adjust `[tool.hardware]` if the tool has known requirements
- Correct `[tool.entrypoint]` if the auto-detected command is wrong
