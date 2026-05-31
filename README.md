# StationFinder v3.0

StationFinder is a self-contained radio station database application. It runs entirely in a Chromium-based browser with no installation required. Load a frequency list file and search by frequency. Then filter by station name, mode, language, source, or on-air status. Optionally connect to SDRconnect via WebSocket or use CAT control to link to other SDR programs or a Kenwood or Icom rig. Once a connection is established the program will track the VFO frequency and display stations on that frequency. Click any row in the database table to tune the receiver to that frequency. In Range mode you can scan the band for active signals, step through stations one at a time, or hop automatically through a list of frequencies.

## Features

- **Schedule file import**

  - Loads station frequency lists in multiple formats (auto-detected on import):

    - **Aoki** — text based schedule format. Frequently updated.

    - **EiBi** — semicolon-delimited schedule format. Regular updates.

    - **HFCC** — a retrieval and conversion program is included in ListBuilder.

    - **swskeds** — combined EiBi/Aoki/HFCC format. Semi-annual updates.

    - **ILGRadio** — Requires a paid ILGRadio subscription. Converted using ListBuilder.

    - **s1b** — SDRplay format for memory files. Exported by SDRuno.

    - **SDR Console** — frequency database converted to CSV format.

  - All formats normalized to a common internal schema.

  - Columns that are empty in the loaded format are automatically hidden.

- **Frequency search**

  - Three search modes selectable via buttons:

    - **Exact** — matches frequencies within ±2 kHz of the entered value.

    - **Prefix** — shows all stations whose frequency starts with the typed digits.

    - **Range** — enter a range of interest in kHz (e.g. 9000-10000). Enables Scan, Step, and Hop.

  - Smart mode switching:

    - Typing a range (e.g. 9000-10000) in Exact mode automatically switches to Range mode.

    - Typing a single frequency in Range mode automatically switches to Exact mode.

    - Exact → Range pre-fills a ±150 kHz window around the current value.

    - Range → Exact uses the midpoint of the range.

  - Search timing displayed in a status indicator.

- **Band Selector**

  - Click **Band** to open the band selector modal.

  - Select any standard medium wave or shortwave broadcast band (MW, 120 m through 11 m).

  - Automatically sets the frequency search to that band's range, switches to Range mode, tunes the SDR to the band centre, and sets the sample rate to cover the full band.

- **Filtering**

  - **On Now** — filters to stations currently on air based on UTC time.

  - **Active** — available after a scan is stopped; filters to stations where a signal was detected.

  - **Mode filter** — dynamic drop-down built from the modes present in the loaded data.

  - **Language filter** — dynamic drop-down built from the loaded data. Includes grouping shortcuts (e.g. "English (all)").

  - **Source filter** — filter by schedule source (EiBi, Aoki, HFCC, ILGRadio etc.).

  - **Station name search** — substring search on the station name column. Press Enter to search.

- **Row detail modal**

  - **Ctrl-click any row** — opens a detail modal showing all available fields for that station.

  - For ILGRadio files, shows all 21 fields including extended data not visible in the table.

  - For other formats, shows the standard 14 fields.

  - **Frequency** — clickable links to sw-live and sw-info at that frequency.

  - **Station** — clickable search link to Google.

  - **Call sign** (ILG only) — clickable search links to Google and Perplexity AI.

  - **Additional info** (ILG only) — clickable search link to Google.

  - **Position of site** (ILG only) — decoded from DMS to decimal degrees with a clickable Google Maps link.

  - **Active** (ILG only) — decoded from single letter code to full description.

  - **Year** (ILG only) — decoded from YYMM code to Month/Year format.

- **Sortable table**

  - First 6 columns (Frequency, Mode, Station, On, Off, Language) are sortable by clicking the column header.

  - Sort state persists across searches.

  - Column headers show ↑, ↓, or ↑↓ arrows to indicate sort state.

- **Scan**

  - Available in Range mode with a WebSocket (SDRconnect) connection.

  - Click **Scan** to open the Pre-Scan Review panel before starting:

    - Displays a live FFT spectrum for the current frequency range, updated in real time.

    - A draggable search range bar overlaid on the spectrum — drag the centre to shift the range, drag the edges to adjust the limits.

    - Clickable tiles to adjust **sample rate**, **center frequency** (±100 kHz steps), and **SNR threshold** — left-click increases, right-click decreases.

    - Shows the number of database entries within the search range.

    - Checks that SDRconnect is in AM or SAM mode (required for scanning) and shows AM/SAM buttons to switch if needed.

  - Click **Start Scan** to begin. Stations where a signal is detected above the SNR threshold are highlighted in the table.

  - Click **Stop Scan** to halt — highlighted results remain visible.

  - Click **Clear** to reset all scan results and return to normal operation.

  - Scan is not available with CAT or CI-V serial connections.

