# Concepts

Tvheadend is operated primarily through a tabbed web interface. There are some basic navigation concepts that will help you use it effectively:

## **Page Structure**

* The web interface uses tabs with similar functions grouped together. Tabs for major configuration functions are located on the top row, with tabs for configuration items related to the currently selected major function located on the row below. In some cases a third row of config options will be shown.
* Most tabs have display a menu bar with _Add, Save, Edit, Undo_ functions and a spreadsheet-like grid below. Grid items are frequently editable.
* Most configuration items are in this grid. However, some item-specific configuration is accessed through the _Add_ and _Edit_ dialog boxes. For example: the main network configuration tab grid covers parameters common to DVB-S, DVB-T, DVB-C and IPTV networks, but configuration like FEC rolloff or mux URL is only present in dialogs for networks that need these values.

## **Displaying & Manipulating Columns**

* Some columns are hidden. If you hover the mouse over a column heading a down-arrow will show, and when clicked a drop-down menu appears allowing you to select which columns are visible and which columns are hidden.
* The drop-down menu also allows you to sort results. You can also sort columns by clicking on the column header: first click will sort ascending and a second click will reverse the sort (descending).
* The same drop-down menu also allows you to filter results using basic string pattern matching.
* Columns can be rearranged by dragging the column header to a new position.
* Columns can be resized by dragging the edges of the column header to the width position required.

## **Editing Fields**

* To edit a cell in the grid, double click on it and make changes. After a cell has been changed, a red flag or triangle appears in the top-left corner to indicate it has been changed. Changes can be kept (click _Save)_ or discarded (click _Undo_).
* To change a checkbox or radio button, click once.
* To add a new entry press the _Add_ button. The new (empty) entry will be shown in the interface but will not be stored in the server configuration until values are added, the configuration is marked as enabled, and then saved. Changes are applied when saved, not when edited.
* Most grid views support ctrl+click to select multiple fields at the same time, and shift+click to select field ranges.
