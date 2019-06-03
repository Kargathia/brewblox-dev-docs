# BrewBlox Release Notes

## Edge release 2019/05/28

**Firmware version: 9b0330f4** (no changes)

Also compatible: 2789cc06.

A set of smaller changes. Two bigger features are in progress, but are not yet ready for release:

- A rework of digital actuators, to also support valve expansion boards.
- A stepper widget: apply predetermined changes to multiple Blocks at the same time.

**Changes**

- The Spark service page can now be sorted by Block role.
  - Roles are: Process, Control, Output, Limiter, and Display.
  - The icons in the Spark page index are now role-specific.
- Sorting in the Spark page is now persistent (will retain the setting if you reload the page).
- Fixed a bug where Block (widget) wizards would not allow `-` characters in the name.
- The Blocks in the relations diagram are now clickable.
  - Clicking on them will open the settings popup for that Block.
- Added a "show relations" action to PID.
  - This displays its direct relations: from the sensor input to the pin output.
  - Blocks in this display are also clickable.
- The metric selection trees in Graph/Metric wizards display fields that have had an update in the last day.

## Edge release 2019/05/20

**Firmware version: 9b0330f4** (no changes)

Also compatible: 2789cc06.

The UI can be very overwhelming and cluttered, especially for new users.
To combat this, we've updated the Spark page. It is now more suitable for quickly finding and showing specific blocks.

In the future, we'll also be grouping blocks more. For many use cases, [control loops](https://brewblox.netlify.com/user/control_chains.html) are more relevant than a bunch of loose blocks.

**Changes**

- Reworked the Spark service page.
  - An index is shown on the left, and the blocks on the right.
  - To show a block on the right, select it in the index.
  - Added searching and sorting blocks in the service page.
- Improved the block relations diagram.
  - Layout is now more inline with the control chain documentation diagrams.
  - Relations diagram is now scrollable.
  - Added an "export" button. This will export the full diagram as PNG.
  - Type display names are now used in the diagram (was: type id).
- Added preview graphs to Graph and Setpoint Profile widgets.
  - They're shown when editing the widget, if the browser window is at least 1500px wide.
  - We're considering whether to add them to all block widgets that can display fullscreen graphs.
- Fixed a bug where text fields in the Process view edit window would trigger tool shortcuts.
- Fixed a bug where editing copied widgets and parts would also change the original.
- Fixed scrolling in Graph and Metric widgets if a large number of metrics were selected.
- Changed the display name of "Offset Actuator" to "Setpoint Driver".
- Changed the display name of "Pulse Width Modulator" to "PWM".

## Edge release 2019/05/14

**Firmware version: 9b0330f4** (same as last week)

Also compatible: 2789cc06. 

**Changes**

- Fixed a bug where the Block relations diagram would fail to render if any Block linked to a non-existent other Block.
- Removed a fix for an earlier bug, where the Process View edit window would calculate the wrong grid square when opened after scrolling the page.
  - The bug was also fixed upstream, making our fix an overcorrection.
- Improved error messages when the UI failed to save the change in the backend.
- Added the "Export errors" action.
  - This can be found in a dropdown menu in the bottom left corner of the sidebar.
  - This will save all REST/datastore errors in the current session to a .json file.
  - If you're getting error messages in the UI, please run this action, and add the file in your bug report.
  - Errors are only kept for the current session: please export them before refreshing the page.
- Fixed a bug where during creation of a Setpoint Profile, no target Block could be selected.
- Moved both Y-axes in graphs to the right side, for easier viewing of the latest value.
- The Brewpi Classic arrangement wizard now also creates a Graph widget
- During the Brewpi Classic wizard, initial fridge/beer setpoint values are configurable in the user-defined temperature units.
- The first created point in a Setpoint Profile is automatically set at 20 degC, 68 degF, or 293 degK, depending on the user-defined temperature unit.
- When editing the Graph settings, a small preview graph is displayed.
  - This is only shown if the browser viewport is more than 1500px wide.
- Fixed a bug in brewblox-devcon-spark where Blocks could not be read/changed/deleted using their numeric ID.

## Edge release 2019/05/07

**Firmware version: 9b0330f4**
If you're on the previous firmware version (2789cc06), you don't need to flash your Spark.

This release, we've reworked the brewblox-ctl tool. This improved code quality, and gives us more options for what we can do with future commands.

Running `brewblox-ctl` without a command will no longer open a menu, but now print all available commands. This allows us to add arguments to commands.

**Changes**

- Reworked brewblox-ctl.
  - When running brewblox-ctl on an ARMv6 platform (Raspberry Pi model 0 or 1), a warning message with a confirmation prompt will be shown on startup.
  - The firmware flash commands will no longer print a notification about updating particle-cli.
  - The flash/bootloader/wifi commands must now either be run in a BrewBlox directory, or with the `--release` argument.
  - Added `brewblox-ctl http`. This is used by other commands to make HTTP requests, and can be used for debugging the system.
  - The system will automatically restart after running `brewblox-ctl update`
