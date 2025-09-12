You are a prompt engineer for a designer. Create a highly detailed and actionable design brief for a generative AI design tool (e.g., Figma AI) to create wireframes and a style guide for a macOS menubar application.

**App Concept:** "AltGenie" - an AI-powered alternatives generator.
**Platform:** macOS Menubar App (with a strong focus on native macOS design aesthetics, implicitly supporting both light and dark modes).
**Core Functionality:** Users input the name of an app, service, or website. The app leverages AI to find and return a list of alternative suggestions, each with a brief description and a direct URL.

**Instructions for the Generative AI Design Tool:**

1.  **Define a Color Palette:**
    *   Create a modern, clean, and professional color palette suitable for a macOS menubar utility application. The palette should evoke efficiency, intelligence, and trustworthiness, while being unobtrusive and integrating well with the macOS environment.
    *   **Primary Color:** A dominant color for branding and key interactive elements (e.g., a subtle blue, a dark teal, or a sophisticated grey).
    *   **Secondary Color:** A complementary color, used for less prominent interactive elements or background accents.
    *   **Accent Color:** A vibrant, yet tasteful, color for call-to-action buttons, highlights, and status indicators. This color should provide clear visual feedback without being overwhelming.
    *   **Neutral Colors:** A comprehensive range of light, medium, and dark grays, along with pure white and deep black, for backgrounds, text, borders, and shadows, ensuring optimal contrast in both light and dark modes.

2.  **Choose Typography:**
    *   Select a typography system that prioritizes legibility, clarity, and aligns with modern macOS design principles. The system should feel native to macOS (e.g., SF Pro Display/Text equivalents, if not directly available).
    *   **Headings Font:** A clean, contemporary sans-serif font suitable for titles, subtitles, and important labels. Define sizes and weights for `H1` (main title), `H2` (section titles), and `H3` (sub-headings/card titles).
    *   **Body Text Font:** A highly readable sans-serif font for general text, descriptions, and smaller UI elements. Define sizes and weights for `Body` (main text), `Small Text` (metadata, helper text), and `Button Text`.

3.  **Design a Logo Concept:**
    *   Develop 2-3 distinct, minimalist, and memorable logo concepts for the "AltGenie" application.
    *   The logo must be highly effective as a small menubar icon (e.g., 18x18px, 36x36px @2x), representing the core concept of discovery, intelligence, connection, or smart alternatives.
    *   Consider abstract shapes, subtle gradients, and iconographic elements that convey "search," "switch," or "alternatives." Ensure it looks good in both light and dark modes.

4.  **Wireframe the 4 Most Critical Application Screens:**
    *   For each screen, provide a detailed layout, identify key UI components, and describe the user flow. Ensure all designs respect the compact nature and interaction patterns of a macOS menubar popover window.

    *   **Screen 1: Main Search/Input View**
        *   **Purpose:** The initial view presented when the user clicks the menubar icon, allowing them to input a query.
        *   **Layout:** A compact, clean window. Centrally placed, prominent input field. Perhaps a subtle app title/icon at the top for branding.
        *   **Key UI Components:**
            *   **Search Input Field:** A `NSTextField` (or equivalent) with a clear placeholder (e.g., "Enter app, service, or website name...").
            *   **Clear Input Button:** A small 'x' button within or beside the input field to clear the text.
            *   **Implicit Search Trigger:** Hitting 'Enter' after typing should initiate the search.
        *   **User Flow:** User clicks menubar icon -> AltGenie window appears -> User types query into the input field -> User presses Enter.

    *   **Screen 2: Loading/Processing View**
        *   **Purpose:** To inform the user that their query is being processed by the AI.
        *   **Layout:** A minimalist view, centered within the application window.
        *   **Key UI Components:**
            *   **Progress Indicator:** A standard macOS `NSProgressIndicator` (spinner) or a subtle progress animation.
            *   **Status Message:** Text below the spinner, e.g., "Searching for alternatives...", "AltGenie is thinking...".
        *   **User Flow:** After the user submits a query from the "Main Search/Input View", this screen briefly appears while AI processes.

    *   **Screen 3: Alternatives Results List View**
        *   **Purpose:** To display the AI-generated list of alternatives with their details.
        *   **Layout:** A scrollable list of individual "alternative cards" or "rows". Each item should be concise but informative. The overall window should maintain a compact width but allow for vertical scrolling.
        *   **Key UI Components (for each alternative item):**
            *   **Alternative Name:** Prominent `NSTextField` for the name of the alternative.
            *   **Brief Description:** `NSTextField` for a short, AI-generated summary of the alternative.
            *   **Visit Website Button/Link:** A clear `NSButton` or hyperlink (`NSLink`) to open the alternative's URL in the default browser. Consider a small external link icon.
            *   **Copy URL Button (Optional):** A small button to quickly copy the URL to the clipboard.
        *   **User Flow:** After the AI processes, this screen replaces the loading view -> User sees a list of alternatives -> User can click "Visit Website" to open the URL or scroll through the list.

    *   **Screen 4: Empty State / Error State View**
        *   **Purpose:** To gracefully handle scenarios where no alternatives are found or an error occurs (e.g., network issues, AI processing failure).
        *   **Layout:** A centered message and an icon to clearly convey the status.
        *   **Key UI Components:**
            *   **Informative Icon:** A relevant macOS SF Symbol (or equivalent) indicating no results (e.g., `magnifyingglass.slash`) or an error (e.g., `exclamationmark.triangle`).
            *   **Status Message:** A clear `NSTextField` message, e.g., "No alternatives found for that query. Try something else!", or "Oops! Something went wrong. Please try again later."
            *   **Action Button:** An `NSButton` for relevant actions, such as "Try Again" (for errors) or "Go Back to Search" (for empty results).
        *   **User Flow:** If AI returns no results or an error occurs during processing, this screen appears instead of the "Alternatives Results List View". User can then retry or return to the main search.