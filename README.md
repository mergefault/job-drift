# job-drift

Worldwide job-listing drift across a curated set of technology companies using official public applicant-tracking-system feeds.

The repository collects published openings daily, normalizes objective fields, detects material changes, and publishes a dependency-free GitHub Pages dashboard. It does not scrape LinkedIn, Indeed, search results, or arbitrary career-site HTML.

## Sources

Collectors support the public Greenhouse Job Board API, Lever Postings API, and Ashby Job Postings API. The initial enabled catalogue contains only company board identifiers verified against live official feeds. Public listing endpoints require no API keys.

## Data semantics

Jobs retain the employer's title, location text, application URL and source provenance. Remote eligibility, country and compensation remain unknown unless the feed exposes usable structured values. A listing disappearing from a successful feed produces `JOB_CLOSED`; it does not assert that the role was filled. The first collection is a baseline and does not generate artificial posting events.

Events include `JOB_POSTED`, `JOB_CLOSED`, `TITLE_CHANGED`, `LOCATION_CHANGED`, `WORKPLACE_CHANGED`, `SALARY_CHANGED`, `DESCRIPTION_CHANGED`, and `JOB_UPDATED`.

## Operation

Node 24 is required. There are no runtime or development dependencies and no installation step.

```sh
npm test
npm run collect
npm run generate
```

The daily workflow isolates company failures, applies explicit request timeouts, validates normalized records, serializes runs through a concurrency group, and uses only `contents: write`. Generated site data lives under `docs/data/`.

## Adding a company

Add a reviewed entry to `config/companies.json` with the official company name, ATS type and public board identifier. Verify the feed before setting `enabled` to `true`. Do not infer board identifiers or add third-party aggregators.

## License

MIT
