# JS-Hunter v6.1

**JS-Hunter** is a blazing-fast, dependency-light Bash script for comprehensive JavaScript reconnaissance. It automates the discovery of JS files from multiple sources, then uses a powerful native regex engine to extract secrets, API endpoints, and external links—all without relying on external Python tools for analysis.

Designed with a hacker-themed, Matrix-inspired UI, JS-Hunter is the perfect companion for bug bounty hunters, penetration testers, and security researchers looking to streamline their web asset discovery and analysis workflow.

## ✨ Key Features

  * **Multi-Source JS Discovery**: Aggregates JS files from up to 4 different strategies (`subjs`, `katana`, `waybackurls`, `gau`) for maximum coverage.
  * **Blazing-Fast Native Analysis**: Scans files for secrets, paths, and links using a highly efficient, built-in regex engine—no more `linkfinder` or Python dependencies\!
  * **Secret Verification**: Automatically validates discovered API keys for services like GitHub, Slack, Google, and more, separating real threats from false positives.
  * **Dependency-Light**: The core analysis engine is 100% native Bash. You only need the Go-based discovery tools you choose to use.
  * **Advanced Concurrency**: Processes multiple domains and URLs in parallel to get you results in a fraction of the time.
  * **Flexible Output**: Save JS URLs, secrets, verified secrets, paths, and links to separate, neatly organized files.
  * **Hacker-Ready UI**: A clean, minimalist interface with banners, spinners, and color-coded output that makes reconnaissance feel like you're in the Matrix.
  * **Safe & Smart**: Includes automatic dependency checks, confirmation prompts before overwriting files, and robust cleanup of temporary files.

-----

## ⚙️ Workflow

The tool follows a simple but powerful 4-stage workflow:

```
            ┌────────────────┐     ┌───────────────┐     ┌────────────────┐     ┌──────────┐
Input List ─►│ 1. Discover JS ├─►─► │ 2. Consolidate├─►─► │  3. Analyze    ├─►─► │ 4. Output│
(domains.txt)│ (subjs, gau...)│     │ (Unique URLs) │     │ (Regex Engine) │     │ (files)  │
            └────────────────┘     └───────────────┘     └────────────────┘     └──────────┘
```

-----

## 📦 Installation

1.  **Download the script directly**

    ```bash
    wget https://raw.githubusercontent.com/0bl1vyx/JS-Hunter/refs/heads/main/JS-Hunter
    ```

2.  **Make the script executable:**

    ```bash
    chmod +x JS-Hunter
    ```

3.  **Install Dependencies:**
    JS-Hunter's core analysis engine is dependency-free. You only need to install the discovery tools based on the `-lv` (level) you intend to use.

    ```bash
    # (Required for Level 1)
    go install -v github.com/lc/subjs@latest

    # (Required for Level 2)
    go install -v github.com/projectdiscovery/katana/cmd/katana@latest

    # (Required for Level 3)
    apt install waymore
    ```

    Ensure that your Go bin directory (`$HOME/go/bin`) is in your system's `$PATH`.

-----

## 🚀 Usage

The script is controlled via simple command-line flags.

### **Options**

| Flag | Argument | Description | Required |
| :--- | :--- | :--- | :--- |
| `-dl` | `<file>` | Input file containing a list of domains (one per line). | **Yes** |
| `-o` | `<file>` | Output file to save all discovered JS URLs. | No |
| `-s` | `<file>` | Output file to save discovered secrets. | No |
| `-cs` | `<file>` | Output file to save **verified** secrets (requires `-s`). | No |
| `-p` | `<file>` | Output file to save discovered paths/endpoints. | No |
| `-l` | `<file>` | Output file to save discovered external links. | No |
| `-lv` | `<1-4>` | Discovery level (default: 4). Higher is more thorough. | No |
| `-c` | `<num>` | Concurrency level for parallel tasks (default: 4). | No |
| `-v` | | Enable verbose mode for detailed execution logs. | No |
| `-h` | | Display the help menu. | No |

### **Examples**

  * **Simple Scan:** Find JS files for a list of domains and print results to the terminal.

    ```bash
    ./JS-Hunter -dl domains.txt
    ```

  * **Full Recon:** Use the highest discovery level, save all outputs, and verify secrets with high concurrency.

    ```bash
    ./JS-Hunter -dl domains.txt -o js_urls.txt -s secrets.txt -cs verified_secrets.txt -p paths.txt -l links.txt -c 20
    ```

  * **Stealthy & Fast:** Use only Level 1 discovery (`subjs`) to quickly find secrets.

    ```bash
    ./JS-Hunter -dl domains.txt -lv 1 -s secrets.txt
    ```

-----

## 🤝 Contributing

Contributions, issues, and feature requests are welcome\! Feel free to check the [issues page](https://www.google.com/search?q=https://github.com/0bl1vyx/JS-Hunter/issues).

## 📜 License

This project is licensed under the MIT License. See the `LICENSE` file for details.
