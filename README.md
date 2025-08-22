# JSHunter

Bash script for JS recon: discovers JavaScript URLs from domains, filters live ones, extracts secrets/paths/links, and verifies specific secrets. Built for bug bounty hunters.

## Features
- Multi-level JS URL discovery (subjs, katana, waybackurls, gau).
- Live filtering with httpx (200 OK).
- Secret extraction via secretfinder.
- Endpoint/path/link extraction via linkfinder.
- Parallel secret verification for specific keys (Google OAuth, Facebook, etc.).
- Concurrency control, verbose mode.
- Hacker-themed UI with spinners and banners.

## Dependencies
- Core: bash, curl, xargs, httpx.
- Discovery: subjs, katana, waybackurls, gau (based on level).
- Analysis: secretfinder (for -s), linkfinder (for -p/-l).
Install via your package manager or Go (e.g., `go install github.com/hakluke/subjs@latest`).

## Installation
1. Clone repo: `git clone https://github.com/cryptspecter/JS-Hunter.git`
2. Make executable: `chmod +x JS-Hunter`
3. Run: `./JS-Hunter -h`

## Usage
```
./JS-Hunter [options]
```

| Option | Description | Required? |
|--------|-------------|-----------|
| `-dl <file>` | Domain list input (txt) | Yes |
| `-o <file>` | JS URLs output | No |
| `-s <file>` | Secrets output | No |
| `-cs <file>` | Verified secrets output (requires -s) | No |
| `-p <file>` | Paths output | No |
| `-l <file>` | Links output | No |
| `-lv <1-4>` | Discovery level (default: 4) | No |
| `-c <num>` | Concurrency (default: 4) | No |
| `-v` | Verbose | No |
| `-h, --help` | Help menu | No |

## Examples
- Basic recon: `./JS-Hunter -dl domains.txt -o js.txt`
- Full with verification: `./JS-Hunter -dl domains.txt -s secrets.txt -cs verified.txt -p paths.txt -l links.txt -lv 3 -c 10 -v`

## Contributing
Fork, PR with fixes/enhancements. Test thoroughly—don't break parallelism.

## License
MIT License. Use responsibly in authorized scopes.
