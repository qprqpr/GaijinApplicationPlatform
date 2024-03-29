---
title: Configs Management
---

# Config Management

Config Management – the general tab for working with game services configs.

![Config Managment Tab](./images/config-management.png)

It contains tabs with all game configs and [deploy](#deploy) tab.

## Config list

There are different types of configs:

[Multi element configs](#multi-element-config):
* Stats        [(see format)](../configs-format/stats-config-format.md)
* Unlocks      [(see format)](../configs-format/unlocks-config-format.md)
* Modes        [(see format)](../configs-format/modes-config-format.md)
* Tables       [(see format)](../configs-format/tables-config-format.md)
* Triggers
* Items

[Single configs](#single-config):
* Contacts     [(see format)](../configs-format/contacts-config-format.md)
* Externals

[Scripts configs](#scripts-config):
* Scripts      [(see format)](../configs-format/profile-config-format.md)

### Multi-element config
Multi-element config contains array of similar elements, like stat, unlock, table, etc. All multi-element configs are editing in one way.
Consider stat config editing:

#### Adding new config element
For adding new config element, click button with “Add” text. After click a new config element will be added.
New config element automatically filled with default parameters.
![Add element](./images/add-element.png)
You need to fill the name field and press save button. Also you can change another fields.
![Add element](./images/add-element_save.png)
:::caution
The changes aren't saved until Save button not pressed. If page reload all unsaved changes will be missed.
:::

#### Deleting element
To delete config element, click Remove button. Then you must confirm your action in the modal window.
![Remove element](./images/remove-element.png)

#### Editing element
To edit config element, use [Code Editor](#code-editor).
![Edit element](./images/edit-element.png)
To open Code Editor for Config element, click to arrow in the Code Editor column.
![Edit element open](./images/edit-element-open.png)
Data are edited as in a regular text editor, with [code-complete](#code-complete), [errors marker](#errors-marker) and [changes marker](#changes-marker)

#### Common actions for config elements
You can change some config elements and save the click to button “Save all”
![Save all elements](./images/save-all-elements.png)
To edit the common values ​​of several config elements, select them by checking the appropriate checkboxes
![Check elements](./images/check-elements.png)
Click on the “Change selected” button. In the window that opens, edit the necessary values.
![Change values for checked rows](./images/change-values-for-checked-rows.png)
To remove a config parameter, use the parameter with value `null`
![Delete values for checked rows](./images/delete-values-for-checked-rows.png)
To delete selected elements click to button “Delete selected”
![Delete selected](./images/delete-selected.png)
You can upload config from file and download to file with buttons “Upload config” and “Download config”
![Upload and download config](./images/upload-downoad-config.png)

#### Filters
To open the string input for filtering, click the button with the filter icon.
![Open filter button](./images/open-filter-button.png)
Filters available values:
Equality/inequality - matches records where value of the field is equal/unequal to specified value, ex.: `foo=42, foo!=-3.14, foo!="a string", foo=true, foo=false`
Regex - if field value is a string, matches it against specified regex, ex.: `foo=/^https?:\/\// foo=/^https?:\/\//`
Comparison `(<, >, <=, >=)` - if field value is a number, compares it with specified value, ex.: `foo>42, foo<=-3.14`
Presence - matches records where specified field is present/missing, ex.: `foo exists, foo !exists`
Array - matches records where the value of a field equals to any value in the array, ex.: `foo in [42, -3.14, "bar", true, false]`
Complex queries can be constructed using logical AND (&) and OR (|) operators, ex.: `foo=42&bar exists`
Filters can be grouped by parenthesis, ex.: `foo=42&(bar exists|foo<100)`
Operator precedence (from highest to lowest): `(), &, |`
Spaces may be omited where possible: `foo = 42 & bar in [1, 2, 3] | baz exists` is equivalent to `foo=42&bar in[1,2,3]|baz exists`
Array may have trailing comma: `[1, 2, 3,]` is equivalent to `[1, 2, 3]`
To search by date, use the timestamp format `create_t=1708437468`

You always can use clue to watch filters available values
![Open filter clue](./images/open-filter-clue.png)
To filter by dates you need to use timestamp format. To get date in timestamp format click to button into configs row beside data value.
![Copy timestamp button](./images/copy-timestamp-button.png)
The date in timestamp format will be copy to clipboard and you can use it in filters.

### Single config
Single config is a json object which may contains fields with different type.
To edit single config use [Code Editor](#code-editor).
![Single config edit](./images/single-edit.png)
Data are edited as in a regular text editor, with [code-complete](#code-complete), [errors marker](#errors-marker) and [changes marker](#changes-marker)

### Scripts config
Profile server use scripts configs on [daScript](https://dascript.org/) language.
More information about [script config format](../configs-format/profile-config-format.md).

#### Upload/Download scripts archive
To upload scripts use zip archive containing folder with scripts.
You must create zip archive by you self and than upload it using `Upload Zip` button.
You can download scripts zip archive using `Download Zip` button.
Вы можете загрузить конфиги из директории используя кнопку Upload from directory
![Upload scripts](./images/scripts.png)

Под кнопками оторбражаются загруженные файлы в виде дерева

### Code Editor
#### Code Complete
Code completion allows complete all fields for config element or prompts the possible values.
To initiate code compleate press `Ctrl+Space`
Field name code complete:
![Code complete](./images/code-complete-field.png)
Value code complete:
![Code complete](./images/code-complete-value.png)

#### Errors marker
If Configs editor contains errors the Save button is disabled. Line with error marked with a red circle.
To read the error message move mouse arrow over the red circle.
![Mark error](./images/mark-error.png)

#### Changes marker
Changed parameters marked with a special symbol (pencil) for simpler tracking changes.
![Mark change](./images/mark-change.png)

## Deploy configs
To deploy configs to the services use Deploy menu item.

![Deploy](./images/deploy.png)

The deploy window has 2 tabs:
* Tags List
* Compare

### Tags List
Еag list tab provides an interface for working with tags: adding tags, uploading configs from tag, exporting data from tag, etc.
![Tag list](./images/tag-list-tab.png)

#### Fast deploy configs
The easiest way to deploy configs to services is `Fast update`.
![Fast deploy](./images/fast-deploy.png)
This will directly upload current configs to services, just like from a master in git.
Fast update automatically create special tag `_fast`. This tag rewrite each time you use `Fast update`.
![Fast deploy](./images/fast-deploy-tag.png)

'Fast update' is useful on test circuit, but this is not good idea for production.
The best way - save the configs in a tag first, as add git tag. And then deploy to services from tag.
In the future, you can reuse this tag, for deploy or restore configs from it.

#### Add new tag
To add new tag from current configs press `Add tag`.
:::note
Tag name must be unique.
:::
![Add tag](./images/add-tag.png)

#### Deploy configs from tag
To deploy configs from tag click `Update configs` button and than confirm deploy:
![Deploy tag](./images/deploy-tag.png)
You can see updates progress information after launching the update for any configs:
![Deploy progress](./images/deploy-progress.png)
Last deployed tag shows in the top of the table:
![Last deployed tag](./images/last-deployed-tag.png)

#### Import tag
Also you can import configs, press `Import tag` button. Set the tag name and paste configs text to the modal window:
![Import tag data](./images/import-tag.png)

#### Copy configs to buffer
To get configs from tag use `Copy to buffer` button:
![Copy to buffer](./images/copy-tag-to-buffer.png)
Also you can copy to buffer current configs:
![Copy current to buffer](./images/copy-current-to-buffer.png)
This is useful to transferring tags between different game environments(test, staging, production) or between different game.

#### Restore configs from tag
You can replace all current configs to configs from tag, just press 'Restore configs` button:
![Restore tag](./images/restore-tag.png)

#### View tag configs
Click to arrow button to display tag configs:
![View tag](./images/view-tag.png)

### Compare
Select "Compare" tab to view diff between 2 tags:
![Compare tab](./images/compare-tab.png)
Choose Before and After tags:
![Compare tags](./images/compare-tags.png)
You can see the difference in this section after clicking on the block with changing:
![Tags diff](./images/tags-diff.png)
A large number of equal lines are hidden in differentials. If you want to see more equal rows, select the value in the context selection:
![Tags diff rows](./images/tags-diff-rows.png)
