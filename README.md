# VPINHUB Tournament Helper

> A lightweight, single-page web application designed to help virtual pinball tournament organizers and players quickly find and share information about specific table releases. This tool serves as a fast, searchable front-end for the extensive Virtual Pinball Spreadsheet (VPS) database, with the intention of supporting the VPINHUB competition page tournaments.

➡️ **Live Application Link:** [https://vpinhub.github.io/vpinhubtournamenthelper/](https://vpinhub.github.io/vpinhubtournamenthelper/)

---

## Acknowledgments

This tool would not be possible without the incredible work of the entire community behind the Virtual Pinball Spreadsheet. The data is sourced directly from their public database.

## Features

-   **Live Search**: Instantly filter thousands of tables by name, manufacturer, author, or theme.
-   **Infinite Scroll**: Smoothly browse the entire database without pagination.
-   **Detailed Modal View**: Click any table to see a pop-up with all associated files, including backglasses, ROMs, PUP-Packs, alternate sounds/colors, and tutorials.
-   **Direct Linking**: Share a link that opens directly to a specific table's modal view.
-   **iScored VPinStudio Tag**: Quickly generate and copy a URL tag for use in iScored tournaments.
-   **Tournament View**: A dedicated, shareable "full-page" view for a single table release, perfect for tournament instructions.

---

## Tournament Helper URL Parameters

The power of this tool comes from its ability to generate and interpret custom URLs. You can create these manually to build tournament pages with specific, and even unlisted, files.

1.  **Open a Specific Table Modal**
    -   Opens the modal view for a specific table on the main page.
    -   **Structure**: `?tableId=[TABLE_ID]`
    -   **Example**: `.../?tableId=sHyAt2jR` (Opens the modal for Jungle Princess)

2.  **Open the Tournament View for a Specific Release**
    -   Displays the dedicated "Tournament View" page for a single table file, along with all its related assets.
    -   **Structure**: `?tableId=[TABLE_ID]&releaseId=[RELEASE_ID]`
    -   **Example**: `.../?tableId=sHyAt2jR&releaseId=RZnU4RRXxJ`

3.  **Add a Custom ROM to the Tournament View**
    -   For tables where the required ROM is not listed, you can dynamically add a "Tournament Table Rom" card with a custom download link.
    -   **Structure**: `?tableId=[TABLE_ID]&releaseId=[RELEASE_ID]&rom=[ROM_URL]`
    -   **Example**: `.../?tableId=QDWTicJY&releaseId=d53_5NH4ne&rom=https://.../cactjack.1644/`

4.  **Use an Unlisted Table in the Tournament View**
    -   For tournaments using a table version that is not in the VPS database, you can create a Tournament View that replaces the main table file with your own custom link.
    -   **Structure**: `?tableId=[TABLE_ID]&unlistedtable=[TABLE_URL]`
    -   **Example**: `.../?tableId=QDWTicJY&unlistedtable=https://.../unlisted_canyon.vpx`
    -   **Note**: The `&rom=` parameter can also be combined with the `&unlistedtable=` parameter.

---

## Technology

This project is built as a self-contained, single `index.html` file with:

-   **Vanilla JavaScript**: For all logic, data fetching, and DOM manipulation.
-   **Tailwind CSS**: For styling, loaded via CDN.
-   **VPS DB**: Fetches the latest pinball database directly from the official VPS GitHub repository.

---

## Running Locally

1.  Download the `index.html` file.
2.  Because the page fetches data from a remote URL, you must serve it from a local web server to avoid CORS security errors. The easiest way is to use Python's built-in server:

```bash
# Navigate to the folder containing index.html in your terminal
cd /path/to/your/project

# Run the server
python -m http.server
