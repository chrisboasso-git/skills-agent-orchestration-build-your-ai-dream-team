# Project Pulse dashboard plan

## Summary

The Project Pulse dashboard is a small static app that presents a contributor-friendly overview of active projects. It should use lightweight HTML, CSS, and JSON to provide clear project cards, status badges, owner labels, recent activity, priority cues, and a polished responsive layout.

The orchestrated workflow keeps design and implementation responsibilities separate: the Designer owns UX and styling, while the Coder owns the data shape and runnable-app support. The final outcome should resemble a polished dashboard and launch directly from the `app/` folder without showing a directory listing.

## Roles and responsibilities

### Designer

The Designer is responsible for:

- Layout and information hierarchy for the Project Pulse dashboard
- Semantic HTML structure in `app/index.html`
- Deterministic CSS hooks such as `.dashboard` and `.project-card`
- Status badge styling, priority emphasis, spacing, typography, and responsiveness
- Accessibility improvements such as contrast, readable text, clear labels, and keyboard-friendly interactions

### Coder

The Coder is responsible for:

- Defining and validating the `projects` data contract in `app/project-data.json`
- Creating the static rendering logic needed to parse and display project data
- Creating `.vscode/launch.json` with the VS Code launch configuration named `Run Project Pulse Dashboard`
- Ensuring the launch configuration uses `${workspaceFolder}/app` as `cwd` and opens `index.html`
- Validating that the app loads cleanly from the app directory

## Ordered implementation steps

1. **Confirm the dashboard contract**
   - Align on the required data fields: `name`, `owner`, `status`, `recentActivity`, and `priority`.
   - Confirm the expected design outcome from the brief and repository conventions.
   - The Coder defines the JSON schema; the Designer confirms that the UI can represent each field cleanly.

2. **Build the static structure in `app/index.html`**
   - Add a top-level dashboard shell with a header, summary area, and responsive card grid.
   - Create semantic project-card markup that can mirror the JSON data.
   - Include hook classes for CSS and predictable rendering order.
   - **Owner:** Designer.

3. **Implement styling in `app/styles.css`**
   - Add polished dashboard visuals: spacing, card shadows, border radius, typography, and status treatments.
   - Create card-level styling for owners, priorities, and activity indicators.
   - Ensure mobile and desktop responsiveness, with visible emphasis on risk or priority.
   - **Owner:** Designer.

4. **Create the project data in `app/project-data.json`**
   - Add a top-level `projects` array with the required object shape.
   - Keep content realistic and contributor-friendly, with clear status strings and recent activity.
   - **Owner:** Coder.

5. **Add runnable support in `.vscode/launch.json`**
   - Create the VS Code launch configuration that starts from the `app/` directory and opens `index.html`.
   - Ensure it is strict JSON and follows the Project Pulse requirement.
   - **Owner:** Coder.

6. **Validate end to end**
   - Load the app via the `Run Project Pulse Dashboard` configuration.
   - Confirm that the dashboard renders instead of a directory listing.
   - Check that each project card displays the expected information and layout.
   - Verify that JSON and HTML/CSS are internally consistent.
   - **Owners:** Coder and Designer jointly.

## File assignments

| File | Primary owner | Supporting responsibility |
|---|---|---|
| `app/index.html` | Designer | Coder reviews data-contract compatibility and confirms that the markup matches the expected JSON keys. |
| `app/styles.css` | Designer | Coder checks that styles do not interfere with app behavior and preserve accessibility. |
| `app/project-data.json` | Coder | Designer confirms that the structure supports the dashboard information hierarchy. |
| `.vscode/launch.json` | Coder | Designer verifies that launch behavior opens the intended dashboard surface. |

## Dependencies

- The JSON data contract must exist before the dashboard HTML is finalized because the UI content and card fields must match the data keys.
- CSS depends on the final HTML structure and class names; styling should be built after the layout is agreed.
- The launch configuration depends on the existence of `app/index.html` and the app folder structure; it should be created after the main page is in place.
- End-to-end validation depends on all four assigned files being present and internally consistent.

## Parallel work decisions

Parallel work is safe for these early-phase tasks:

- The Designer can draft the dashboard shell and styling in `app/index.html` and `app/styles.css` while the Coder prepares the `projects` data schema in `app/project-data.json`.
- The Coder can create `.vscode/launch.json` in parallel once the app entry point is known, as long as the launch target remains `app/index.html`.

Parallel work is constrained by the data contract:

- The Designer should not finalize card text or layout details that assume different JSON keys from the Coder's schema.
- The Coder should not finalize the launch configuration without confirming that the index file is the UI entry point.

Sequential execution is preferred for final integration:

- Reconcile HTML and CSS before launch validation.
- Check the data against the final card markup before final review.
- Run end-to-end validation only after all assigned files are present.

## Work that must run sequentially

- Finalize `app/project-data.json` before locking card-markup details.
- Finalize `app/index.html` before the final CSS pass.
- Create `.vscode/launch.json` after `app/index.html` exists and before runtime validation.
- Validate the app after all files are present; do not treat earlier partial checks as end-to-end verification.

## Edge cases

- Missing or malformed `projects` data should fail clearly rather than rendering a blank or broken dashboard.
- HTML should be resilient to zero or unusually short project lists.
- Long `recentActivity` strings should not break the layout or overflow cards.
- Status values should remain deterministic so styling stays consistent across cards.
- The launch configuration must never target the parent directory; it should explicitly open `index.html` from the `app/` folder.

## Validation expectations

The implementation is complete when:

- `app/index.html` renders a dashboard-like page with project cards.
- `app/styles.css` includes deterministic hooks such as `.dashboard` and `.project-card`.
- `app/project-data.json` contains a valid top-level `projects` array with the required fields.
- `.vscode/launch.json` exists, has valid JSON, and opens `index.html` from `${workspaceFolder}/app`.
- Running the VS Code launch configuration opens the dashboard instead of a directory listing.
- The layout is readable and responsive across common desktop and narrow mobile widths.

Validation should include:

- JSON parsing of `app/project-data.json`.
- Strict JSON parsing of `.vscode/launch.json`.
- A consistency check between the data fields and rendered card markup.
- A browser or VS Code launch smoke test.
- Visual checks at desktop and narrow mobile widths, including status, priority, owner, and activity readability.

## Open questions

- Are there branding preferences or naming conventions for project names and status labels beyond the brief?
- Should project priority be represented as text, color, or both in the final dashboard?
- Is a small amount of JavaScript acceptable for rendering the JSON into cards, or should the page use static markup only?