- **Step**

  - Available in Range mode when the table has results and a connection is active.

  - **Left-click Step** — advances one row in the table and tunes the SDR to that frequency.

  - **Right-click Step** — steps back one row.

  - Starts from the row closest to the current VFO frequency, or the top of the table if the VFO is unknown or out of range.

  - Wraps at both ends of the table.

  - After a scan is stopped (Clear state), Step only walks through rows where a signal was detected, regardless of which filter is active.

- **Hop**

  - Automatically steps through frequencies one by one, sending each to the SDR after the selected dwell time.

  - Dwell time is selectable: 1, 2, 4, 6, 8, or 10 seconds.

  - In Range mode with no scan running, hops through all visible table rows in order.

  - After a scan is stopped (Clear state), hops only through frequencies where a signal was detected.

  - Click **Hop** to start, click **Stop Hop** to pause on the current frequency, and click **Hop** again to resume from the next frequency.

- **SDR WebSocket integration**

  - Connects to SDRplay program SDRconnect via WebSocket.

  - Default connection: 127.0.0.1 port 5454 (both configurable).

  - IP address field remembers previously entered addresses and shows them as a drop-down history.

- **SDR CAT Control**

  - **CAT (COM port)** — connects to SDR programs using Kenwood-style CAT commands over a virtual COM port. Works with SDRconnect, SDRuno, SDR Console and HDSDR.

  - **CAT (Icom rig)** — connects to Icom transceivers using CI-V protocol over a COM port. CI-V address and baud rate are user configurable.

  - Baud rate selectable from 1200 to 115200.

- **Flexible Search Capability**

  - **Manual** — type a frequency to search manually. Disconnects from SDR frequency tracking.

  - **Fetch** — one-shot read of the SDR VFO frequency into the search box.

  - **Track** — continuously follows the SDR VFO frequency and updates results.

  - **Click a row** — tunes the SDR to that station's frequency and mode.

  - **Web Search 1** — opens shortwave.live at the current search frequency.

  - **Web Search 2** — opens short-wave.info at the current search frequency.

- **Keyboard shortcuts**

  - **F or f** — jump to frequency search box.

  - **S or s** — jump to station search box.

  - **Enter** — run search and release focus.

  - **Escape** — release focus from search box, or close modal.

- **User Interface details**

  - Live UTC and local clock updated every second.

  - Status indicators showing loaded row count and search result count.

  - Signal strength and SNR pills displayed in the status bar during scan.

  - All controls disabled until a file is loaded, then enabled progressively.

  - Built-in help with button descriptions, keyboard shortcuts, and file format information.

## Requirements

- **Chromium-based browser required** — Google Chrome, Microsoft Edge, Brave or Opera. Firefox and Safari are not supported. The program will display a warning and disable all controls if run in an unsupported browser.

- No installation, no server, no internet connection required after initial setup.

- Will connect to SDRconnect running on the same machine or local network.

- Will connect over the WAN if router has port 5454 forwarding enabled.

- Virtual COM port pair required if using CAT mode (Com0Com or VSPE).

## Companion Program

**ListBuilder** (v1.1) is a companion program for retrieving, converting and merging schedule files from multiple sources into formats compatible with StationFinder. It supports Aoki, EiBi, HFCC, ILGRadio and swskeds sources. ListBuilder also requires a Chromium-based browser.

## Typical Workflow

1. **Open StationFinder** in your browser. Just double-click the file.

2. Click **Import File** and load a frequency schedule (Aoki, EiBi, HFCC, swskeds, ILGRadio, s1b or SDR Console format). Use ListBuilder to download and convert frequency list files.

3. Type a frequency in the **Search (Frequency)** box and press **Enter**.

4. Use **Range** mode to browse a range of frequencies, or click **Band** to select a standard shortwave or medium wave band.

5. Use **On Now** to filter to stations currently broadcasting.

6. Use the **Mode**, **Language** and **Source** drop-downs to narrow results further.

7. **Ctrl-click** any row to open the full detail modal for that station.

8. Optionally connect to your SDR program via **WebSocket** or **CAT**, then use **Fetch** or **Track** to follow the SDR VFO frequency automatically.

9. **Click** any row to tune the SDR program to that station.

10. In Range mode, click **Scan** to open the Pre-Scan Review panel, adjust settings, then click **Start Scan** to scan the band and highlight active stations.

11. Use **Step** or **Hop** to walk through stations — either all visible rows or, after a scan, only those where a signal was detected.

## License

This program is free software: you can redistribute it and/or modify it under the terms of the **GNU General Public License** as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

You must:

- Keep the copyright and license header.

- Release any modifications or derivative works under GPLv3 (or later).

See [https://www.gnu.org/licenses/gpl-3.0.html](https://www.gnu.org/licenses/gpl-3.0.html) for the full license text.

