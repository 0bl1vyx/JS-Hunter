# JS-Hunter

![JS-Hunter Banner](https://img.shields.io/badge/Version-5.7-brightgreen?style=flat-square) ![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square) ![Language](https://img.shields.io/badge/Language-Bash-yellow?style=flat-square)

A powerful, hacker-themed Bash tool for discovering JavaScript files from a list of domains, analyzing them for secrets, paths, and links, and optionally verifying extracted secrets. Inspired by the Matrix aesthetic, JS-Hunter combines multiple reconnaissance tools for efficient bug bounty hunting, security research, and web asset enumeration.

Built by **Crypt Specter**. Version 5.7.

## Features

- **Multi-Level JS Discovery**: Choose from 1 to 4 levels of depth using tools like `subjs`, `katana`, `waybackurls`, and `gau` to uncover JS files from live sites, archives, and crawls.
- **Live URL Filtering**: Uses `httpx` to verify only responsive (200 OK) JS URLs.
- **Secret Extraction**: Scans JS files for sensitive data (e.g., API keys, tokens) using `secretfinder`.
- **Endpoint and Link Discovery**: Extracts relative paths and absolute links from JS files with `linkfinder`.
- **Secret Verification**: Automatically checks validity of common secrets (e.g., Google OAuth, Stripe, GitHub tokens) via API calls.
- **Concurrency Control**: Adjustable parallel processing for faster scans.
- **Verbose Mode**: Detailed output for debugging and insights.
- **Hacker UI**: Minimalist, green-themed interface with spinners, banners, and progress indicators.
- **Output Flexibility**: Save results to custom files for JS URLs, secrets, verified secrets, paths, and links.
- **Safety Features**: Overwrite confirmation, dependency checks, and temporary file cleanup.

## Dependencies

JS-Hunter relies on the following external tools. Install them via your package manager (e.g., `go install`, `apt`, or `brew`) before running:

- `httpx` (required for live filtering)
- `subjs` (Level 1 discovery)
- `katana` (Level 2 discovery)
- `waybackurls` (Level 3 discovery)
- `gau` (Level 4 discovery)
- `secretfinder` (for secret extraction, if `-s` is used)
- `linkfinder` (for path/link extraction, if `-p` or `-l` is used)

The script dynamically checks for required dependencies based on your options and exits if any are missing.

**Note**: No internet access is needed beyond the tools themselves. Ensure tools are in your `$PATH`.

## Installation

1. Clone the repository:
   ```
   wget https://raw.githubusercontent.com/0bl1vyx/JS-Hunter/refs/heads/main/JS-Hunter
   ```

2. Make the script executable:
   ```
   chmod +x JS-Hunter
   ```

3. Install dependencies (example for Go-based tools):
   ```
   go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest
   go install github.com/projectdiscovery/katana/cmd/katana@latest
   go install github.com/lc/gau/v2/cmd/gau@latest
   go install github.com/tomnomnom/waybackurls@latest

   git clone https://github.com/lc/subjs
   cd subjs
   sudo go build
   sudo mv subjs /usr/local/bin
   ```

   Adjust based on your OS and preferred installation method.

## Usage

Run the script with your domain list and desired options:

```
./JS-Hunter [options]
```

### Essential Options
- `-dl <file>`: Input file containing a list of domains (one per line, e.g., `domains.txt`).

### Optional Options
- `-o <file>`: Output file for discovered JS URLs (e.g., `js.txt`).
- `-s <file>`: Output file for extracted secrets (e.g., `secrets.txt`).
- `-cs <file>`: Output file for verified secrets (requires `-s`, e.g., `verified.txt`).
- `-p <file>`: Output file for extracted paths (e.g., `paths.txt`).
- `-l <file>`: Output file for extracted links (e.g., `links.txt`).
- `-lv <1-4>`: Discovery level (1: basic, 4: comprehensive; default: 4).
- `-c <num>`: Concurrency level for parallel processing (default: 4).
- `-v`: Enable verbose output for extra details.
- `-h, --help`: Display the help menu.

The script will prompt for confirmation before overwriting existing output files.

### Example

Basic scan for JS URLs at level 2 with concurrency 8:
```
./JS-Hunter -dl domains.txt -o js.txt -lv 2 -c 8
```

Full analysis with secrets, verification, paths, links, and verbose mode:
```
./JS-Hunter -dl domains.txt -o js.txt -s secrets.txt -cs verified.txt -p paths.txt -l links.txt -lv 4 -c 8 -v
```

Input `domains.txt` example:
```
example.com
sub.example.com
```

## How It Works

1. **Discovery Phase**: Gathers JS URLs using selected tools based on level.
2. **Consolidation**: Merges and deduplicates URLs.
3. **Live Filtering**: Checks for 200 OK responses.
4. **Analysis Phase**: Scans for secrets, paths, and links (if requested).
5. **Verification Phase**: Tests secret validity for supported types (e.g., Google, Facebook, Stripe).
6. **Summary**: Displays counts and exports results.

Phases include progress spinners for a smooth CLI experience.

## Output Format

- **JS URLs**: One URL per line.
- **Secrets**: Tool output with separators between files.
- **Verified Secrets**: Format like `type: secret (verified)`.
- **Paths**: Relative paths (e.g., `/api/v1/user`).
- **Links**: Absolute URLs (e.g., `https://api.example.com/endpoint`).

Empty output files are automatically removed.

## Limitations

- Relies on external tools; ensure they are up-to-date.
- Secret verification is limited to specific types (Google OAuth, Facebook, Mailgun, Square, Stripe, GitHub).
- No proxy support built-in; configure in underlying tools if needed.
- Designed for ethical use only—respect robots.txt and legal boundaries.

## Contributing

Pull requests welcome! For major changes, open an issue first. Ensure code follows the hacker-minimalist style.

## License

MIT License. See [LICENSE](LICENSE) for details.

## Author

- **Crypt Specter** - [GitHub](https://github.com/cryptspecter)

Happy hunting! 🚀
