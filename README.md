# DataSync-API

> One-sentence pitch: a REST API that ingests, validates, and serves structured data (CSV/JSON/XML) across inconsistent client schemas.

## What it does

DataSync API lets you upload data in CSV, JSON, or XML format, normalizes it against a flexible schema-mapping layer, stores it in PostgreSQL, and exposes it back through a queryable REST interface. Built to handle the kind of messy, inconsistent data formats that show up when integrating with multiple external systems.

**Why I built it:** [1-2 sentences — e.g. "I wanted hands-on practice with the kind of data-format normalization and testing discipline used in production backend systems, since most of my prior projects focused on real-time features rather than data integrity."]

## Features

- Multi-format ingestion: upload CSV, JSON, or XML; auto-detect or specify schema mapping
- Configurable column/field aliasing so client A's `order_date` and client B's `OrderDate` map to the same internal field
- RESTful endpoints for create/read/update/delete plus bulk export in any supported format
- Input validation with detailed per-row error reporting (no silent data loss)
- 90%+ test coverage via Pytest, covering parsing edge cases (missing columns, malformed rows, encoding issues)
- CI pipeline (GitHub Actions) running lint + full test suite on every push
- Query optimization: indexed lookups on high-traffic fields, reducing average response time by XX%

## Tech stack

| Layer | Tool |
|---|---|
| Backend | Django, Django REST Framework |
| Database | PostgreSQL |
| Testing | Pytest, coverage.py |
| CI/CD | GitHub Actions |
| Other | [Pandas for parsing? lxml for XML? — fill in] |

## Architecture

```
Client → REST API (DRF) → Schema Mapper → Validator → PostgreSQL
                                ↓
                        Error Report (per-row)
```

[Replace with an actual diagram if you have one — even a simple draw.io export or ASCII box diagram helps a lot here.]

## Getting started

```bash
git clone https://github.com/USERNAME/REPO.git
cd REPO
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env  # add your DB credentials
python manage.py migrate
python manage.py runserver
```

## Running tests

```bash
pytest --cov=. --cov-report=term-missing
```

## API reference (example)

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/imports/` | Upload a file (CSV/JSON/XML) for ingestion |
| GET | `/api/records/` | List records with filtering/pagination |
| GET | `/api/records/{id}/` | Retrieve a single record |
| GET | `/api/records/export/?format=csv` | Bulk export in chosen format |

Full API docs: [link to Postman collection / Swagger / docs site if you add one]

## What I'd improve next

- [Be honest here — e.g. "Add async processing for large file uploads via Celery" or "Support nested/hierarchical JSON schemas"]

## License

MIT
