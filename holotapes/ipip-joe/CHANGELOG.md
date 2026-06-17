# iPip Media Player v1.3.0

### Modifications by Joe Byers

### Based on iPip Media Player v1.2.1 by Cody Tolene

---

# FEATURE CHANGES

### Added Upload-Order Song Sorting

* Added a third sort mode: **UPLOAD**.
* Original build only supported **A-Z** and **Z-A** sorting.
* Upload order is now the default mode.
* Added upload-order backup array (`ao`) to preserve original file order.
* Original filesystem upload order can now be restored instantly without reloading playlists.

### Added Upload / A-Z / Z-A Sort Cycling

* Sort menu now cycles:

  * UPLOAD → A-Z → Z-A → UPLOAD
* Original version only toggled:

  * A-Z ↔ Z-A

### Preserved Original Filesystem Order

* Removed automatic alphabetical sorting when reading playlist folders.
* Upload order is now preserved before any custom sorting is applied.
* Allows accurate restoration of original playlist order.

### Increased Filename / Path Length Limit

* Raised path-length limit from 56 characters to 200 characters.
* Longer filenames that were previously rejected can now be loaded and played.

### Added Long Song Title Scrolling Marquee

* Added scrolling marquee title system for currently playing tracks.
* Includes a pause before scrolling begins.
* Continuously scrolls while music is playing.
* Improves readability of long song names.

---

# PLAYBACK CHANGES

### Modified Song Selection Behavior

* Selecting an individual song now prepares proper sequential playback continuation.
* Current song position is tracked so playback can continue correctly afterward.

### Sequential Playback Enabled by Default

* Selecting a song now automatically enables sequential playlist playback.
* Playback continues through the playlist after the selected song finishes.
* Eliminates the need to manually start a separate Play All mode after selecting a track.
* Provides a more radio-like listening experience while preserving direct song selection.

### Modified Play-All Logic

* Play-all position is recalculated after sort-order changes.
* Current song is preserved when sort order changes during playback.

### Modified Audio-Stopped Callback

* Added delayed advancement during sequential playback.
* Play-all now advances through a timeout instead of immediately.
* Intended to reduce callback-related instability observed during testing.

### Improved Playlist Selection Responsiveness

* Playback transition timing was adjusted after track completion.
* Added a short delay before automatic advancement to improve reliability.
* Helps prevent callback-related playback issues observed during testing.

---

# RANDOM PLAYBACK CHANGES

### Reworked Random Queue Construction

* Random queue now builds manually from valid songs.
* Random playback avoids immediately replaying the currently playing song after reshuffling.
* Queue reshuffles automatically when exhausted.

---

# USER INTERFACE CHANGES

### Simplified Main Menu Labels

Removed:

* SHUFFLE PLAY ALL
* PLAY ALL
* PLAY ALL (TOP-DOWN)
* BACK TO PLAYLISTS

Replaced with:

* RANDOMIZE
* BACK

### Updated Sort Menu Display

Sort menu now displays:

* UPLOAD
* A-Z
* Z-A

instead of only:

* A-Z
* Z-A

### Updated Playback Status Text

* Random playback status text updated to match RANDOMIZE terminology.

### Expanded Interface Audio Feedback

* Added additional UI sound feedback throughout menu navigation and playback controls.
* More actions now provide audible confirmation when activated.

### Modified Volume Wheel Direction

* Volume adjustment direction was reversed to better match expected wheel behavior.

---

# PERFORMANCE / RESPONSIVENESS CHANGES

### Increased Wheel Responsiveness

* Thumbwheel debounce reduced from 50ms to 5ms.
* Improves wheel responsiveness and menu navigation feel.

### Reduced Navigation Delay

* Navigation timing adjusted to improve menu responsiveness.
* Menu movement reacts more immediately to wheel input.

### Increased Volume Overlay Visibility

* Volume display timeout increased from 1.5 seconds to 3 seconds.

---

# INTERNAL CODE CHANGES

### Added Upload-Order Backup Array

Added:

* `ao = []`

Purpose:

* Stores original song order independently of active sort order.
* Allows instant restoration of upload order.

### Replaced Built-In Sort Method

* Original version relied on JavaScript's built-in sort behavior.
* Hybrid version uses custom insertion-sort logic.
* Preserves upload order while supporting A-Z and Z-A sorting modes.

### Added Scrolling Title State Variables

Added:

* `ts`
* `tsLast`
* `tsName`

Purpose:

* Manage title scrolling position and timing.

### Modified Waveform Refresh Timer

* Waveform refresh timer now also updates scrolling song titles during playback.
* Enables smooth continuous title scrolling without requiring additional timers.

### Revised Sort Data Management

* Sorting logic was redesigned to preserve upload order and improve playback synchronization.
* Sort-related behavior was reworked after crashes were encountered during testing.

---

# STABILITY CHANGES

### Reduced Sort-Related Stability Issues

* Sort implementation was revised after crashes were observed during development and testing.
* New implementation has demonstrated improved stability during testing.

### Improved Sort / Playback Synchronization

* Sorting while playback is active now attempts to preserve the correct next-song position.
* Helps maintain playback continuity after sort changes.

### Improved Playback State Management

* Playback state handling was updated to better coordinate sorting, random playback, and sequential playback modes.
* Reduces the likelihood of playlist position desynchronization after user actions.

---

# PROJECT GOAL

Preserve Cody's original iPip functionality while improving usability, adding upload-order playback support, increasing filename compatibility, improving navigation responsiveness, adding scrolling titles, improving playback continuity, and providing more flexible sorting behavior.
