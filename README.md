# companion-module-sermon-helper

Bitfocus Companion module for controlling Broadlink IR/RF devices and PowerPoint presentations through the Sermon Helper application.

## Installation

### From Release

1. Download the latest `.tar.gz` from [Releases](../../releases)
2. Extract it into your Companion modules folder
3. Restart Companion

### For Development

1. Create a `companion-module-dev` folder on your system
2. Clone or copy this module into that folder
3. In Companion settings, set the developer modules path to your `companion-module-dev` folder
4. Run `npm install` and `npm run build` in this module's directory
5. Restart Companion

### Building

```bash
npm install
npm run build
```

### Development Mode

```bash
npm run dev
```

This will watch for changes and recompile automatically.

## Configuration

| Option | Description | Default |
|--------|-------------|---------|
| **Host** | IP address or hostname of the Sermon Helper server | `localhost` |
| **Port** | Discovery Server API port | `8765` |
| **Auth Token** | Optional authentication token | |
| **Poll Interval** | How often to refresh command list (seconds) | `30` |

## Actions

### RF/IR Commands

| Action | Description |
|--------|-------------|
| Execute RF/IR Command | Execute a saved command by slug |
| Execute Command by Category | Execute a command filtered by category (Projector, Screen, HVAC, Lighting, Audio, Other) |
| Refresh Command List | Manually refresh the list of available commands from the server |

### PPT File Selector

| Action | Description |
|--------|-------------|
| PPT: Type Digit | Append a digit (0-9) to the file filter for numeric lookup |
| PPT: Backspace | Remove the last digit from the filter |
| PPT: Clear Filter | Clear the file filter completely |
| PPT: Select File | Open the PPT file at a specific display slot (1-5), optionally starting presenter mode |
| PPT: Select Folder | Switch to a different PPT folder |
| PPT: Refresh Files | Refresh the list of PPT files from the current folder |

### Presentation Control

| Action | Description |
|--------|-------------|
| Presentation: Open File | Open a presentation file by path, optionally starting presenter mode |
| Presentation: Start Slideshow | Start the slideshow from the beginning or a specific slide |
| Presentation: Stop Slideshow | Stop the currently running slideshow |
| Presentation: Next Slide | Go to the next slide or animation step |
| Presentation: Previous Slide | Go to the previous slide |
| Presentation: Go to Slide | Jump to a specific slide number |
| Presentation: First Slide | Go to the first slide |
| Presentation: Last Slide | Go to the last slide |
| Presentation: Toggle Blank Screen | Toggle black screen on/off during slideshow |
| Presentation: Close All | Close all open presentation files |
| Presentation: Close Latest | Close the most recently opened presentation file |

## Feedbacks

| Feedback | Description |
|----------|-------------|
| Connection Status | Shows whether connected to the Sermon Helper server |
| Command Available | Shows if a specific RF/IR command is available |
| PPT: Slot Has File | Shows if a PPT slot has a file available |
| PPT: Filter Active | Shows if a PPT filter is currently applied |
| Presentation: Slideshow Active | Shows if a slideshow is currently running |
| Presentation: Screen Blanked | Shows if the presentation screen is blanked |

## Variables

| Variable | Description |
|----------|-------------|
| `connection_status` | Connected / Disconnected |
| `last_command` | Last executed RF/IR command name |
| `command_count` | Total number of available commands |
| `server_host` | Configured server host |
| `server_port` | Configured server port |
| `ppt_filter` | Current PPT numeric filter |
| `ppt_match_count` | Number of files matching the current filter |
| `ppt_folder_name` | Name of the currently selected PPT folder |
| `ppt_slot_1_name` .. `ppt_slot_5_name` | File names in PPT display slots 1-5 |
| `ppt_last_opened` | Last opened PPT file name |
| `ppt_current_slide` | Current slide number |
| `ppt_total_slides` | Total number of slides |
| `ppt_slideshow_active` | ON / OFF |
| `ppt_app` | Presentation application name |
| `ppt_blanked` | YES / NO |

## Presets

The module includes ready-to-use button presets:

- **Status** - Connection status indicator with refresh action
- **RF/IR Commands** - Auto-generated button for each saved command, color-coded by category
- **PPT Selector** - Numeric digit pad (0-9), backspace, clear, refresh, 5 file slot buttons, filter status display, and folder display
- **Presentation Control** - Play, stop, next, previous, first, last, go to slide, blank toggle, open, close, close latest, and slide status display

## Requirements

- Sermon Helper desktop application running with Discovery Server enabled
- Broadlink devices configured in Sermon Helper (for RF/IR control)
- PowerPoint or compatible presentation software (for presentation control)

## API Endpoints Used

### RF/IR
- `GET /api/v1/health` - Connection health check
- `GET /api/v1/rfir/commands` - List all commands
- `POST /api/v1/rfir/commands/:slug/execute` - Execute a command

### PPT File Management
- `GET /api/v1/ppt/folders` - List PPT folders
- `GET /api/v1/ppt/files` - List PPT files (with folder/filter params)
- `POST /api/v1/ppt/open` - Open a PPT file

### Presentation Control
- `POST /api/v1/presentation/open` - Open a presentation file
- `POST /api/v1/presentation/start` - Start slideshow
- `POST /api/v1/presentation/stop` - Stop slideshow
- `POST /api/v1/presentation/close` - Close all presentations
- `POST /api/v1/presentation/close-latest` - Close latest presentation
- `POST /api/v1/presentation/next` - Next slide
- `POST /api/v1/presentation/previous` - Previous slide
- `POST /api/v1/presentation/goto` - Go to specific slide
- `POST /api/v1/presentation/first` - First slide
- `POST /api/v1/presentation/last` - Last slide
- `POST /api/v1/presentation/blank` - Blank screen
- `POST /api/v1/presentation/unblank` - Unblank screen
- `GET /api/v1/presentation/status` - Get presentation status
- `WS /ws` - Real-time status updates

## License

MIT
