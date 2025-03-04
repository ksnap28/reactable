# reactable 0.2.3.9000

This release upgrades to a new major version of React Table
([#35](https://github.com/glin/reactable/issues/35)), which introduces many
new features, improvements, and bug fixes. Backward compatibility was kept
where possible, but note that there are several breaking changes.

### New features

* Column group headers can now be resized.
* Column group headers and filters are now sticky. Previously, only column
  headers were sticky ([#107](https://github.com/glin/reactable/issues/107)).
* Expanded rows now stay expanded on sorting, filtering, and pagination changes.
  Previously, expanded rows were always collapsed on sorting and pagination
  changes, and incorrectly persisted on filtering changes
  ([#39](https://github.com/glin/reactable/issues/39)).
* Aggregated rows can now be selected when multiple selection is enabled.
* `colDef()` gains a `grouped` argument to customize rendering for grouped cells
  in `groupBy` columns ([#33](https://github.com/glin/reactable/issues/33),
  [#94](https://github.com/glin/reactable/issues/94),
  [#148](https://github.com/glin/reactable/issues/148)).
* JavaScript render functions and style functions receive several new properties:
  * `rowInfo.expanded` and `cellInfo.expanded` indicating whether the row is expanded
  * `cellInfo.selected` property indicating whether the cell's row is selected
  * `state.page`, `state.pageSize`, and `state.pages` for the current page index,
    page size, and number of pages in the table
* JavaScript render functions for cells, headers, footers, and row details
  can now access the table state using a new `state` argument
  ([#88](https://github.com/glin/reactable/issues/88)).
* Custom cell click actions can now access the table state using a new `state`
  argument.

### Breaking changes

* When expanding grouped rows, sub rows are now paginated and included in the
  row count. Use `reactable(paginateSubRows = FALSE)` to exclude sub rows from
  pagination like before.
* The row selection column is now always placed as the first column in the
  table, even before the `groupBy` and row details columns
  ([#71](https://github.com/glin/reactable/issues/71)).
* Increased the default width of the row selection column to match the row
  details column (45px).
* When both `columnGroups` and `groupBy` arguments are provided, `groupBy`
  columns are no longer added to a column group automatically
  ([#87](https://github.com/glin/reactable/issues/87)).
* The `defaultGroupHeader` argument in `reactableLang()` is now deprecated and
  no longer used. Use the `columnGroups` argument in `reactable()` to customize
  the column group header for `groupBy` columns.
* The `state.expanded` property has been removed from JavaScript render
  functions and style functions. To check whether a row is expanded, use
  `rowInfo.expanded` instead.
* The `rowInfo.page` and `cellInfo.page` properties have been removed from
  JavaScript render functions and style functions. To get the current page
  index of the table, use `state.page` instead.

### Minor improvements and bug fixes

* Setting `show = FALSE` as a default value in `defaultColDef()` now works
  (@csgillespie, [#105](https://github.com/glin/reactable/pull/105)).
* Using a single value for `pageSizeOptions` in `reactable()` now works.
* Column resizing is now limited by the min and max width of the column.
* Column group headers and filter cells in fixed height tables now display
  properly in Safari, Chrome, and the RStudio Viewer
  ([#76](https://github.com/glin/reactable/issues/76)).
* In `reactable()`, `defaultExpanded = TRUE` now expands all rows in the table,
  not just rows on the first page.
* In `reactable()`, `defaultExpanded = TRUE` now works when column groups are present.
* Aggregated cell values are now recalculated when filtering or searching the table.
* Aggregate functions now always take the unaggregated values in the column.
  Previously, if there were multiple `groupBy` columns, aggregate functions
  could take aggregated values which could produce inaccurate calculations
  (e.g., when calculating the mean of values).
* The `"max"` and `"min"` aggregate functions now work on dates, date-times,
  and strings ([#130](https://github.com/glin/reactable/issues/130)).
* Column formatters no longer apply to empty aggregated cell values.
* Searching now properly ignores the row details and selection columns.
* Selected rows now reset when the table data changes in Shiny
  ([#110](https://github.com/glin/reactable/issues/110)).
* When selecting rows, errors from other Crosstalk widgets no longer cause the
  table to disappear.
* HTML widgets and HTML dependencies in nested tables now render correctly
  ([#125](https://github.com/glin/reactable/issues/125)).
* Row expand buttons now set the `aria-expanded` attribute to indicate expanded
  or collapsed state. The default label for row expand buttons is now
  "Toggle details" instead of "Expand details" or "Collapse details".
* `reactableLang()` gains the `groupExpandLabel` and `groupCollapseLabel`
  arguments to customize the accessible labels for row group expand buttons.
* Cells in the row names column are now marked up as row headers for assistive
  technologies.

# reactable 0.2.3

### Bug fixes

* Fixed a character encoding issue in the documentation.

# reactable 0.2.2

### Bug fixes

* Headers in fixed height tables now display properly in Safari, Chrome, and
  the RStudio Viewer ([#76](https://github.com/glin/reactable/issues/76)).

# reactable 0.2.1

### New features

* `updateReactable()` gains a `data` argument to update the data of a reactable
  instance in Shiny ([#49](https://github.com/glin/reactable/issues/49)).

### Bug fixes

* Row selection columns now display correctly in tables with column groups
  ([#52](https://github.com/glin/reactable/issues/52)).
* `defaultSelected` now works correctly with Crosstalk linked selection.
* Crosstalk selection and filtering now works with nested and dynamically
  rendered tables [#57](https://github.com/glin/reactable/issues/57)).
* Tables now display correctly for Crosstalk `SharedData` objects with zero or one rows.
* Shiny UI elements in expanded row details are now properly removed when
  collapsed on page changes.
* `colFormat()` now always formats numbers as a localized string when `locales`
  is specified.
* Table rows no longer stretch to fill the height of the container
  ([#69](https://github.com/glin/reactable/issues/69)). To make rows stretch
  again, use a theme like `reactableTheme(tableBodyStyle = list(flex = "auto"))`.
* Multi-sorting no longer selects text in column headers.

# reactable 0.2.0

### New features

* `reactable()` now supports linked selection and filtering with Crosstalk-compatible
  HTML widgets ([#46](https://github.com/glin/reactable/issues/46)).
* `reactable()` gains a `theme` argument to customize the default styling of a table.
* `reactable()` gains a `language` argument to customize the language strings in a table
  ([#24](https://github.com/glin/reactable/issues/24)).
* `reactable()` gains a `defaultSelected` argument to set default selected rows.
* `reactable()` gains a `defaultExpanded` argument to set default expanded rows
  ([#23](https://github.com/glin/reactable/issues/23)).
* New `updateReactable()` function to update the selected rows, expanded rows, or
  current page of a reactable instance in Shiny ([#20](https://github.com/glin/reactable/issues/20)).
* New `getReactableState()` function to get the state of a reactable instance in Shiny
  ([#20](https://github.com/glin/reactable/issues/20)).
* `colDef()` gains a `"median"` aggregate function to calculate the median of numbers
  ([#30](https://github.com/glin/reactable/issues/30)).
* The row selection column can now be customized using `".selection"` as the column name
  ([#19](https://github.com/glin/reactable/issues/19)).
* In `reactable()`, the `rowClass`, `rowStyle`, and `details` JavaScript functions
  now receive a `rowInfo.selected` property indicating whether the row is selected
  ([#20](https://github.com/glin/reactable/issues/20)).

### Breaking changes

* The `selectionId` argument in `reactable()` will be deprecated in a future release.
  Use `getReactableState()` to get the selected rows of a table in Shiny instead.

### Bug fixes

* General accessibility improvements, particularly for screen reader users.
* Table searching now works correctly when row selection is enabled.
* `colFormat(date = TRUE)` now formats `YYYY-MM-DD` dates correctly ([#38](https://github.com/glin/reactable/issues/38)).
* `colFormat(percent = TRUE)` now works correctly when viewing tables in IE11.
* Cell click actions now work for all cells in aggregated rows.
* Aggregated cells in columns with row details no longer throw an error when clicked.
* In `colDef()`, the `class` and `style` R functions now handle list-columns correctly.
* Column headers now truncate long text properly.
* Footers now display properly in fixed height tables for Safari and Chrome ([#41](https://github.com/glin/reactable/issues/41)).
* Dark themes no longer affect text color in RStudio R Notebooks ([#21](https://github.com/glin/reactable/issues/21)).
* Checkboxes and radio buttons now align with multi-line text in selectable tables.
* Text selection now works in column headers.
* Row striping and highlighting styles no longer affect nested tables.

# reactable 0.1.0.1

* Updated tests for compatibility with R 4.0.0.

# reactable 0.1.0

* Initial release.
