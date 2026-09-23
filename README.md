# Erdős numbers and collaboration networks in Icelandic engineering

`erdos-eng-is` is a focused research project about collaboration in Icelandic
engineering. It is a spin-off from
[`HI-IDN/skemman-msc`](https://github.com/HI-IDN/skemman-msc) and uses data
collected by
[`HI-IDN/skemman-harvester`](https://github.com/HI-IDN/skemman-harvester).

## Research questions

1. **Who among Icelandic engineering researchers has the lowest genuine Erdős
   number?** Here, a genuine Erdős path is a documented chain of research
   co-authorship to Paul Erdős.
2. **Who is structurally the “Erdős of Icelandic engineering”?** This is a
   network question rather than an Erdős-number question. It asks who occupies
   the most central or connective position in Icelandic engineering through
   co-authorship and MSc co-supervision.

The two questions are deliberately kept separate: a short path to Erdős does
not by itself make someone central to the Icelandic engineering network.

## Relationship to the other repositories

- **`skemman-harvester`** owns collection, parsing, caching, and the normalized
  DuckDB data model. It already supports OAI-PMH and XOAI harvesting, file and
  title-page metadata, and author/advisor loading. Harvesting logic belongs
  there and should not be duplicated here.
- **`skemman-msc`** studies how MSc engineering education has changed over
  time. Some of its data-selection and identity-resolution work may be reused,
  but features unrelated to collaboration networks should stay upstream.
- **`erdos-eng-is`** owns the network-specific analysis: resolving researchers,
  adding bibliographic co-authorship evidence, constructing co-authorship and
  MSc co-supervision graphs, measuring structure, and documenting genuine
  Erdős paths.

The project may later sit under a broader **`erdos-is`** umbrella covering
other departments or disciplines.

## Data workflow

The default input is the DuckDB database produced by `skemman-harvester`; this
repository does not crawl Skemman itself.

```powershell
python -m venv .venv
.venv\Scripts\activate
pip install "skemman-harvester @ git+https://github.com/HI-IDN/skemman-harvester.git"

# Run in a separate data workspace configured for the relevant collections.
skemman oai-pmh
skemman metadata-load
skemman oai-pmh --metadata-prefix xoai
skemman files-load
skemman people-load
```

Large or derived datasets are local artifacts and are not committed here. The
analysis should accept an explicit path to the upstream DuckDB database.

## Work organization

This work shares the HI-IDN project used for Skemman MSc thesis analysis. Use
these labels to keep responsibilities clear:

- **`skemman`** — harvesting, parsing, caching, and data infrastructure;
- **`msc-eng`** — longitudinal MSc engineering education analysis;
- **`erdos-eng`** — Erdős paths and engineering collaboration networks.

## Initial scope

The first analysis should:

1. define the Icelandic engineering researcher population and observation
   period;
2. resolve people consistently across thesis supervision and publication data;
3. retain source evidence for every co-authorship edge used in an Erdős path;
4. build separate co-authorship and MSc co-supervision graphs before combining
   them;
5. report centrality and brokerage measures with sensitivity checks, rather
   than naming an “Erdős” from a single metric.

## License

MIT. See [LICENSE](LICENSE).
