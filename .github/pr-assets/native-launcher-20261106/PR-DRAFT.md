# iOS: adopt native launcher navigation and refine adaptive library layouts

## Fix or feature

- [ ] Fix
- [x] Feature

## What and why

Custom navigation rails and repeated action placements made the library harder to follow across iPhone, iPad, and Duo layouts, especially when a game needed recovery. This change uses native SwiftUI toolbars, sheets, and grouped settings, with contextual primary actions across adaptive layouts. Implements #695 and relates to #622, following testing of #633 on v1.1.1 and the Duo orientation work in #230 and #642. Gameplay orientation policy and the saved arrangement format remain unchanged.

### Native navigation and adaptive libraries

- Controllers and Settings are independent system toolbar items. Game Settings sits beside Play in the library. Game Settings sheets put Play or the relevant recovery action in the toolbar.
- Portrait and tabletop libraries share the bottom action row. Cover Flow keeps compact actions with the focused game and supports touch swipes, keyboard, and controller navigation. Partially folded landscape uses one continuous carousel without duplicating the selected game.
- Tabletop keeps the selected-game context above the fold while the lower grid scrolls. Expanded portrait heroes collapse into a compact layout. Native sheets use contextual titles, Close, Back, and confirmation actions rather than custom navigation rails.
- Glass is reserved for appropriate controls and navigation. Content and settings sections retain standard grouped backgrounds. The cream/black treatment keeps primary and selected controls distinct.

### Game state, artwork, and selection

- Play already communicates availability, so remove redundant READY TO PLAY text while retaining the green artwork indicator for glanceability.
- Missing Data, Update Required, and Fix Game Files share an orange-outlined black status chip. Unavailable artwork is grayscale. A single alert color makes games needing attention easier to scan.
- A 4-point outline replaces the selection underline. Early testing found the line could appear to belong to either adjacent grid row.
- Use wide cover art for library heroes, tiles, and Cover Flow, and square app icons for Recently Played and Game Settings. Recently Played rows select a game, while the separate neutral Liquid Glass Play button launches that row’s game.
- Display the version once in a native Version row below Cloud Saves and above Reset/Delete. Remove version chips from heroes, artwork, and sheet headers. Longer titles use the available hero space without pushing the grid down.

### Touch Controls — review focus

Duo poses and small iPhone settings areas made the old preview difficult to understand and manipulate. Touch Controls now opens a full-screen editor, showing placement in gameplay context instead of inside a small settings card. iPhone editing uses landscape; supported portrait and Duo layouts follow the current display and pose. The contextual cog contains native Size and 2D/3D controls, reset, Save, and Exit. Exit confirms before discarding edits.

Existing grouping, boundary, overlap, and protected-menu checks remain. Save retains positions, global size, and the chosen 2D/3D default. Per-game overrides remain authoritative. Per-control resizing is outside the current engine format and is not included.

## Updated since the initial draft

- Replaced the outdated screenshots with matching current-main and proposed-design captures using the same nine Nintendo titles and official cover/icon metadata. Demo readiness, installed versions, recency, settings, and controller/battery values are simulated. This is not a game compatibility list.
- Refined the full-bleed cover-art hero and square-icon usage following the artwork feedback. Recently Played icons have subtler corners. The controller count is a black badge with white text, with a white controller symbol rather than an alert-red badge.
- Completed the shared native settings renderer for all profile-supplied choices, toggles, and ranges, including Upscaling and Picture. Native grouped sections, themed toggles and sliders, adaptive segmented/menu pickers, folder actions, and destructive Delete styling replace remaining legacy cards and controls. Inherited mapping values read Default.
- Refined Controllers, Button Mapping, and Button Test: native sheet navigation, contextual controller previews, a standard Swap A/B in Game toggle, and an adaptive Reset action with confirmation.

## UI bugs patched during the conversion

- Narrow controller rows truncate names without displacing battery status. VoiceOver retains the full name, and the charging bolt overlays the battery symbol.
- Toolbar actions stay available after scrolling and rotation. Presenting a sheet preserves the library layout and its toolbar space.
- Visible grid selections remain tappable during hero collapse and scroll into view. Controller focus does not double the artwork selection outline. Short libraries do not create artificial scrolling to animate the hero.
- Long-pressing a thumbnail no longer summons the software keyboard. Play is first in its context menu and is disabled for unavailable games; native hardware-key navigation remains available.
- Sheet content uses its available width, backgrounds extend behind native headers where appropriate, and the touch editor’s Save/Exit and orientation handling retain their editing state.


