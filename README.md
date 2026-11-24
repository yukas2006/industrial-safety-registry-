# EPB Registry

A local desktop application for managing industrial safety expertise (EPB) conclusions and searching them by description. Built for a single user, no network or authentication required.

## The problem

Industrial safety expertise conclusions (EPB) are often tracked in spreadsheets or paper archives. Finding a specific conclusion by equipment name, registration number, expert name, or a fragment of the repair measures text is slow, and there's no easy way to see which conclusions expire soon.

## What it does

- **Conclusions registry** — 16 fields per conclusion (equipment, organization, dates, registration numbers, file links, repair measures) plus a free-text field for the expert organization.
- **Experts with attestation areas** — multiple experts per conclusion, each with multiple attestation areas. The same expert can have different areas in different conclusions.
- **Full-text search** — search across equipment name, conclusion number, registration number, factory number, RTN registry number, and repair measures. Plus search by organization, department, device type, expert organization, and expert name.
- **Filters** — by organization, EPB object type, expert organization, expert, signing date range, next expertise year, and presence of repair measures.
- **Document links** — scan of the conclusion, RTN notification, EDS (electronic digital signature) files, and supporting documents — all stored as URLs (e.g., Yandex.Disk).
- **Autocomplete** — suggestions for organizations, departments, device types, expert organizations, expert names, and attestation areas, drawn from existing records.
- **Orphan cleanup** — when a conclusion is deleted or edited, dictionary entries that are no longer referenced are removed automatically (so typos don't linger in suggestions).
- **Sticky header/footer** — author credit and version in the UI.

## Tech stack

| Layer | Technology |
|---|---|
| Language | Python 3.11 |
| ASGI server | Uvicorn |
| Web framework | FastAPI |
| Templating | Jinja2 |
| ORM | SQLAlchemy 2.x |
| Database | SQLite + FTS5 (full-text search) |
| Desktop window | pywebview |
| Packaging | PyInstaller (onedir) |

## Architecture

The app runs a local Uvicorn server on `127.0.0.1` and opens a native pywebview window that loads the UI. Everything is local — no network calls, no external services (except the URLs you paste, which point to your own cloud storage).
