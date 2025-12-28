# PixelOS Build Script

Automated ROM build script with Telegram notifications and GoFile upload.

## Requirements

```bash
pip3 install requests
```

- Python 3.8+
- repo, git, jq

## Usage

```bash
./build.py <device> [options]
```

**Options:**
- `--skip-sync` - Skip source sync
- `--skip-clone` - Skip device repo cloning
- `--skip-upload` - Skip GoFile upload
- `--clean` - Clean build (make installclean)
- `--clean-repos` - Clean device repos before cloning
- `--build-dir PATH` - Custom build directory (default: ~/pos)

**Examples:**
```bash
# Full build
./build.py spartan

# Skip sync and clone (incremental build)
./build.py spartan --skip-sync --skip-clone

# Clean build without upload
./build.py spartan --clean --skip-upload
```

## Device Configuration

Add device configs to `devices/<codename>.json`:

```json
{
  "device": {
    "codename": "spartan",
    "full_name": "Realme GT Neo 3T"
  },
  "build": {
    "variant": "user",
    "target_release": "bp3a"
  },
  "environment": {
    "UNSAFE_DISABLE_HIDDENAPI_FLAGS": "true"
  },
  "repositories": {
    "device_tree": {
      "url": "https://github.com/...",
      "branch": "sixteen-qpr1",
      "path": "device/realme/spartan"
    }
  }
}
```

## Telegram Notifications

**Option 1:** Set environment variables
```bash
export TELEGRAM_BOT_TOKEN="your-bot-token"
export TELEGRAM_CHAT_ID="your-chat-id"
```

**Option 2:** Interactive prompt (script will ask)

**Disable:** `export TELEGRAM_DISABLE=true`

## Features

- ✅ Real-time build progress
- ✅ Single Telegram message that updates in-place
- ✅ Automatic GoFile upload with SHA256
- ✅ JSON-based device configs
- ✅ Non-blocking notifications
