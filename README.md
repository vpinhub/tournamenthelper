# VPINHUB Tournament Helper

> A lightweight, single-page web application designed to help virtual pinball tournament organizers and players quickly find and share information about specific table releases. This tool serves as a fast, searchable front-end for the extensive Virtual Pinball Spreadsheet (VPS) database, with the intention of supporting the VPINHUB competition page tournaments.

➡️ **Live Application Link:** [https://vpinhub.github.io/tournamenthelper/](https://vpinhub.github.io/tournamenthelper/)

---

## Acknowledgments

This tool would not be possible without the incredible work of the entire community behind the Virtual Pinball Spreadsheet. The data is sourced directly from their public database.

---

## Features

-   **Live Search**: Instantly filter thousands of tables by name, manufacturer, author, or theme.
-   **Infinite Scroll**: Smoothly browse the entire database without pagination.
-   **Detailed Modal View**: Click any table to see a pop-up with all associated files, including backglasses, ROMs, PUP-Packs, alternate sounds/colors, and tutorials.
-   **Direct Linking**: Share a link that opens directly to a specific table's modal view.
-   **iScored VPinStudio Tag**: Quickly generate and copy a URL tag for use in iScored tournaments.
-   **Tournament View**: A dedicated, shareable "full-page" view for a single table release, perfect for tournament instructions.
-   **Dynamic Tournament Cards**: Automatically displays rules, date ranges, and submission links for specific weekly competitions (`?swl`, `&ttd`, `&vpc`) when added to a Tournament View URL.
-   **Pinball FX/FX3 Support**: Dedicated tournament cards and layouts for **Pinball FX** (`&fx`) and **Pinball FX3** (`&fx3`) tournaments, which automatically hide irrelevant files like ROMs and downloads.
-   **Fully Dynamic Tournament View**: Add custom notes, unlisted files, and hide non-essential files to create a clean, focused tournament page.
-   **Deep Customization via URL**: Override table/ROM features and even the main preview image for a fully tailored tournament page.
-   **QR Code Generation**: Add `&qrcode` to any URL to display a large QR code at the bottom of the page, perfect for sharing on streams or in person.

---

## Tournament Helper URL Parameters

The power of this tool comes from its ability to generate and interpret custom URLs. You can create these manually to build tournament pages with specific, and even unlisted, files. Remember, the first parameter uses `?` and all subsequent parameters use `&`.

### General & VPX Parameters

1.  **Open a Specific Table Modal**
    * Opens the modal view for a specific table on the main page.
    * **Structure**: `?tableId=[TABLE_ID]`
    * **Example**: `.../?tableId=sHyAt2jR` (Opens the modal for Jungle Princess)

2.  **Open the Tournament View for a Specific Release**
    * Displays the dedicated "Tournament View" page for a single table file, along with all its related assets.
    * **Structure**: `?tableId=[TABLE_ID]&releaseId=[RELEASE_ID]`
    * **Example**: `.../?tableId=sHyAt2jR&releaseId=RZnU4RRXxJ`

3.  **Display a VPX Tournament Information Card**
    * Add a special information card to the top of any Tournament View. The card automatically calculates the current event period and displays specific rules and links.
    * Supported competitions: `&swl` (Special When Lit), `&ttd` (Thursday Throw Down), `&vpc` (VPC Competition Corner).
    * **Structure**: `?[TABLE_PARAMS]&[TOURNAMENT_FLAG]`
    * **Example**: `.../?tableId=sHyAt2jR&releaseId=RZnU4RRXxJ&swl`

4.  **Use an Unlisted Table**
    * For tournaments using a table version not in the VPS database, you can replace the main table file with your own custom link.
    * **Structure**: `?tableId=[TABLE_ID]&unlistedtable=[TABLE_URL]&author=[AUTHOR_NAME]`
    * **Example**: `.../?tableId=QDWTicJY&unlistedtable=.../unlisted.vpx&author=VPW`

5.  **Add a Custom ROM**
    * Dynamically add a "Tournament Table Rom" card with a custom download link and author.
    * **Structure**: `...&rom=[ROM_URL]&rauthor=[AUTHOR_NAME]`
    * **Example**: `...&rom=https://.../cactjack.zip&rauthor=Community`
    * **Note**: Use underscores `_` for spaces in author names (e.g., `&rauthor=John_Doe`).

6.  **Add a Custom B2S Backglass**
    * Dynamically add a "Tournament B2S" card with a custom download link and author.
    * **Structure**: `...&b2s=[B2S_URL]&b2sauthor=[AUTHOR_NAME]`
    * **Example**: `...&b2s=https://.../cactjack.directb2s&b2sauthor=Rawd`

7.  **Add Custom Notes**
    * Display important information for players. Notes support underscores `_` for spaces.
    * **`&tnotes`**: A general note displayed in a prominent banner at the top of the view.
    * **`&rnotes`**: A note attached specifically to the custom ROM card (requires `&rom=` to be present).
    * **Structure**: `...&tnotes=[NOTE_TEXT]&rom=...&rnotes=[ROM_NOTE_TEXT]`
    * **Example**: `...&tnotes=Please_use_5-ball_settings.&rom=...&rnotes=Use_v1.6_of_this_ROM`

8.  **Add Custom Features**
    * Adds a "Features" line to an unlisted table or a custom ROM. Use commas `,` to separate multiple features and underscores `_` for spaces.
    * **`&tfeatures`**: For unlisted tables (requires `&unlistedtable=`).
    * **`&rfeatures`**: For custom ROMs (requires `&rom=`).
    * **Structure**: `...&unlistedtable=[URL]&tfeatures=[FEATURE_1,FEATURE_2]`
    * **Example**: `...&rom=...&rfeatures=Colorized_DMD,Custom_Music`

9.  **Override the Preview Image**
    * Sets a custom header image for the Tournament View, overriding the default image from the database.
    * **Structure**: `...&img=[IMAGE_URL]`
    * **Example**: `...&img=https://i.imgur.com/your-image.jpeg`

10. **Hide Non-Essential Files**
    * Cleans up the Tournament View by hiding all database-listed files except for the primary Table and ROM files.
    * **Note**: This will *not* hide custom files added via `&b2s=` or `&rom=`.
    * **Structure**: `...&hide`
    * **Example**: `.../?tableId=QDWTicJY&releaseId=d53_5NH4ne&hide`

---

### Pinball FX / FX3 Tournament Parameters

You can also create tournament pages for Pinball FX and FX3. These flags will automatically re-skin the page for an FX-style event.

1.  **Display Pinball FX / FX3 Tournament Card**
    * Adds a dedicated "VPINHUB Pinball FX Tournament" (or FX3) card.
    * Automatically re-labels the main table file to "Tournament Pinball Table" and hides its download button.
    * Automatically hides all ROMs and most other files, *except* for "Tutorial Documents" and any B2S files authored by "DDH69".
    * **Structure**: `...&fx` or `...&fx3`
    * **Example**: `.../?tableId=sHyAt2jR&releaseId=RZnU4RRXxJ&fx`

2.  **Add FX Tournament Details**
    * These parameters add specific details to the `&fx` or `&fx3` tournament card.
    * **`&fxcode`**: Displays a "Tournament Code" with a copy button.
    * **`&fxhost`**: Adds a "Table Host:" line to the rules.
    * **`&fxpassword`**: Adds a "Tournament Password:" line to the rules.
    * **Structure**: `...&fx&fxcode=[CODE]&fxhost=[HOST_NAME]&fxpassword=[PASSWORD]`
    * **Example**: `...&fx3&fxcode=VPINHUB&fxhost=Rawd&fxpassword=pinball`

---

### Utility Parameters

1.  **Generate a QR Code**
    * Displays a large QR code at the bottom of the page pointing to the current URL (minus the `&qrcode` parameter itself).
    * **Structure**: `...&qrcode`
    * **Example**: `.../?tableId=sHyAt2jR&releaseId=RZnU4RRXxJ&swl&qrcode`

---

### Full Example (VPX)

You can combine these parameters to create a highly specific VPX tournament page.

**URL:**
`?tableId=QDWTicJY&unlistedtable=URL_HERE&author=VPW&swl&rom=URL_HERE&rfeatures=Colorized_DMD&tnotes=Welcome!&hide&img=https://i.imgur.com/your-image.jpeg`

**This URL will generate a page that:**
-   Is based on the "Cactus Canyon (Remake)" entry.
-   Uses a custom, **unlisted table file** by "VPW".
-   Displays the **"Special When Lit"** tournament info card.
-   Includes a custom ROM link with the feature **"Colorized DMD"**.
-   Shows a prominent note saying **"Welcome!"**.
-   Uses a **custom preview image** at the top.
-   **Hides** all other files (POVs, PUP-Packs, etc.) listed in the database.

### Full Example (Pinball FX3)

**URL:**
`?tableId=LkyZJm-E&releaseId=9z-5uT1TfK&fx3&fxcode=VPIN-FALL&fxhost=Tournament_Admin&fxpassword=top_score&tnotes=Good_luck_players!&qrcode`

**This URL will generate a page that:**
-   Is based on the "Star Wars: A New Hope" entry.
-   Displays the **"VPINHUB Pinball FX3 Tournament"** card.
-   Includes the tournament code **"VPIN-FALL"**, host **"Tournament_Admin"**, and password **"top_score"**.
-   Shows a prominent note saying **"Good luck players!"**.
-   **Hides** all irrelevant files (ROMs, etc.) automatically.
-   Displays a **QR code** at the bottom for easy sharing.

---

## Technology

This project is built as a self-contained, single `index.html` file with:

-   **Vanilla JavaScript**: For all logic, data fetching, and DOM manipulation.
-   **Tailwind CSS**: For styling, loaded via CDN.
-   **QRCode.js**: For generating QR codes, loaded via CDN.
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
