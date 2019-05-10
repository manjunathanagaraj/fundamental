# SAP Theme Parameters Mapping

### Goals
- We want to use the SAP unified theme parameters to implement the default Fiori 3 look and feel. This will allow Fundamentals to easily opt-in to centrally distributed user themes and customized customer themes available with SAP Theme Designer.
- We want to maintain the ability to modify the Fundamentals theme irrespective of the default theme by defining a small number of variables.

### Proposal



Consuming base params from theme designer or NPM package works well but some changes will be required ...
- Distribute SASS version of the LESS params, change `@` to `$`
- Order of SASS variables matter, must be defined before being referenced
- Include only color values, no fonts, no sizes
- Derived values should be systemized into shades of primary colors, theme params include:
	- 41 `darken()` values
	- 18 `lighten()` values
	- 23 `contrast()` values (SASS does not support this function)
	- 1 `fade()` value

Fundamentals settings can be further separated by colors, grid, etc. These are themeable values that could be swapped/augmented with additional values to effect global interface changes. A `settings` directory may include:
- `colors`
- `type`
- `fonts`
- `spacing`
- `images` ?
- `motion` ?

The `root` file with the CSS custom properties shall be expanded to include all global and component variables
> ? | Should the component vars be part of the component files and assembled by `root.scss`


### Migration

**Step 1**
Map SASS params to quickly get a dark theme distributed and begin gathering feedback from applications consuming the full compiled library

Requires very few updates to the existing build process

**Step 2**
Update the library toolkit to Migrate global and components variables








-----


### SAP Unified Theming
Theme palette
https://wiki.wdf.sap.corp/wiki/pages/viewpage.action?pageId=2017191746

Theme parameters
https://wiki.wdf.sap.corp/wiki/pages/viewpage.action?pageId=2017196009

### Fundamentals SASS mappings
| hex| color | param | use | notes |
|-- |-- |-- | -- | -- |
| `#354a5f` | shell-1 | `sapPrimary1` | Shell header | ✅ |
| `#d1e8ff` | shell-2 | `--sapShell_TextColor` | Interactive icons or text in the shell | ✅  |
| `#283848` | <s>shell-3</s> | `--sapShell_Hover_Background` | Shell content hover  |  ❗️ **Should be a derived color** |
| `#23303E` | <s>shell-4</s> | `--sapShell_Active_Background`, `--sapShell_Selected_Background` | Shell selected content  |  ❗️ **Should be a derived color** |
| `#7996B4` | <s>shell-5</s> | `--sapShell_InteractiveBorderColor` | Interactive shell content border |  ❗️ **Should be a derived color** |
| `#0a6ed1` | action-1 | `sapPrimary2` | Branded elements and base color for derived interaction states | ✅  |
| `#ffffff` | action-2 | <small> *Fiori params do not include global inverse values* </small> | Interaction inverse for dark backgrounds | ✅  |
| `#0854A1` | <s>action-3</s> |  |  |  ❗️ **Not used in FD** |
| `#32363a` | text-1 | `sapPrimary6` | Base color for texts and titles  | ✅  |
| `#515559` | text-2 |   | Used in FD selectively for form messages and for text-colored links like pagination and tabs | ❗️ **No matching Fiori 3 param** |
| `#6a6d70` | text-3 | `sapPrimary7` | Base color for labels, non-interactive icons and sub-titles | ✅ |
| `#74777a` | text-4 | Only `--sapField_PlaceholderTextColor` |  | ❗️ **Not used in FD** — `::placeholder` uses adjusted-color `$fd-forms-color--placeholder` |
| `#ffffff` | text-5 | <small> *Fiori params do not include global inverse values* </small> | Inverse text color for dark backgrounds | ⚠️ Theme params do not include global inverse values |
| `#edeff0` | background-1 | `sapPrimary4` | Shell background | ✅  |
| `#ffffff` | background-2 | `sapPrimary3` | Light base for containers and derived controls | ✅ |
| `#f1fdf6` | background-3 | `--sapSuccessBackground` | Success state backgrounds | ⚠️ Theme param is derived |
| `#fef7f1` | background-4 | `--sapWarningBackground` | Warning state backgrounds | ⚠️ Theme param is derived |
| `#ffebeb` | background-5 | `--sapErrorBackground` | Error state backgrounds | ⚠️ Theme param is derived |
| `#f5faff` | background-6 | `--sapInformationBackground` | Information state backgrounds | ⚠️ Theme param is derived |
| `#f4f4f4` | background-7 | `--sapNeutralBackground` | Neutral state backgrounds | ⚠️ Theme param is derived |
| `#fafafa` | neutral-1 | `--sapTile_Hover_Background`, `--sapList_Hover_Background`, `--sapList_FooterBackground` | Used in FD primarily for header backgrounds and for standard button | |
| `#e5e5e5` | neutral-2 | `--sapList_BorderColor` | Borders for table, tree | |
| `#d9d9d9` | neutral-3 | `--sapPageHeader_BorderColor`, `--sapGroup_TitleBorderColor`, `--sapToolbar_SeparatorColor` | Page section borders | |
| `#89919a` | neutral-4 | `sapPrimary5` | Borders and derived controls, popover, alert  | ✅ |
| `#107E3E` | status-1 | `sapPositiveColor` |  | ✅|
| `#E9730C` | status-2 | `sapCriticalColor` |  | ✅|
| `#BB0000` | status-3 | `sapNegativeColor` |  | ✅|
| `#6A6D70` | status-4 | `sapNeutralColor` |  | ✅|
| `#0A6ED1` | status-5 | `sapInformativeColor` |  |✅ |
| `#d08014` | accent-1 | `sapAccentColor1` |  | ✅ |
| `#d04343` | accent-2 | `sapAccentColor2`|  |  ✅ |
| `#db1f77` | accent-3 | `sapAccentColor3` |  | ✅ |
| `#c0399f` | accent-4 | `sapAccentColor4` |  | ✅ |
| `#6367de` | accent-5 | `sapAccentColor5` |  | ✅ |
| `#286eb4` | accent-6 | `sapAccentColor6` |  | ✅ |
| `#0f828f` | accent-7 | `sapAccentColor7` |  | ✅ |
| `#7ca10c` | accent-8 | `sapAccentColor8` |  | ✅ |
| `#925ace` | accent-9 | `sapAccentColor9` |  | ✅ |
| `#647987` | accent-10 |`sapAccentColor10` | | ✅ |
| `#D17F15` | accent-11 |  |  | ❗️ **No matching Fiori 3 param** |
| `#D04343` | accent-12 |  |  | ❗️ **No matching Fiori 3 param** |
| `#2B78C5` | accent-13 |  |  | ❗️ **No matching Fiori 3 param** |
| `#0F828F` | accent-14 |  |  | ❗️ **No matching Fiori 3 param** |
| `#647887` | accent-15 |  |  | ❗️ **No matching Fiori 3 param** |

### Notes

--sapPrimary1: #354a5f;
--sapShellColor: var(--sapPrimary1);
