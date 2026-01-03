# Mikrus Wiki Rules Updater

This script automatically extracts all content from the Mikrus wiki (https://wiki.mikr.us) and creates individual `.mdc` rule files in `.cursor/rules/` directory for Cursor IDE.

## Features

- ✅ Downloads the entire Mikrus wiki from GitHub
- ✅ Extracts all Markdown files from the repository
- ✅ Creates individual `.mdc` files in `.cursor/rules/` directory (one per wiki page)
- ✅ Checks for updates automatically (compares commit hashes)
- ✅ Cleans up temporary files (doesn't keep the full repo on disk)
- ✅ Only keeps the `.mdc` rule files (doesn't keep the full repo)

## Usage

### First Time / Manual Update

```bash
python3 update_mikrus_rules.py
```

### Force Update (even if up to date)

```bash
python3 update_mikrus_rules.py --force
# or
python3 update_mikrus_rules.py -f
```

## How It Works

1. **Update Check**: Compares the latest commit hash from GitHub with the last downloaded version
2. **Download**: If updates are available (or forced), downloads the repository as a ZIP archive
3. **Extract**: Extracts all Markdown files from the `content/` directory
4. **Generate**: Creates individual `.mdc` files in `.cursor/rules/` with YAML frontmatter
5. **Cleanup**: Removes temporary files and repository

## Files Created

- `.cursor/rules/*.mdc` - Individual rule files for each wiki page (47 files total)
- `.mikrus_rules_update.json` - Tracks the last update (commit hash and timestamp)

**Note**: Cursor uses `.mdc` files in the `.cursor/rules/` directory (not `.cursorrules` file). Each wiki page becomes a separate rule file with YAML frontmatter.

## Update Frequency

The script automatically checks for updates each time you run it. It only downloads if:
- The commit hash has changed (new content available)
- You use the `--force` flag

## Notes

- The script requires internet access to download from GitHub
- Temporary files are stored in `.mikrus_temp/` and automatically cleaned up
- The repository is NOT kept on disk - only the final `.cursorrules` file
- SSL certificate verification is disabled for sandbox compatibility

## Troubleshooting

If you encounter issues:

1. **Network errors**: Ensure you have internet access
2. **Permission errors**: Make sure you have write permissions in the workspace directory
3. **SSL errors**: The script handles SSL issues automatically, but if problems persist, check your Python SSL certificates

## Source

- **Wiki**: https://wiki.mikr.us
- **Repository**: https://github.com/Mrugalski-pl/mikrus-dokumentacja
- **Branch**: `dev`

