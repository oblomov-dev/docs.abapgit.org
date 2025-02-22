---
title: Development Guidelines
category: read-first
order: 20
---

## Object Types

abapGit is merged into a [stand-alone version](/user-guide/getting-started/install.md). For this reason, the only allowed object types for *new* repository objects are classes and interfaces. In particular, function groups or modules must *not* be included.

Exceptions for existing objects:
- Transaction `ZABAPGIT`
- Program `ZABAPGIT` and includes
- Function group `ZABAPGIT_PARALLEL` for parallel serialization (only available in the developer version)
- MIME objects `ZABAPGIT_*` for UI (CSS, JS, and fonts)

## Conventions

### Naming

#### Object Prefixing

Classes and interfaces are prefixed using `zcl_abapgit_` or `zif_abapgit_` (`zcx_abapgit_` for exception classes, `lcl_` and `ltcl_` for local and test classes). The description of objects should begin with `abapGit - ...`. 

#### Variable Prefixing

Variables are prefixed using the standard setting in [abapOpenChecks Naming Conventions](https://docs.abapopenchecks.org/checks/69/)

### Downport

#### Syntax

abapGit is targeted for [version 7.02](https://help.sap.com/doc/abapdocu_latest_index_htm/latest/en-US/index.htm?file=abennews-71.htm) and higher. Therefore, the code must only contain expressions and statements that work on 7.02.

[abaplint](https://abaplint.org) will automatically check every pull request for language syntax that is compatible with 7.02.

#### Standard Objects

The code must only reference standard SAP objects (classes, interfaces, DDIC types) that exist in version 7.02 and higher. Referencing objects that do *not* exist in 7.02 creates syntax errors and therefore requires using dynamic ABAP. DDIC types that do *not* exist in 7.02 should be replaced by local type definitions.

### Formatting the Source Code

#### Line Width

The maximum width of ABAP source code should be set at 120 characters per line and is checked during linting.

#### Pretty Printer

Use pretty-printer, keywords upper case + indentation, [abapOpenChecks](https://docs.abapopenchecks.org/checks/06/) can be used for checking this.

### Dynpros

For the user interface, we are moving towards everything in HTML, i.e. new Dynpro screens or the use of Dynpro screens and popups should *not* be added to the source code.

### abaplint

Pull requests must pass all abaplint configured checks before they can be merged. You find the current rules in [abaplint.json](https://github.com/abapGit/abapGit/blob/main/abaplint.json).

::: info
You can view abaplint findings directly in abapGit using an [extension](https://github.com/Marc-Bernard-Tools/ABAP-Lint-Ext-for-abapGit).
:::

### Internationalization (I18N)

abapGit supports only the English language. Neither objects nor text literals are translated. Therefore, all objects shall be set to English as the original language, and text literals in the code shall be maintained in English. 

Since there's only one language, using the `##NO_TEXT` pragma is not required and will actually lead to lint errors. The exceptions are global class and interface definitions, where the pragmas are added automatically by `SE24/SE80`. 