- Made decimal precision user-configurable in the Metrics widget.
- Made the rules for new Block IDs stricter to prevent future issues.
  - ID must start with a letter.
  - ID may consist of letters, numbers, spaces, and these characters: | ( ) _ -
  - ID must not be longer than 200 characters.
- Fixed a bug where clicking on an actuator button in unknown state would do nothing.
- Disabled edit button (pencil) in PID widgets for input/output blocks that are not set.
- The Wizardry menu is now scrollable on smaller screens.
- Fixed a bug where the Block ID was still reserved if Block creation failed during importing of Spark Blocks.
- Fixed a bug where importing a large amount of Blocks over USB would cause a buffer overrun.

## Edge release 2019/04/29

**Changes**

- Added the Metrics widget
  - This is like the Graph widget, except that it only displays the last logged value from history.
  - It displays warning messages for values that have not been updated in a while. The "valid time" can be configured.
- Fixed importing/exporting Blocks on the Spark controller.
  - The export format has changed: old export files are no longer compatible.
  - The import button is re-enabled in the Spark service page.
  - If a Block couldn't be imported, it will be skipped, and a message will be displayed in the UI.
  - Removed the savepoints functionality, as it was made obsolete by the new import/export mechanics.
- Fixed a bug where Setpoint Profile would fail to save points with a temperature lower than 0°C.
- In Process View, if a part can be linked to a Block (valves, sensors), the part menu now has a shortcut to configure the linked Block.
- Fixed a bug where new Process View parts would be placed incorrectly if you scrolled the page before opening the edit modal.
- Improved widget layout: if a Block has both a setting, and a measured value, it will consistently display setting before (left of) value.
- Services will now log their version on startup.
- EDIT: brewblox-ctl now allows disabling confirmation prompts. Run `brewblox-ctl settings` to enable/disable.

## Edge release 2019/04/23

There are no firmware changes in this release. If you have the latest version (2019/04/18), you do not need to flash your Spark. When in doubt, it's best to be safe and flash your Spark.

**Changes**

- In the Process View edit modal, tools can now be swapped by hotkey.
    - Keys are listed to the right of the tool in the side bar.
- In Process View, parts can be flipped again, using either the part menu, or the Flip tool.
- Improved part display in the "New Part" modal.
- Moved generic actions from the Spark Widget modal to the Actions button in the Spark service page.
- Fixed a bug in Graph where the config would be corrupted when changing display type.
- Fixed a bug in PID where Measured and Target output were displayed swapped.
- DS2413 actuators are now viable options when running the BrewPi classic arrangement wizard.
    - For now, you must manually create the DS2413 actuator.
    - A button to create new blocks was added to the wizard.


## Edge release 2019/04/18

This is a small release, to fix two serious bugs. We will be releasing new features after Easter.

**Changes**

- Fixed a bug where setpoint profile time values would be corrupted after changing them.
- Fixed a bug where some Block wizards would crash.

## Edge release 2019/04/16
- Fixed how setpoint/sensor pair works, so that setting can always be set and enabled/disabled is handled separately.
- Fixed some issues with popup edit menus
- Make invalid widgets deletable
- Fix tree dropdown in graph config to not hide children when search is used

## Edge release 2019/04/15

**Breaking Changes**

- SetpointSimple Blocks no longer exist, and have been merged into SetpointSensorPair
- SetpointProfile now drives SetpointSensorPair
- In Process View, rotated parts larger than 1x1 will have moved a few squares.
  - This is due to the new calculation for rotating parts

**Changes**

- Resolved multiple issues with setpoints. 
  - Merged SetpointSimple and SetpointSensorPair.
  - All fancy setpoints (eg. SetpointProfile) are now drivers of SetpointSensorPair.
  - Thanks @j616s for the suggestion of making SetpointProfile a driver!
- Fixed a bug where disabling a PID would not set its output value to 0.
- Overhauled how Process View is edited:
  - Editing is now done in a fullscreen modal. The widget is never editable.
  - Moved "Export widget" and "Delete all parts" actions to the edit modal.
  - Parts are highlighted on mouseover in the edit modal.
  - Editing can be done with selectable tools. Select a tool, and then click or drag parts.
  - Available tools: 
    - Click to add new part.
    - Drag to move part.
    - Click to rotate part.
    - Click to open part menu (edit settings).
    - Click to interact with part (toggle valves and pumps).
    - Drag to copy part.
    - Click to delete part.
- Parts now consistently react if you click in the square containing the part.
- When rotating parts, the upper left corner will stay in place. (the part used to rotate around its center).
- Fixed a bug where flows would be incorrectly calculated for rotated parts greater than 1x1.
- Improved responsiveness when moving parts.
- Improved collision detection when moving parts.
- HeatingElement parts can now be linked to a PWM Block, and will display the achieved duty setting.
- Fixed a bug where ActuatorValve parts would cause datastore conflicts
- Fixed a bug where datastore conflicts would cause Process View to silently stop persisting changes
  - An error is now displayed, and the last change is rolled back. You can redo the change to continue.
- Widgets are now unpinned when moved or copied.
- Disabled the "Import Blocks" button while we fix some serious issues.
- When a service loses connection, a notification with a "Retry" button is displayed.
  - This notification will disappear automatically if connection is restored.
