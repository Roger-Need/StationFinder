# StationFinder ListBuilder v1.1

ListBuilder is a self-contained frequency list preparation tool for StationFinder. It runs entirely in any Chromium-based browser with no installation or dependencies. Load frequency list files from one or more sources, convert formats where needed, and save the files.  Optionally merge selected files into a single unified CSV file ready for use with StationFinder.

## Features

- **Multi-source schedule support**

- Loads and converts frequency schedule files from six sources:

  - **Aoki** — text-based schedule format distributed as a zip file. Frequently updated.

  - **EiBi** — semicolon-delimited CSV schedule format. Regular updates.

  - **HFCC** — zip-based format requiring a built-in two-step conversion before use.

  - **swskeds** — combined EiBi/Aoki/HFCC format distributed as a zip file. Semi-annual updates.

  - **ILGRadio** — paid subscription database distributed as a zip file. Requires a built-in conversion step. Two zip variants supported: full HF coverage (ilgaacsv.zip) and broadcast-focused (ilgbbcsv.zip).

  - **Custom** — import any CSV already in the 14-column StationFinder format.

- **Per-source download guidance**

  - Each source has a **Get file** button that opens a step-by-step modal explaining exactly where to download the schedule file and how to save it.

  - Direct links to each schedule provider are included in the modals.

- **Built-in conversion for HFCC and ILGRadio**

  - HFCC and ILGRadio zip files cannot be used directly and require conversion.

  - A two-step **Convert → Save** workflow within the modal handles this automatically.

  - Conversion status is shown inline; the Save button is enabled only after a successful conversion.

- **Merge & Save**

  - Any combination of imported sources can be merged into a single output file.

  - Merged rows are sorted numerically by frequency before saving.

  - Output is saved as a standard comma-delimited CSV named merged\_schedule.csv.

  - Uses the browser's File System Access API for save-to-disk with a file picker dialog.

- **Row count display**

  - A live count table shows how many rows are loaded from each source.

  - A running total updates as sources are imported or cleared.

- **Custom format support**

  - Accepts any CSV with a header row matching the 14-column StationFinder schema: Frequency, M, Station, On, Off, Language, Site, TX Country, Days, Target, Power, Azimuth, Origin, Source

  - Any row missing a Source value is automatically tagged as `Custom`.

- **Clear All**

  - Resets all loaded sources and counts in a single step with a confirmation prompt.

- **Status feedback**

  - A status box below the export controls reports progress, row counts, filenames, and errors in real time.

## Requirements

- A Chromium-based browser is required (Google Chrome, Microsoft Edge, Opera).

- Firefox and Safari are not supported — the File System Access API used for file picking and saving is not available in those browsers.

- No installation, no server, no internet connection required.

## Typical Workflow

1. **Open ListBuilder** in Chrome or Edge. Just double-click the file if one of these is your default browser.

2. For each frequency list source you want to use, click **Get file** to open the download instructions modal. Follow the steps to download and save the file from the provider's website.

3. For **HFCC** or **ILGRadio**, open the **Get file** modal and use the **Convert → Save** steps to produce a compatible CSV file.

4. **Import file** is an optional step if you want to create a merged file of several different sources.

5. Click **Import file** for each source to load the downloaded (or converted) file into ListBuilder.

6. Review the row counts in the count table to confirm each source loaded correctly.

7. Click **Merge & Save** to combine all loaded sources into a single frequency-sorted CSV file. Choose a save location when prompted.

8. Load the saved CSV into StationFinder using its **Import File** button.

## License

This program is free software: you can redistribute it and/or modify it under the terms of the **GNU General Public License** as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

You must:

- Keep the copyright and license header.

- Release any modifications or derivative works under GPLv3 (or later).

See [https://www.gnu.org/licenses/gpl-3.0.html](https://www.gnu.org/licenses/gpl-3.0.html) for the full license text.

