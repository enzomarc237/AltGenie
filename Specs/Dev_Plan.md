This project plan outlines the development of an "Alternatives Generator" macOS menubar app using Flutter, leveraging `macos_ui` for a native look and feel. Each phase includes a detailed, actionable prompt designed for an AI pair programmer.

### Project Plan
- **Phase 1: Project Setup & Core Dependencies**
- **Phase 2: Menubar Integration & Basic UI Shell**
- **Phase 3: AI Service Integration & Data Model**
- **Phase 4: Core Logic & State Management**
- **Phase 5: UI/UX Enhancements & Interaction**
- **Phase 6: Testing, Error Handling & Deployment**

### Phase 1: Project Setup & Core Dependencies Prompt
```
Initialize a new Flutter project named `alternatives_generator_app` with macOS as a target platform. Add the following core dependencies to `pubspec.yaml`: `macos_ui` (for native macOS widgets), `system_tray` (for menubar integration), `http` (for API calls), `url_launcher` (for opening URLs), and `flutter_dotenv` (for environment variable management). Set up a basic folder structure within `lib/src/`: `features`, `services`, `widgets`, `models`, and `utils`. Ensure the macOS runner has network access permissions configured.
```

### Phase 2: Menubar Integration & Basic UI Shell Prompt
```
Implement `system_tray` to create a menubar icon for the `alternatives_generator_app`. Configure this menubar icon to toggle the visibility of the main application window when clicked. Design the initial UI for this pop-up window using `macos_ui` widgets: include a `MacosTextField` for user input, a `MacosButton` labeled "Generate Alternatives" to trigger the search, and a `MacosScrollable` area (e.g., a `ListView.builder` wrapped in `MacosScrollable`) to display results. The window should be compact, borderless, and appear near the menubar.
```

### Phase 3: AI Service Integration & Data Model Prompt
```
Create a `lib/src/services/ai_service.dart` file. Implement a `fetchAlternatives(String query)` asynchronous method within this service. This method should make an HTTP POST request to an AI API (e.g., OpenAI's Chat Completions API) with the user's `query`. Design the AI prompt to request "alternatives to [query] with a brief description and a URL for each, presented in a structured, easily parsable format like JSON or markdown list." Integrate `flutter_dotenv` to securely manage the AI API key via environment variables. Define a `lib/src/models/alternative.dart` data model with fields like `name` (String), `description` (String), and `url` (String) to represent a single alternative. Implement basic parsing of the AI's response into a list of `Alternative` objects.
```

### Phase 4: Core Logic & State Management Prompt
```
Implement the core application logic in `lib/src/features/alternatives_generator/alternatives_generator_view.dart` and an associated state management solution (e.g., `flutter_riverpod` or `provider`). The state should manage: the current user input string, a boolean `isLoading` flag, a `List<Alternative>` for results, and an optional `String? errorMessage`. Connect the UI components (input field, search button) to trigger state updates and call the `AiService.fetchAlternatives` method. Update the UI dynamically based on the current state: show a `MacosProgressCircle` when loading, display the list of alternatives upon success, or show a `MacosText` error message on failure or no results.
```

### Phase 5: UI/UX Enhancements & Interaction Prompt
```
Refine the display of the alternatives list. Each `Alternative` should be presented as a `MacosListTile` or a custom `MacosCard`-like widget, clearly showing its `name`, `description`. Make the `url` field clickable using `url_launcher` to open in the user's default web browser. Implement visual feedback for various app states: a clear "Enter an app/service name to find alternatives" message for the initial empty state, a "No alternatives found for your query" message if the AI returns no results, and smooth transitions/animations for loading and result display. Add basic input validation to prevent empty queries.
```

### Phase 6: Testing, Error Handling & Deployment Prompt
```
Write unit tests for the `AiService`'s `fetchAlternatives` method, mocking HTTP responses for success, parsing errors, and network failures. Implement widget tests for the `AlternativesGeneratorView` to verify correct behavior across loading, success (with various alternatives), and error states. Enhance error handling throughout the app, providing user-friendly `MacosAlertDialog` messages for issues like network connectivity problems, API rate limits, or AI response parsing errors. Add a simple "About" menu item to the `system_tray` context menu showing the app version. Provide clear instructions and commands for building and packaging the Flutter macOS app for distribution.