## Screenshots

Fresh comparisons captured on November 6, 2026. **Before** is current main `0af7a9f5`, with only screenshot-demo fixtures adapted. All 54 production source files in its iOS UI, host, and controller targets were verified unchanged. **Proposed design** is this branch at `533d2479` plus the local review changes. Publication commit `01999ca0` also integrates main `0af7a9f5`; its iOS UI, host, and controller sources are identical to the approved review commit `4ab3855e`. Main has no additional `frontend-ios` changes between the already integrated `9da53b33` and this baseline.

Both sides use the same nine-title Nintendo catalog and official cover/icon assets, with simulated game states. iPhone and iPad images are direct simulator screenshots. Duo images retain the actual Device Hub model and pose, cropped only around surrounding whitespace. Raw window captures and source/image hashes are recorded in the local screenshot manifest. These images replace the earlier mixed-revision comparison set.

<details>
<summary><strong>iPhone Duo — outer, inner, and folded poses</strong></summary>


**Outer portrait — library and primary action**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/01-outer-portrait-library.png" alt="Before: Outer portrait — library and primary action" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/01-outer-portrait-library.png" alt="Proposed design: Outer portrait — library and primary action" width="360"> |


**Outer portrait — Controllers**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/02-outer-portrait-controllers.png" alt="Before: Outer portrait — Controllers" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/02-outer-portrait-controllers.png" alt="Proposed design: Outer portrait — Controllers" width="360"> |


**Outer portrait — Game Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/03-outer-portrait-game-settings.png" alt="Before: Outer portrait — Game Settings" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/03-outer-portrait-game-settings.png" alt="Proposed design: Outer portrait — Game Settings" width="360"> |


**Outer portrait — App Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/04-outer-portrait-app-settings.png" alt="Before: Outer portrait — App Settings" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/04-outer-portrait-app-settings.png" alt="Proposed design: Outer portrait — App Settings" width="360"> |


**Outer portrait — Missing Data**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/05-outer-portrait-missing-data.png" alt="Before: Outer portrait — Missing Data" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/05-outer-portrait-missing-data.png" alt="Proposed design: Outer portrait — Missing Data" width="360"> |


**Fully open inner portrait — library**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/06-inner-portrait-library.png" alt="Before: Fully open inner portrait — library" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/06-inner-portrait-library.png" alt="Proposed design: Fully open inner portrait — library" width="360"> |


**Tabletop portrait — fixed hero and lower library**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/07-tabletop-library.png" alt="Before: Tabletop portrait — fixed hero and lower library" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/07-tabletop-library.png" alt="Proposed design: Tabletop portrait — fixed hero and lower library" width="360"> |


**Tabletop portrait — Game Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/08-tabletop-game-settings.png" alt="Before: Tabletop portrait — Game Settings" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/08-tabletop-game-settings.png" alt="Proposed design: Tabletop portrait — Game Settings" width="360"> |


**Fully open inner landscape — Cover Flow**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/09-inner-landscape-coverflow.png" alt="Before: Fully open inner landscape — Cover Flow" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/09-inner-landscape-coverflow.png" alt="Proposed design: Fully open inner landscape — Cover Flow" width="360"> |


**Partially folded landscape — continuous Cover Flow**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/10-partial-landscape-coverflow.png" alt="Before: Partially folded landscape — continuous Cover Flow" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/10-partial-landscape-coverflow.png" alt="Proposed design: Partially folded landscape — continuous Cover Flow" width="360"> |


**Outer landscape — camera at bottom right**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/11-outer-landscape-left.png" alt="Before: Outer landscape — camera at bottom right" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/11-outer-landscape-left.png" alt="Proposed design: Outer landscape — camera at bottom right" width="360"> |


**Outer landscape — camera at top left**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/12-outer-landscape-right.png" alt="Before: Outer landscape — camera at top left" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/12-outer-landscape-right.png" alt="Proposed design: Outer landscape — camera at top left" width="360"> |


**Tabletop portrait — Controllers**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/13-tabletop-controllers.png" alt="Before: Tabletop portrait — Controllers" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/13-tabletop-controllers.png" alt="Proposed design: Tabletop portrait — Controllers" width="360"> |


**Partially folded landscape — Game Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/14-partial-landscape-game-settings.png" alt="Before: Partially folded landscape — Game Settings" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/14-partial-landscape-game-settings.png" alt="Proposed design: Partially folded landscape — Game Settings" width="360"> |