- Made PID input/output blocks directly editable from the PID widget.

## Edge release 2019/04/04

This release includes a pretty big rework of the UI.

The framework we're using for UI components ([Quasar](https://v1.quasar-framework.org/)) recently released a major update.
While we were making all the required changes, we took the opportunity to revisit many of our more clumsy UI elements.

We're pretty happy with the result. It looks better, loads faster, and the underlying code is significantly cleaner.

Changes:

- Lots of small display improvements throughout the UI.
  - The dashboard background is now lighter than the widgets, improving contrast.
  - Widget title is now displayed above the type to improve display of small widgets.
  - Widgets now have a dropdown menu with additional actions. This allowed us to add more actions while saving space.
  - Improved layout for all widgets and widget settings forms.
  - Removed color from unimportant warnings (eg. inactive actuators).
  - Improved and standardized the toolbar in modal windows (eg. Widget settings).
- The Block relations diagram is now displayed fullscreen.
- Fixed multiple issues with the Block relations diagram, and improved startup time.
- Reworked all wizards to be more consistent and easier to navigate.
- The widget options menu (accessible in dashboard edit mode) is removed.
- Added the widget actions to a dropdown menu. This makes copy/move/delete widget buttons more accessible.
- You can now resize widgets without activating dashboard edit mode.
  - Widgets on the Spark page are still not resizable.
- Fixed an issue where the version would not display in the left drawer.
- You can now separately change dashboard title (displayed) and ID (unique, used for the URL)
- Widget names were reworked.
  - Widget names no longer have to be unique.
  - Block widgets now always use the Block ID as name. This improves visibility how widgets and blocks are linked.
  - You can freely change names for non-block widgets (graph, session view, process view).
- You can now export and import widgets.
  - For now the Process view is the only widget where exporting it makes any sense.
  - Import widgets in the Wizardry menu.
- You can now export, import, and clear Blocks on the controller.
  - The functionality is accessible through the Spark Service widget.
  - Exporting Blocks will export all Blocks.
  - Clearing Blocks will remove all user-added Blocks, and reset the system Blocks.
  - Importing Blocks will first clear Blocks, and then import from file.
- Fixed a bug where the Lauterhexe Process view part did not have any flow.
- Added the small and large kettles to the Process view.
  - This is in addition to the "normal" kettle already available.
- Added the Sensor display part to the Process view. It can be linked to a temperature sensor, and will display the value.
- Added the Actuator valve part to the Process view. It can be linked to a digital actuator (Actuator Pin or DS2413 Actuator).
  - Toggling the valve will toggle the actuator, and vice versa.
- Fixed a bug where the eventbus would gradually consume more RAM, until it froze.

## Edge release 2019/03/18

- `brewblox-ctl update` will now prompt to also update the firmware
  - IMPORTANT: this does not apply to this update. You will need to manually run `brewblox-ctl flash` this time.
- Updated the firmware system layer to version 1.0.1. This will be automatically applied when updating the firmware.
- Fixed a bug where brewblox-ctl would not create downsampling rules in history (only display 4.5 hours in graphs)
- The graph widget can now be displayed fullscreen
- Graphs now have preset buttons for displayed period (duration to now: 10m, 1h, 1d, 7d, 14d, 30d)
- Blocks now display whether their values are set by other blocks (eg. PWM controlled by PID).
- When a PID is disabled, it will stop overriding the setting of its output block.
- PWM and offset actuator can now be disabled separately. This allows manually setting their target.
- PWM now supports a 100Hz mode when controlling digital pins.
  - This can be used for driving DC pumps or fans.
  - This will be triggered automatically when the period is set to less than 1s.
  - OneWire actuators still have a minimum period of 1s.

Apart from these changes, we're working on the implementation of a drag-n-drop interactive display of a brewery - flows included.
https://brewpi-ui-demo.herokuapp.com/processview/herms-automated-valves is the prototype and proof of concept. The BrewBlox implementation will allow users to recreate their own setup, and control / view their blocks in the display.

When the most important features are included, we will start drawing more attention to it in the UI, and add it to the BrewPi classic wizard.

For those interested in an early preview: it is creatable as the `Process View` widget.

## Edge release 2019/03/11

This release includes changes to the firmware. To update, please run both `brewblox-ctl flash`, and `brewblox-ctl update`.

- The Spark LCD can now display temperatures as either Celsius or Fahrenheit. This is configurable in the Display Settings widget.
- Added a wrapper in brewblox-ctl to make HTTP request commands significantly shorter.
- Dashboards are now displayed as a list of cards on mobile devices. This eliminates clipping, but dashboard editing is disabled.
- Fixed a bug where you no longer could show/hide single values in graphs by (double) clicking.
- Graph values mapped to the right axis are now indicated by having a different color title in the legend.
- Fixed a bug where Spark Photon devices would not be discovered over USB.
- Added the `--discovery=all|usb|wifi` argument for the Spark service. This allows specifying connection type without hard-coding the address. Defaults to "all".
  - This can be used in combination with `--device-id`.