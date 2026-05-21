# Table Column Generation Rule

Table columns are generated from resource `columns`.

## Column Fields

- `key`: data path.
- `label`: visible header.
- `type`: text, number, boolean, datetime, date, enum, action.
- `sortable`: enables server sort UI.
- `searchable`: adds to search fields.
- `filterable`: connects to filters.

## Rendering

- text: fallback `-`.
- number: formatted number.
- boolean: status badge or text.
- datetime: project date formatter.
- enum: label map.
- action: callback buttons.

## Rules

- Preserve input order.
- Keep renderer display-only.
- Put column defs in `entities/{resource}/lib`.
