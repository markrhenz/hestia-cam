# ⚠️ CRITICAL: File Handling Instructions for ALL AI Assistants

## 🚨 IMPORTANT NOTICE FOR ANY AI ACCESSING THIS FOLDER

**ALL AI assistants must read and follow these instructions before performing any file operations.**

This file contains critical safety guidelines to prevent permanent data loss. Any AI that accesses this folder MUST read this entire document and adhere to all guidelines.

## Safe File Operations Guidelines

To prevent accidental permanent deletion of important files, follow these guidelines:

### 1. Avoid Permanent Deletion
- **Do not use `del` command** for permanent deletion
- Instead, use `move` to relocate files to a backup folder
- Example: `move important-file.txt backup\` instead of `del important-file.txt`

### 2. Always Confirm Before Deletion
- Ask for user confirmation before removing any files
- Clearly state what files will be affected

### 3. Create Backups First
- Before any file operations, create backups of important files
- Use commands like `xcopy` or `robocopy` to preserve originals

### 4. Use Safer Commands
- Prefer `move` over `del`
- Use `rd /s /q` only when absolutely necessary and after confirmation
- Consider using version control (git) for important files

### 5. Recovery Options
- Keep backups in a dedicated folder
- Use version control systems
- Document important file locations

## Project Structure
This project follows the structure:
```
hestia-cam/
├── hestia-cam-main/
│   ├── index.html
│   ├── manifest.json
│   ├── sw.js
│   ├── cdn/
│   └── icons/
└── hestia-cam-server/
    ├── server.js
    └── package.json
```

## Important Files
- Preserve all source files in hestia-cam-main and hestia-cam-server
- Keep context files and documentation
- Use git for version control when possible

## AI Responsibility
Any AI assistant accessing this folder must:
1. Read this INSTRUCTIONS.md file FIRST
2. Acknowledge understanding of safe file handling
3. Follow all guidelines without exception
4. Ask for user confirmation before any potentially destructive operations
5. Create backups before making changes

**VIOLATION OF THESE GUIDELINES MAY RESULT IN PERMANENT DATA LOSS**