**Partially folded landscape — App Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/15-partial-landscape-app-settings.png" alt="Before: Partially folded landscape — App Settings" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/15-partial-landscape-app-settings.png" alt="Proposed design: Partially folded landscape — App Settings" width="360"> |


**Partially folded landscape — Controllers**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/16-partial-landscape-controllers.png" alt="Before: Partially folded landscape — Controllers" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/16-partial-landscape-controllers.png" alt="Proposed design: Partially folded landscape — Controllers" width="360"> |


**Tabletop portrait — App Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/duo/01-before/17-tabletop-app-settings.png" alt="Before: Tabletop portrait — App Settings" width="360"> | <img src="images/review-20261106/duo/02-proposed-design/17-tabletop-app-settings.png" alt="Proposed design: Tabletop portrait — App Settings" width="360"> |


</details>

<details>
<summary><strong>iPhone — iPhone 17 Pro</strong></summary>


**Portrait library and contextual primary action**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/01-library-portrait.png" alt="Before: Portrait library and contextual primary action" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/01-library-portrait.png" alt="Proposed design: Portrait library and contextual primary action" width="360"> |


**Controllers — native rows, title, and battery states**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/02-controllers.png" alt="Before: Controllers — native rows, title, and battery states" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/02-controllers.png" alt="Proposed design: Controllers — native rows, title, and battery states" width="360"> |


**Game Settings — artwork, native choices, and toggles**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/03-game-settings-top.png" alt="Before: Game Settings — artwork, native choices, and toggles" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/03-game-settings-top.png" alt="Proposed design: Game Settings — artwork, native choices, and toggles" width="360"> |


**Game Settings — performance sliders and folder controls**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/03b-game-settings-middle.png" alt="Before: Game Settings — performance sliders and folder controls" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/03b-game-settings-middle.png" alt="Proposed design: Game Settings — performance sliders and folder controls" width="360"> |


**Game Settings — Cloud Saves, Version, Reset, and Delete**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/03c-game-settings-bottom.png" alt="Before: Game Settings — Cloud Saves, Version, Reset, and Delete" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/03c-game-settings-bottom.png" alt="Proposed design: Game Settings — Cloud Saves, Version, Reset, and Delete" width="360"> |


**App Settings — native grouped rows and Touch Controls entry**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/04-app-settings.png" alt="Before: App Settings — native grouped rows and Touch Controls entry" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/04-app-settings.png" alt="Proposed design: App Settings — native grouped rows and Touch Controls entry" width="360"> |


**Touch Controls entry — legacy preview and native settings row**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/04b-touch-controls-settings.png" alt="Before: Touch Controls entry — legacy preview and native settings row" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/04b-touch-controls-settings.png" alt="Proposed design: Touch Controls entry — legacy preview and native settings row" width="360"> |


**Missing Data — shared recovery action and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/05-missing-data.png" alt="Before: Missing Data — shared recovery action and unavailable artwork" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/05-missing-data.png" alt="Proposed design: Missing Data — shared recovery action and unavailable artwork" width="360"> |


**Update Required — shared recovery action and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/06-update-required.png" alt="Before: Update Required — shared recovery action and unavailable artwork" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/06-update-required.png" alt="Proposed design: Update Required — shared recovery action and unavailable artwork" width="360"> |


**Fix Game Files — shared alert treatment and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/07-fix-game-files.png" alt="Before: Fix Game Files — shared alert treatment and unavailable artwork" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/07-fix-game-files.png" alt="Proposed design: Fix Game Files — shared alert treatment and unavailable artwork" width="360"> |


**Button Mapping — native navigation and controller context**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/08-button-mapping.png" alt="Before: Button Mapping — native navigation and controller context" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/08-button-mapping.png" alt="Proposed design: Button Mapping — native navigation and controller context" width="360"> |


**Button Mapping — child selection and mapping context**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/08b-button-mapping-choice.png" alt="Before: Button Mapping — child selection and mapping context" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/08b-button-mapping-choice.png" alt="Proposed design: Button Mapping — child selection and mapping context" width="360"> |


**Button Test — visual controller feedback in native navigation**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/09-button-test.png" alt="Before: Button Test — visual controller feedback in native navigation" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/09-button-test.png" alt="Proposed design: Button Test — visual controller feedback in native navigation" width="360"> |


**Landscape library and Cover Flow**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/10-library-landscape.png" alt="Before: Landscape library and Cover Flow" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/10-library-landscape.png" alt="Proposed design: Landscape library and Cover Flow" width="360"> |


