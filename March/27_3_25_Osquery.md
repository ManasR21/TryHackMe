## Osquery Interactive Mode

- Open terminal and run `osqueryi`.
- Use `.help` command for available commands.
- Example commands:
  - `.tables` - List all tables.
  - `.schema table_name` - Show table structure.
  - `.mode MODE` - Set output mode (csv, column, line, etc.).

## Listing Tables

- Use `.tables` to list all tables.
- Example: `.tables process` - List tables related to processes.
- Example: `.tables user` - List tables containing "user".

## Understanding Table Schema

- `.schema table_name` - View table schema.
- Example: `.schema users` - Displays columns like `username`, `uid`, `directory`, etc.

## Querying Data

- Basic SQL syntax: `SELECT column1, column2 FROM table;`
- Example: `SELECT gid, uid, description, username, directory FROM users;`
- Returns user-related details.

## Display Modes

- Available modes:
  - `csv` - Comma-separated values.
  - `column` - Left-aligned columns.
  - `line` - One value per line.
  - `list` - Values delimited by separator.
  - `pretty` - Default formatted output.

## Exploring Installed Programs

- Check schema: `.schema programs`
- Query: `SELECT * FROM programs LIMIT 1;`
- Returns installed program details.
- Select specific columns:
  - `SELECT name, version, install_location, install_date FROM programs LIMIT 1;`

## Counting Entries

- Use `count()` to get total entries.
- Example: `SELECT count(*) FROM programs;`

## Filtering Results (WHERE Clause)

- Example: `SELECT * FROM users WHERE username='James';`
- Operators:
  - `=` Equal
  - `<>` Not equal
  - `>` Greater than
  - `<` Less than
  - `BETWEEN` Range
  - `LIKE` Wildcard search

## Wildcard Matching Rules

- `%` - Match all files/folders for one level.
- `%%` - Match all recursively.
- `abc%` - Match starting with "abc".
- `%abc` - Match ending in "abc".

## Required WHERE Clause

- Some tables require `WHERE` clause.
- Example: Querying `file` table without `WHERE` results in an error.
- Check documentation: [Osquery Schema](https://osquery.io/schema/#file)
