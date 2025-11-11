# repo-context

Generate repository context for AI consumption - perfect for feeding your codebase to AI assistants.

## Features

- ✅ Respects `.gitignore` automatically
- ✅ Supports `.repoignore` for additional project-specific exclusions
- ✅ `-e` flag for temporary runtime exclusions
- ✅ `-i` flag to force include normally ignored files
- ✅ Excludes `.git` directory automatically
- ✅ Generates readable file tree with emojis
- ✅ Wraps file contents in `<file>` tags for AI parsing
- ✅ Cross-platform (Linux, Windows, macOS)

## Installation

Download the binary for your platform from [Releases](https://github.com/coder-maks/repo-context/releases/latest):

| Platform | Binary |
|----------|--------|
| Linux | `repo-context-linux-x86_64` |
| Windows | `repo-context-windows-x86_64.exe` |
| macOS (Intel) | `repo-context-macos-x86_64` |
| macOS (Apple Silicon) | `repo-context-macos-arm64` |

### Quick Install (Linux/macOS)

```bash
# Download
curl -L https://github.com/coder-maks/repo-context/releases/latest/download/repo-context-linux-x86_64 -o repo-context

# Make executable
chmod +x repo-context

# Move to PATH (optional)
sudo mv repo-context /usr/local/bin/
```

### Windows

Download `repo-context-windows-x86_64.exe`, rename to `repo-context.exe`, and run in terminal.

## Quick Start

```bash
# Basic usage - respects .gitignore and .repoignore
./repo-context

# Specify output file
./repo-context --output ai-context.md

# Get help
./repo-context --help
```

This generates a `context.md` file with your repository structure and contents.

## Usage

### Basic Options

```bash
# Generate context with default settings
./repo-context

# Custom output file
./repo-context -o my-context.md

# Tree structure only (no file contents)
./repo-context --tree-only
```

### Exclusions (`-e` flag)

Temporarily exclude files/patterns beyond `.gitignore` and `.repoignore`:

```bash
# Exclude specific patterns
./repo-context -e "*.png,*.jpg"

# Exclude directories
./repo-context -e "assets/,docs/"

# Multiple patterns
./repo-context -e "*.png,target/,node_modules/"
```

### Force Include (`-i` flag)

**Override** `.gitignore` and `.repoignore` to include specific files:

```bash
# Include a normally ignored file
./repo-context -i "error.log"

# Include multiple files
./repo-context -i "*.log,debug.txt"

# Include directory
./repo-context -i "secrets/config.yaml"
```

### Combined Usage

```bash
# Exclude all images but include logo.png
./repo-context -e "*.png,*.jpg" -i "logo.png"

# Exclude assets directory but include config
./repo-context -e "assets/" -i "assets/config.json"

# Complex filtering
./repo-context -e "*.mp4,*.zip" -i "demo.mp4" -o demo-context.md
```

## Configuration

### `.repoignore` File

Create a `.repoignore` file in your repository root for project-specific exclusions:

```gitignore
# repo-context ignore file
# Syntax: same as .gitignore

# Build artifacts
target/
dist/
*.exe
*.dll

# IDE files
.vscode/
.idea/
*.swp

# Large files
*.zip
*.tar.gz
assets/**/*.png

# Logs
*.log
```

Then simply run:
```bash
./repo-context
```

### Priority Order

Rules are applied with the following priority (highest to lowest):

1. **`-i` flag** (force include) - **HIGHEST PRIORITY** ✅
2. **`-e` flag** (runtime exclude) ❌
3. **`.repoignore`** (project exclude) ❌
4. **`.gitignore`** (base exclude) ❌

**Example:**
- `.gitignore` excludes `*.log`
- `.repoignore` excludes `debug/`
- You run: `./repo-context -e "*.md" -i "error.log"`
- **Result:** `error.log` is included (despite `.gitignore`), all `.md` files excluded

## Examples

### Scenario 1: Basic AI Context

Generate clean context for AI (exclude heavy assets):

```bash
./repo-context -e "*.png,*.jpg,*.mp4,assets/videos/"
```

### Scenario 2: Debug Session

Include normally ignored logs for debugging:

```bash
./repo-context -i "*.log,debug/"
```

### Scenario 3: Documentation Only

Get only markdown documentation:

```bash
./repo-context -e "*.rs,*.toml,src/,target/" -i "README.md,docs/*.md"
```

### Scenario 4: Specific Feature Context

Focus on a specific module (Bevy game example):

```bash
./repo-context -e "assets/,target/" -i "Cargo.toml" -o gameplay-context.md
```

## Output Format

The generated markdown file contains:

```markdown
# Repository Context

## Additional Exclusions
- ❌ `*.png`
- ❌ `target/`

## Force Included (Override .gitignore)
- ✅ `logo.png`

## File Tree
```
📁 src
  📄 ./src/main.rs
📄 ./Cargo.toml
```

## File Contents

<file path="./src/main.rs">
fn main() {
    println!("Hello, world!");
}
</file>
```

Perfect for copying into AI chat interfaces like Claude, ChatGPT, or other LLMs.

## Use Cases

- 🤖 **AI Code Review** - Feed entire codebase to AI assistants
- 📚 **Documentation** - Generate project snapshots for onboarding
- 🔍 **Code Analysis** - Provide context for static analysis tools
- 💬 **Debugging** - Share complete context when asking for help
- 🎓 **Learning** - Export project structure for studying

## Integration

### GitHub Actions

See the [GitHub Actions Guide](https://github.com/coder-maks/repo-context/wiki/GitHub-Actions) for automated context generation.

### CI/CD

```yaml
- name: Generate Context
  run: |
    curl -L https://github.com/coder-maks/repo-context/releases/latest/download/repo-context-linux-x86_64 -o repo-context
    chmod +x repo-context
    ./repo-context -e "*.png,target/" -o context.md
```

## License

MIT - see [LICENSE](LICENSE) file

## Contributing

Issues and PRs welcome! This is a simple tool - keep it simple.