# Super Table

Super Table is a Craft CMS field type to allow you to create powerful tables. You can utilise all your favourite native Craft field types in your tables, including Assets, Users, Entries and even Matrix. Also supports many third-party field types.

<img src="https://raw.githubusercontent.com/engram-design/SuperTable/master/screenshots/input.png" />


### Field Settings

<img src="https://raw.githubusercontent.com/engram-design/SuperTable/master/screenshots/settings.png" />

Editing a Super Table is very similar to editing a Table. You define your columns, giving them a Name and Handle, and now have the option to select any installed field type.

To edit the settings of a particular field, click on the small 'cog' icon on the far right of the table row. This will open a modal window where you can edit any settings for that field type. Don't forgot to hit Save button to save these field settings!


### Supported FieldTypes

**Craft**

* Assets
* Categories
* Checkboxes
* Color
* Date/Time
* Dropdown
* Entries
* Lightswitch
* Matrix
* Multi-select
* Number
* Plain Text
* Position Select
* Radio Buttons
* Rich Text
* Table
* Tags
* Users

**Third-Party**

* [ButtonBox](https://github.com/supercool/Button-Box)
* [Linkit](https://github.com/fruitstudios/LinkIt)

...and many more. Super Table can handle just about any FieldType, the above are simply those that have been tested.


## Layout

For any Super Table, you can choose between two layout options - Row and Table. This is an option when creating your Super Table field. The Table layout will present fields vertically and in a tabular format - exactly as you'd expect from a Table field. Row on the other hand will present fields horizontally, similar to how a Matrix field works.

Which layout you choose will likely depend on what sort of fields you have in your Super Table, and the number of fields. For a Super Table containing 4 or more fields, your best option is to use the Row Layout.

To illustrate the different layout options, refer to the below, which are the same field using both Table and Row layouts.

<img src="https://raw.githubusercontent.com/engram-design/SuperTable/master/screenshots/layouts.png" />

The Row Layout also shines brightest when using inside a Matrix field as below.

<img src="https://raw.githubusercontent.com/engram-design/SuperTable/master/screenshots/rowLayout.png" />


## Static option

A Super Table field can be set to be static, which turns the field into a non-repeatable collection of fields. This can be useful for a multitude of cases where you wish to simply group a collection of fields together, and not necessarily have them repeatable.

<img src="https://raw.githubusercontent.com/engram-design/SuperTable/master/screenshots/static.png" />


## Roadmap

- Test more third-party fieldtypes, purely for a complete list.
- Add ability to collapse rows.
- New settings layout, including drag/drop, full control over field layout. Allows you to set out the field exactly as you like.
- Add template hook to allow other plugins to provide layouts for editing field.
- Allow for SuperTable-in-SuperTable - because why not.
- Support column duplication in SuperTable field settings.


## Updating from 0.3.4 to 0.3.5
The 0.3.5 update changed the way that Super Table's within Matrix fields store their content. Because two Super Tables with the same handle could be created in different Matrix fields, both these Super Table fields shared a single content table. This creates all sorts of issues when it comes to deleting your Super Table fields.

While the update will automatically rename and migrate all your Super Table content in a non-destructive fashion, you may come across a particular issue which causes the plugin update to fail. This revolves around one of the primary keys becomes too long for MySQL to handle.

If your receive the error when updating the plugin, please check out `craft/storage/runtime/logs/craft.log` for a line that looks similar to:

```
[error] [system.db.CDbCommand] CDbCommand::execute() failed: SQLSTATE[42000]: Syntax error or access violation: 1059 Identifier name 'craft_supertablecontent_NUMBER_HANDLE_elementId_locale_unq_idx' is too long.
```

If you find this error, you will need to manually rename the provided table before performing the plugin update. Simple rename the table from `craft_supertablecontent_HANDLE` to `craft_supertablecontent_NUMBER_HANDLE` with `NUMBER` and `HANDLE` obviously specific to your particular table. This will be identified in the error line in your `craft.log` file. Perform the plugin update once you have renamed these tables.


## Thanks / Contributions

Thanks go to [@brandonkelly](https://github.com/brandonkelly) and [@benparizek](https://github.com/benparizek) for their input, ideas and suggestions.


## Changelog

#### 0.3.5

- Change to content table naming when inside Matrix field. When two Super Table fields in different Matrix fields had the same handle, when one ST field was deleted, content for both would be deleted. Now prefixes tables with Matrix field id - ie: `supertablecontent_matrixId_fieldhandle`. See [notes](https://github.com/engram-design/SuperTable/blob/master/README.md#updating-from-034-to-035).
- Fix for some UI elements not initializing for Matrix > Super Table > Matrix layout [#28](https://github.com/engram-design/SuperTable/issues/28).


#### 0.3.4

- Minor visual fix for Row layout and table overflow [#24](https://github.com/engram-design/SuperTable/issues/24).
- Fix for Table layout and deleting element select items [#25](https://github.com/engram-design/SuperTable/issues/25).

#### 0.3.3

- Minor fixes to issues introduced accidentally in 0.3.2.

#### 0.3.2

- Fix for Matrix-SuperTable-Matrix field configuration and correct namespacing. Caused numerous inner-Matrix issues.

#### 0.3.1

- Fix for field labels on inner-Matrix field being hidden [#16](https://github.com/engram-design/SuperTable/issues/16).
- Latest Redactor version fixes [#3](https://github.com/engram-design/SuperTable/issues/3).
- Fix for width not being applied for columns [#15](https://github.com/engram-design/SuperTable/issues/15).
- Fix issues with multiple Matrix Configurators causing many javascript issues [see Craft 2.4.2677](https://buildwithcraft.com/updates#build2677).

#### 0.3.0

- Added composer support.
- Improved performance (thanks to [@boboldehampsink](https://github.com/boboldehampsink) and [@takobell](https://github.com/takobell))

#### 0.2.9

- Added Static option for fields. Allows for blocks to be non-repeatable [see more](https://github.com/engram-design/SuperTable#staticoption).
- Fixed validation when creating Super Table fields.
- Added option to set the 'Add a row' button text.
- Added Max Rows option.
- Added required option for fields.

#### 0.2.8

- Minor fix for Row Layout and Element Selection fields. Clicking delete on an element select would remove the entire row.

#### 0.2.7

- Full support for Matrix.

#### 0.2.6

- Added Row layout option [see example](https://github.com/engram-design/SuperTable#layout)
- Removed background colouring for cells.

#### 0.2.5

- Added width option to each column.
- Added Label field type.
- Fixed some minor validation bugs.
- Fixed namespacing issues for element-selects and some other fields inside Matrix blocks. 

#### 0.2

- Major refactor of field settings JS. Caused namespacing issues for certain field types.

#### 0.1

- Initial release.