**Landscape Game Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/11-game-settings-landscape.png" alt="Before: Landscape Game Settings" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/11-game-settings-landscape.png" alt="Proposed design: Landscape Game Settings" width="360"> |


**Wide Button Mapping — preview beside controls**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/12-button-mapping-landscape.png" alt="Before: Wide Button Mapping — preview beside controls" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/12-button-mapping-landscape.png" alt="Proposed design: Wide Button Mapping — preview beside controls" width="360"> |


**Touch Controls — small arrangement preview to full-screen editing**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/13-touch-editor-landscape.png" alt="Before: Touch Controls — small arrangement preview to full-screen editing" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/13-touch-editor-landscape.png" alt="Proposed design: Touch Controls — small arrangement preview to full-screen editing" width="360"> |


**Touch Controls — contextual native editor options**

Current editor options (the old editor has no equivalent contextual cog menu):

<img src="images/review-20261106/iphone17pro/02-proposed-design/14-touch-editor-options.png" alt="Touch Controls — contextual native editor options" width="600">


**Localized App Settings — de**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/15-app-settings-de.png" alt="Before: Localized App Settings — de" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/15-app-settings-de.png" alt="Proposed design: Localized App Settings — de" width="360"> |


**Localized App Settings — fr**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/15-app-settings-fr.png" alt="Before: Localized App Settings — fr" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/15-app-settings-fr.png" alt="Proposed design: Localized App Settings — fr" width="360"> |


**Localized App Settings — it**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/15-app-settings-it.png" alt="Before: Localized App Settings — it" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/15-app-settings-it.png" alt="Proposed design: Localized App Settings — it" width="360"> |


**Localized App Settings — sv**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/15-app-settings-sv.png" alt="Before: Localized App Settings — sv" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/15-app-settings-sv.png" alt="Proposed design: Localized App Settings — sv" width="360"> |


**Localized App Settings — zh-Hans**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/15-app-settings-zh-Hans.png" alt="Before: Localized App Settings — zh-Hans" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/15-app-settings-zh-Hans.png" alt="Proposed design: Localized App Settings — zh-Hans" width="360"> |


**Native thumbnail context menu — Play first**

The same long press on current main leaves the library visible. The proposed design presents Play and Game Settings. The keyboard regression arose during conversion and is covered separately by the focused UI test.

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/iphone17pro/01-before/16-thumbnail-context-menu.png" alt="Before: Native thumbnail context menu — Play first" width="360"> | <img src="images/review-20261106/iphone17pro/02-proposed-design/16-thumbnail-context-menu.png" alt="Proposed design: Native thumbnail context menu — Play first" width="360"> |


</details>

<details>
<summary><strong>iPad — Pro 11-inch and mini</strong></summary>
<details>
<summary><strong>iPad — Pro 11-inch (M5)</strong></summary>


**Portrait library and contextual primary action**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/01-library-portrait.png" alt="Before: Portrait library and contextual primary action" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/01-library-portrait.png" alt="Proposed design: Portrait library and contextual primary action" width="360"> |


**Controllers — native rows, title, and battery states**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/02-controllers.png" alt="Before: Controllers — native rows, title, and battery states" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/02-controllers.png" alt="Proposed design: Controllers — native rows, title, and battery states" width="360"> |


**Game Settings — artwork, native choices, and toggles**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/03-game-settings-top.png" alt="Before: Game Settings — artwork, native choices, and toggles" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/03-game-settings-top.png" alt="Proposed design: Game Settings — artwork, native choices, and toggles" width="360"> |


**Game Settings — performance sliders and folder controls**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/03b-game-settings-middle.png" alt="Before: Game Settings — performance sliders and folder controls" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/03b-game-settings-middle.png" alt="Proposed design: Game Settings — performance sliders and folder controls" width="360"> |


**Game Settings — Cloud Saves, Version, Reset, and Delete**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/03c-game-settings-bottom.png" alt="Before: Game Settings — Cloud Saves, Version, Reset, and Delete" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/03c-game-settings-bottom.png" alt="Proposed design: Game Settings — Cloud Saves, Version, Reset, and Delete" width="360"> |


**App Settings — native grouped rows and Touch Controls entry**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/04-app-settings.png" alt="Before: App Settings — native grouped rows and Touch Controls entry" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/04-app-settings.png" alt="Proposed design: App Settings — native grouped rows and Touch Controls entry" width="360"> |


