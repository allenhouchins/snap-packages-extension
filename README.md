# Snap Packages Osquery Extension (Go)

A Go-based osquery extension that provides snap package information as a native table.

## Table Schema

| Column     | Type   | Description                    |
|------------|--------|--------------------------------|
| name       | TEXT   | Snap package name              |
| version    | TEXT   | Package version                |
| rev        | TEXT   | Revision number                |
| tracking   | TEXT   | Tracking channel               |
| publisher  | TEXT   | Package publisher              |
| notes      | TEXT   | Additional notes               |

## Building the Extension

1. Clone the repository
2. Install dependencies:
   ```bash
   go mod tidy
   ```
3. Build the extension:
   ```bash
   make build
   ```
   or manually:
   ```bash
   go build -o snap_packages.ext
   ```

## Usage

### With Fleet
```bash
sudo orbit shell -- --extension snap_packages.ext --allow-unsafe
```

### With standard osquery
```bash
osqueryi --extension=/path/to/snap_packages.ext
```

### Example Queries

```sql
-- List all snap packages
SELECT * FROM snap_packages;

-- Find packages by publisher
SELECT * FROM snap_packages WHERE publisher = 'canonical';

-- Check for specific package
SELECT * FROM snap_packages WHERE name = 'docker';

-- Count total packages
SELECT COUNT(*) as total_packages FROM snap_packages;
```

## Structure

```
├── main.go              # Main extension code
├── go.mod               # Go module definition
├── Makefile             # Build configuration
└── README_GO_EXTENSION.md # This file
```

## Comparison with Shell Script

This Go extension replaces the functionality of `create_snap_database.sh` by:

- **Direct Integration**: No need for SQLite database creation
- **Real-time Data**: Always returns current snap package information
- **Native osquery Table**: Can be queried like any other osquery table
- **Cross-platform**: Works on any Linux system with snap support
- **Performance**: More efficient than shell script + SQLite approach

## Requirements

- Go 1.21 or later
- Linux system with snap support
- osquery or Fleet

## License

Same as the parent project. 