# VPINHUB Tournament Helper

> A lightweight, single-page web application designed to help virtual pinball tournament organizers and players quickly find and share information about specific table releases. This tool serves as a fast, searchable front-end for the extensive Virtual Pinball Spreadsheet (VPS) database, with the intention of supporting the VPINHUB competition page tournaments.

➡️ **Live Application Link:** [https://vpinhub.github.io/tournamenthelper/](https://vpinhub.github.io/tournamenthelper/)

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
-   **Dynamic Tournament Cards**: Automatically displays rules, date ranges, and submission links for specific weekly competitions (`?swl`, `&ttd`, `&vpc`) when added to a Tournament View URL.
-   **Fully Dynamic Tournament View**: Add custom notes, unlisted ROMs, and unlisted B2S files directly via URL parameters, and hide non-essential files to create a clean, focused tournament page.

---

## Tournament Helper URL Parameters

The power of this tool comes from its ability to generate and interpret custom URLs. You can create these manually to build tournament pages with specific, and even unlisted, files. Remember, the first parameter uses `?` and all subsequent parameters use `&`.

1.  **Open a Specific Table Modal**
    -   Opens the modal view for a specific table on the main page.
    -   **Structure**: `?tableId=[TABLE_ID]`
    -   **Example**: `.../?tableId=sHyAt2jR` (Opens the modal for Jungle Princess)

2.  **Open the Tournament View for a Specific Release**
    -   Displays the dedicated "Tournament View" page for a single table file, along with all its related assets.
    -   **Structure**: `?tableId=[TABLE_ID]&releaseId=[RELEASE_ID]`
    -   **Example**: `.../?tableId=sHyAt2jR&releaseId=RZnU4RRXxJ`

3.  **Display a Tournament Information Card**
    -   Add a special information card to the top of any Tournament View. The card automatically calculates the current event period and displays specific rules and links.
    -   Supported competitions: `&swl` (Special When Lit), `&ttd` (Thursday Throw Down), `&vpc` (VPC Competition Corner).
    -   **Structure**: `?[TABLE_PARAMS]&[TOURNAMENT_FLAG]`
    -   **Example**: `.../?tableId=sHyAt2jR&releaseId=RZnU4RRXxJ&swl`

4.  **Use an Unlisted Table**
    -   For tournaments using a table version not in the VPS database, you can replace the main table file with your own custom link.
    -   **Structure**: `?tableId=[TABLE_ID]&unlistedtable=[TABLE_URL]&author=[AUTHOR_NAME]`
    -   **Example**: `.../?tableId=QDWTicJY&unlistedtable=.../unlisted.vpx&author=VPW`

5.  **Add a Custom ROM**
    -   Dynamically add a "Tournament Table Rom" card with a custom download link and author.
    -   **Structure**: `...&rom=[ROM_URL]&rauthor=[AUTHOR_NAME]`
    -   **Example**: `...&rom=https://.../cactjack.zip&rauthor=Community`
    -   **Note**: Use underscores `_` for spaces in author names (e.g., `&rauthor=John_Doe`).

6.  **Add a Custom B2S Backglass**
    -   Dynamically add a "Tournament B2S" card with a custom download link and author.
    -   **Structure**: `...&b2s=[B2S_URL]&b2sauthor=[AUTHOR_NAME]`
    -   **Example**: `...&b2s=https://.../cactjack.directb2s&b2sauthor=Rawd`

7.  **Add Custom Notes**
    -   Display important information for players. Notes support underscores `_` for spaces.
    -   **`&tnotes`**: A general note displayed in a prominent banner at the top of the view.
    -   **`&rnotes`**: A note attached specifically to the custom ROM card (requires `&rom=` to be present).
    -   **Structure**: `...&tnotes=[NOTE_TEXT]&rom=...&rnotes=[ROM_NOTE_TEXT]`
    -   **Example**: `...&tnotes=Please_use_5-ball_settings.&rom=...&rnotes=Use_v1.6_of_this_ROM`

8.  **Hide Non-Essential Files**
    -   Cleans up the Tournament View by hiding all database-listed files except for the primary Table and ROM files.
    -   **Note**: This will *not* hide custom files added via `&b2s=` or `&rom=`.
    -   **Structure**: `...&hide`
    -   **Example**: `.../?tableId=QDWTicJY&releaseId=d53_5NH4ne&hide`

### Full Example

You can combine these parameters to create a highly specific tournament page.

**URL:**
`?tableId=QDWTicJY&releaseId=d53_5NH4ne&swl&rom=URL_HERE&rauthor=JP_Salas&b2s=URL_HERE&b2sauthor=Rawd&tnotes=Welcome_to_the_tournament!&hide`

**This URL will generate a page that:**
-   Is for the table "Cactus Canyon (Remake)".
-   Displays the "Special When Lit" tournament info card.
-   Includes a custom ROM link with "JP Salas" as the author.
-   Includes a custom B2S link with "Rawd" as the author.
-   Shows a prominent note saying "Welcome to the tournament!".
-   Hides all other files (POVs, PUP-Packs, etc.) listed in the database.

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