**Missing Data — shared recovery action and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/05-missing-data.png" alt="Before: Missing Data — shared recovery action and unavailable artwork" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/05-missing-data.png" alt="Proposed design: Missing Data — shared recovery action and unavailable artwork" width="360"> |


**Update Required — shared recovery action and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/06-update-required.png" alt="Before: Update Required — shared recovery action and unavailable artwork" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/06-update-required.png" alt="Proposed design: Update Required — shared recovery action and unavailable artwork" width="360"> |


**Fix Game Files — shared alert treatment and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/07-fix-game-files.png" alt="Before: Fix Game Files — shared alert treatment and unavailable artwork" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/07-fix-game-files.png" alt="Proposed design: Fix Game Files — shared alert treatment and unavailable artwork" width="360"> |


**Button Mapping — native navigation and controller context**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/08-button-mapping.png" alt="Before: Button Mapping — native navigation and controller context" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/08-button-mapping.png" alt="Proposed design: Button Mapping — native navigation and controller context" width="360"> |


**Button Test — visual controller feedback in native navigation**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/09-button-test.png" alt="Before: Button Test — visual controller feedback in native navigation" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/09-button-test.png" alt="Proposed design: Button Test — visual controller feedback in native navigation" width="360"> |


**Landscape library and Cover Flow**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/10-library-landscape.png" alt="Before: Landscape library and Cover Flow" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/10-library-landscape.png" alt="Proposed design: Landscape library and Cover Flow" width="360"> |


**Landscape Game Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/11-game-settings-landscape.png" alt="Before: Landscape Game Settings" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/11-game-settings-landscape.png" alt="Proposed design: Landscape Game Settings" width="360"> |


**Wide Button Mapping — preview beside controls**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/12-button-mapping-landscape.png" alt="Before: Wide Button Mapping — preview beside controls" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/12-button-mapping-landscape.png" alt="Proposed design: Wide Button Mapping — preview beside controls" width="360"> |


**Touch Controls — small arrangement preview to full-screen editing**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadpro11/01-before/13-touch-editor-landscape.png" alt="Before: Touch Controls — small arrangement preview to full-screen editing" width="360"> | <img src="images/review-20261106/ipadpro11/02-proposed-design/13-touch-editor-landscape.png" alt="Proposed design: Touch Controls — small arrangement preview to full-screen editing" width="360"> |


**Touch Controls — contextual native editor options**

Current editor options (the old editor has no equivalent contextual cog menu):

<img src="images/review-20261106/ipadpro11/02-proposed-design/14-touch-editor-options.png" alt="Touch Controls — contextual native editor options" width="600">


</details>

<details>
<summary><strong>iPad — mini (A20 Pro)</strong></summary>


**Portrait library and contextual primary action**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/01-library-portrait.png" alt="Before: Portrait library and contextual primary action" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/01-library-portrait.png" alt="Proposed design: Portrait library and contextual primary action" width="360"> |


**Controllers — native rows, title, and battery states**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/02-controllers.png" alt="Before: Controllers — native rows, title, and battery states" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/02-controllers.png" alt="Proposed design: Controllers — native rows, title, and battery states" width="360"> |


**Game Settings — artwork, native choices, and toggles**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/03-game-settings-top.png" alt="Before: Game Settings — artwork, native choices, and toggles" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/03-game-settings-top.png" alt="Proposed design: Game Settings — artwork, native choices, and toggles" width="360"> |


**Game Settings — performance sliders and folder controls**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/03b-game-settings-middle.png" alt="Before: Game Settings — performance sliders and folder controls" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/03b-game-settings-middle.png" alt="Proposed design: Game Settings — performance sliders and folder controls" width="360"> |


**Game Settings — Cloud Saves, Version, Reset, and Delete**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/03c-game-settings-bottom.png" alt="Before: Game Settings — Cloud Saves, Version, Reset, and Delete" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/03c-game-settings-bottom.png" alt="Proposed design: Game Settings — Cloud Saves, Version, Reset, and Delete" width="360"> |


**App Settings — native grouped rows and Touch Controls entry**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/04-app-settings.png" alt="Before: App Settings — native grouped rows and Touch Controls entry" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/04-app-settings.png" alt="Proposed design: App Settings — native grouped rows and Touch Controls entry" width="360"> |


**Missing Data — shared recovery action and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/05-missing-data.png" alt="Before: Missing Data — shared recovery action and unavailable artwork" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/05-missing-data.png" alt="Proposed design: Missing Data — shared recovery action and unavailable artwork" width="360"> |


