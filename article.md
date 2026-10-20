# Keep identifiers as text when editing CSV data

CSV delimiters preserve fields, but spreadsheet import settings can still change their values. Before editing a data catalogue, import identifier columns as text. Preserve signs, leading zeros, and JSON strings exactly unless a source-backed correction is intended.

After export, parse the original and edited CSV with a real CSV reader. Compare existing records by their stable identifier, check each row's width, and explain every changed value. Sorting records is a separate operation from rewriting their contents.

When the catalogue generates JSON, compare its actual generated output too. A new service can legitimately change provider-category metadata. Treat such metadata changes as evidence to inspect, rather than dismissing them as noise or assuming that a successful schema check proves every value is correct.

This note records the editing checks used for a small CSV catalogue contribution. It does not claim a GUI spreadsheet round-trip or an end-to-end publication integration.