**Update Required — shared recovery action and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/06-update-required.png" alt="Before: Update Required — shared recovery action and unavailable artwork" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/06-update-required.png" alt="Proposed design: Update Required — shared recovery action and unavailable artwork" width="360"> |


**Fix Game Files — shared alert treatment and unavailable artwork**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/07-fix-game-files.png" alt="Before: Fix Game Files — shared alert treatment and unavailable artwork" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/07-fix-game-files.png" alt="Proposed design: Fix Game Files — shared alert treatment and unavailable artwork" width="360"> |


**Button Mapping — native navigation and controller context**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/08-button-mapping.png" alt="Before: Button Mapping — native navigation and controller context" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/08-button-mapping.png" alt="Proposed design: Button Mapping — native navigation and controller context" width="360"> |


**Button Test — visual controller feedback in native navigation**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/09-button-test.png" alt="Before: Button Test — visual controller feedback in native navigation" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/09-button-test.png" alt="Proposed design: Button Test — visual controller feedback in native navigation" width="360"> |


**Landscape library and Cover Flow**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/10-library-landscape.png" alt="Before: Landscape library and Cover Flow" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/10-library-landscape.png" alt="Proposed design: Landscape library and Cover Flow" width="360"> |


**Landscape Game Settings**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/11-game-settings-landscape.png" alt="Before: Landscape Game Settings" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/11-game-settings-landscape.png" alt="Proposed design: Landscape Game Settings" width="360"> |


**Wide Button Mapping — preview beside controls**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/12-button-mapping-landscape.png" alt="Before: Wide Button Mapping — preview beside controls" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/12-button-mapping-landscape.png" alt="Proposed design: Wide Button Mapping — preview beside controls" width="360"> |


**Touch Controls — small arrangement preview to full-screen editing**

| Before · main `0af7a9f5` | Proposed design |
| --- | --- |
| <img src="images/review-20261106/ipadmini/01-before/13-touch-editor-landscape.png" alt="Before: Touch Controls — small arrangement preview to full-screen editing" width="360"> | <img src="images/review-20261106/ipadmini/02-proposed-design/13-touch-editor-landscape.png" alt="Proposed design: Touch Controls — small arrangement preview to full-screen editing" width="360"> |


**Touch Controls — contextual native editor options**

Current editor options (the old editor has no equivalent contextual cog menu):

<img src="images/review-20261106/ipadmini/02-proposed-design/14-touch-editor-options.png" alt="Touch Controls — contextual native editor options" width="600">


</details>

</details>

## Checked

Both screenshot-demo builds compile with the current installed SDK. Matching portrait/landscape captures cover iPhone 17 Pro, iPad Pro 11-inch, and iPad mini; the Duo group documents the displayed outer, open, tabletop, and partially folded poses. German, French, Italian, Swedish, and Simplified Chinese Settings comparisons supplement English. These captures establish the displayed layouts, not full translated coverage, Split View, Stage Manager, VoiceOver, physical hinge behavior, or game compatibility.

The prior code-validation pass passed the iOS package tests, including 63 ShellUI and 168 ShellHost Swift Testing cases. This refresh changes only screenshot fixtures/harnesses and local review artifacts. No gameplay launch, game data, or saved controls are modified by the capture process.

The branch retains the local main integration and renumbers the Duo outer-landscape custom-placement companion to patch **0085**. Built-in safe-area defaults, collision checks, and the protected menu area remain unchanged; expanded custom bounds require rebuilt games. Patch **0086** carries the separately requested TV/controller gear fix from #818. Static demo screenshots cannot validate either engine change. No Mac launcher redesign or data migration is included.

## Scope

- [x] Engine changes are carried as patches with their Upstream-Status rather than adding engine source files.
- [ ] Patch 0085 is still pending an upstream PR. Patch 0086 is forwarded to seedds/nxnative#1485.
- [x] Fresh English before/after screenshots cover the launcher surfaces above, with matching Nintendo fixtures and device poses.
- [ ] All changed views have translated before/after coverage. Six-language App Settings comparisons are included; other translated views were not recaptured in this pass.
- [x] No keys, game files, or data extracted from games are included in code or attachments.

## Merge Danger

**Door:** UI changes are reversible without a data migration. Keep the custom-bounds editor and its engine companion paired.

**Blast Radius:** iOS launcher navigation, sheets, settings, focus, adaptive library layouts, and the touch editor. Engine companions affect only their documented Duo outer-landscape and TV/controller conditions.
