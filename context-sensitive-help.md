---
# Page settings
layout: default
keywords:
comments: false

# Hero section
title: Context Sensitive Help
description: Welcome brave explorer to the Bulk Delete context sensitive help page. You most likely navigated to this page by clicking the help icon in Business Central (the one that looks like a question mark) and then clicking a link under the About apps on this page section. If the page you were looking at has a special topic dedicated to that page, you will have been taken straight to that topic heading when you clicked the link. If there is no dedicated help topic for the page you were on, you will have been shown the top of this page and will be reading this text, probably wondering why you are here, and what it was you were trying to do before you arrived.

# Author box
author:
    title:
    title_url: 
    external_url: 
    description: 

# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Usage Scenarios
        url: /usage-scenarios
    next:
        content: End User License Agreement
        url: /eula
---

# Customer List

![Image showing the Bulk Delete action on the Customer List page](/screenshots/contexthelp/CustomerList.png)

A new action has been added to the **Customer List** page that will attempt to delete the selected records. If any of the records failed to delete you will be asked if you want to see the error messages for each of the records.

# Delete Package

A delete package represents a collection of tables that will be deleted in the order in which they appear on the subpage. The card page comprises three parts: 

- **General** tab which includes the same fields described in the [Delete Packages](#delete-packages) list page.
- **Package Lines** which allows tables to be added to the package.
- **Package Line Details** FactBox which shows details for the selected line such as the count of records matching the filters and how the filters are resolved.

The page includes the following actions.

## ⏵ Delete Now

Attempts to delete the records for the tables and filters specified on the delete package lines. You will be prompted to confirm the delete before it begins. Only users with a license can use this action.

<div class="callout callout--info">
Only users with a Standard Bulk Delete license assigned can run a delete package. Please contact your partner to obtain a valid license or follow the online help topic to learn how to obtain a license.
</div>

For details on how to obtain a license, see [Install Guide: Install With a License](/BulkDelete/install-guide/#install-with-a-license)

The delete now action does not show a progress indicator as it was found that this slowed the delete process. You can process this and all other delete packages as a job queue entry by creating a job queue entry with a Codeunit 71922936 BC_ProcessAvailablePackages. See [Usage Scenarios: Background Processing via the Job Queue](/BulkDelete/usage-scenarios/#background-processing-via-the-job-queue) for more details.    

## ⏵ Refresh

The count of records that match the filters is determined through a page background task. When the number of records in a table hits the tens of millions level, even an operation as simple as counting the records can take many seconds to complete. The background task allows the page to load without waiting for the count to be calculated. The **Refresh** action allows you to force the recalculation of the count. 

## ⏵ Add Delete Run History Line

This action adds a new package line to delete the run history for this package with a filter to keep only the last week's data. For more details of what this does see [Usage Scenarios: Keep Your Database Tidy](/BulkDelete/usage-scenarios/#keep-your-database-tidy). 

## ⏵ Reorder Lines

Launches a page with options to move line up and down to change the processing order for the lines in this package[^1].

## ⏵ Filters

This action launches the filters page for the current package line. It works the same as using the drill down on the **Is Filtered** field.

## ☰ Fields

### General

| Field | Description |
|-------|-------------|
| Code  | Specifies the unique code for the bulk delete package. |
| Package Name | Specifies the name of the bulk delete package. |
| Runs | Specifies the count of run records for this delete package. You can use the drill-down on this field to show the **Delete Package Runs** page which provides the history of each time the delete package has been processed. |
| Job Queue Filter | Specifies whether this package is available for processing in the Job Queue codeunit or is excluded from processing. To process entries via the job queue, create a job queue entry for Codeunit 71922936 BC_ProcessAvailablePackages. This will find any delete packages with a **Job Queue Filter** field set to **Available for Processing** and process the package in the background. One single job queue entry will process all available packages, however you can use the Parameter String field on the job queue entry to provide additional filters that will be applied to the delete package code. |

### Package Lines

| Field | Description |
|-------|-------------|
| Table ID | Specifies the ID of the table to delete records from. Use the lookup option to select from a list or search for a specific table. |
| Table Name | Specifies the name of the table to delete records from. This field is calculated automatically based on the value of Table ID. |
| Delete Action | Specifies the action to take when processing this line. Delete and Log will write a log record for every successful or failed delete attempt. Delete Only will only write a log record for failed attempts. Truncate will use the truncate option on the table which can delete a large number of records extremely quickly but will not use the validation logic. This option can only be used in a Sandbox environment. |
| Is Filtered | Specifies that there are filters for this table. You can use the drill down on this field to open the filters page to allow the filters to be changed. The Resolved Filters field on the Package Line Details FactBox will show how the values entered into all filters have been resolved for the currently package line. |
| Suspend After (mins) | Specifies the number of minutes after which the bulk delete request will be suspended. This field will default to 5 for every new line, but can be edited to any value that is greater than or equal to zero. This allows you to control how much time the system should spend processing a delete package line before it goes on to the next line. If a delete package line is still being processed when the duration reaches the suspend after value, the run will be suspended and an appropriate status will be set. The records that were deleted prior to suspension will remain deleted. If you use the value zero in the **Suspend After (mins)** field, the package line will be skipped without processing any deletes. This is a useful way to temporarily "remove" lines from a package. |
| Delete Runs | Specifies the number of delete runs that have been performed for this package line. Every time a package is processed, the line will get another run created which provides details of duration, records per minute and information on how many records were processed. |

### Package Line Details

| Field | Description |
|-------|-------------|
| Count | Specifies the count of records that match the resolved filters for the currently selected package line. This value is calculated when the current package line changes or the filters are changed, but can be manually refreshed by using the **Refresh** action. |
| Resolved Filters | Specifies the resolved filters that are applied to this package line. Resolved filters have placeholders and date formulae resolved. |

# Delete Package Line Filters

The Delete Package Line Filters page allows a filter to be set for any field on the table that is used on the current Delete Package Line. For more details on how to use this page, see the [Usage Scenarios: Set Filters](/BulkDelete/usage-scenarios/#set-filters) topic.

# Delete Package Line Runs

This page shows the runs that occurred (and still remain) for a given delete package line. Every time a user processes a delete package either directly or through a job queue entry, a new delete package line run is created for each line. This page shows you the history of how many records were processed, how long it took and provides access to any messages for individual records.

## ☰ Fields

| Field | Description |
|-------|-------------|
| Package Code  | Specifies the unique code for the delete package. |
| Line No. | Specifies part of the unique identifier for this delete package line and also determines the order in which lines will be processed. |
| Run No. | Each time a package is processed, a new run number is allocated. This field links the delete package line run back to the delete package run. |
| Table ID | A copy of the Table ID from the delete package line that was processed on this run. |
| Table Name | The name of the table that matches the Table ID. |
| Started At | The date and time that the processing of this line started. |
| Ended At | The date and time that the processing of this line ended. |
| Status | Shows the status of the processing of this package line. |
| Count at Start | Specifies the count of records that match the resolved filters for this line at the start of the run. |
| Count at End | Specifies the count of records that match the resolved filters for this line at the end of the run. |
| Run Duration | Calculated as the difference between the Started At and Ended At fields. |
| Records/Min | The number of processed records (Deleted OK Count and Delete Error Count) divided by the number of minutes it took to process the records. This can be used to estimate how long it might take to process a line in the future. |
| Delete Action | A copy of the delete action that was specified when this line was processed. |
| Deleted OK Count | A count of the number of records that were deleted OK. |
| Deleted OK Log | When the delete action is Delete and Log, a record of successful delete attempts will be saved. This field shows a count that can be used to drill down to show the successful delete attempts. |
| Delete Error Count | A count of the number records that failed to delete. |
| Failed to Delete Log | If the record delete attempt failed, a record delete attempt record is written. This is the total number of failed record delete attempts for this package line run. The drill down can be used to show the failures and the error message that will help to understand why the delete failed. |
| Resolved Filters | Specifies the filters that were applied to the table at the time the line was processed. |
| Error Message | When the truncate delete action is used, this field will show an error if an attempt was made to truncate records in a non-sandbox environment or will show any error message that the attempt to truncate returned. |

# Delete Package Runs

This page shows a list of runs for delete packages. The page can be run from the drill down on the delete package page or alone to show the full history of delete runs.

## ☰ Fields

| Field | Description |
|-------|-------------|
| Package Code  | Specifies the unique code for the delete package that this run relates to. |
| Run No. | Specifies the unique number that identifies this run for the delete package. |
| Started At | Specifies the date and time at which this delete package run started. |
| Ended At | Specifies the date and time at which this delete packated run ended. |
| Deleted OK Log | When the delete action is Delete and Log on a delete package line, a record of successful delete attempts will be saved. This field shows a count that can be used to drill down to show the successful delete attempts for all lines within this package. |
| Failed to Delete Log | If a record delete attempt failed, a record delete attempt record is written. This is the total number of failed record delete attempts for this run. The drill down can be used to show the failures and the error message that will help to understand why the delete attempts failed. |
| Lines | Specifies the number delete package line runs for this delete package run. The value can be used to drill down to show the realted delete package line runs. |

# Delete Packages

The delete packages page shows a list of delete packages in the system. A delete package is a collection of tables that will be deleted in the order they appear on the delete package lines subpage from the [Delete Package](#delete-package) card page.

In addition to being the place where you can manage your list of packages, create new packages and delete a packages, there are additional actions as follows.

## ⏵ Delete Selected

This action allows you delete multiple delete packages at once. Simply select the packages you want to delete and then select **Delete Selected**. The system will prompt to confirm you want to delete the selected packages. This will also delete all related lines and filters but not remove the logs which provides the history of which deletes succeeded or failed.

## ⏵ Export Selected Packages

This action will export the package definitions for the selected packages to a file which you can then import into another environment. The export format is a simple JSON file which uses the hierarchy of an export can contain many packages. Each package can contain many lines. Each line can contain many filters. The file name will contain the data and time the export was made.

## ⏵ Import Packages

The **Import Packages** action will import a JSON file that was previously created using the **Export Selected Packages** action. Importing a file will overwrite the existing packages, although if any of the packages in the file have the same code as existing packages, you will be asked if you want to continue.

## ☰ Fields

| Field | Description |
|-------|-------------|
| Code  | Specifies the unique code for the bulk delete package. |
| Package Name | Specifies the name of the bulk delete package. |
| Runs | Specifies the count of run records for this delete package. You can use the drill-down on this field to show the **Delete Package Runs** page which provides the history of each time the delete package has been processed. |
| Job Queue Filter | Specifies whether this package is available for processing in the Job Queue codeunit or is excluded from processing. To process entries via the job queue, create a job queue entry for Codeunit 71922936 BC_ProcessAvailablePackages. This will find any delete packages with a **Job Queue Filter** field set to **Available for Processing** and process the package in the background. One single job queue entry will process all available packages, however you can use the Parameter String field on the job queue entry to provide additional filters that will be applied to the delete package code. |

# Fixed Asset List

A new action has been added to the **Fixed Asset List** page that will attempt to delete the selected records. If any of the records failed to delete you will be asked if you want to see the error messages for each of the records.

# Item List

A new action has been added to the **Item List** page that will attempt to delete the selected records. If any of the records failed to delete you will be asked if you want to see the error messages for each of the records.

# Record Delete Attempts

This page shows the results of an attempt to delete a records from a table. Depending on the delete action that was allocated to the delete package line this will either show errors only or errors and successful delete attempts.

## ☰ Fields

| Field | Description |
|-------|-------------|
| Sort Text  | Shows the table name followed by the primary key (unique identifier) fields which helps to identify an individual record. |
| Status | Can be Deleted OK or Error (and for a very brief period of time can be Pending) |
| Error Message | If the delete attempt failed, the error message that explains the failure is stored here. |

# Reorder Package Lines

This page is used to change the sort order of package lines in a delete package. The order the lines appear in the package (which is determined by Line No.) will also determine the order in which the lines are processed. Since the lines are processed sequentially, it might be important to you that records from some tables are delete before records from other tables. The page contains fields that show the delete package line (but are non-editable) and has actions to **Move Up** and **Move Down** which will move the currently selected record either up or down in the list.

# Vendor List

A new action has been added to the **Vendor List** page that will attempt to delete the selected records. If any of the records failed to delete you will be asked if you want to see the error messages for each of the records.

# Bulk Delete Request Card

<div class="callout callout--warning">
The new version of Bulk Delete uses <b>Delete Packages</b> which will replace the old <b>Bulk Delete Request</b> options. You should transfer your bulk delete requests to a delete package if you wish to continue using the background delete features as the bulk delete request feature will be removed in a future release.
</div>

This page has been replaced by [Delete Package](#delete-package).

# Bulk Delete Requests

<div class="callout callout--warning">
The new version of Bulk Delete uses <b>Delete Packages</b> which will replace the old <b>Bulk Delete Request</b> options. You should transfer your bulk delete requests to a delete package if you wish to continue using the background delete features as the bulk delete request feature will be removed in a future release.
</div>

This page has been replaced by [Delete Packages](#delete-packages).

# Delete Requests

<div class="callout callout--warning">
The new version of Bulk Delete uses <b>Delete Packages</b> which will replace the old <b>Bulk Delete Request</b> options. You should transfer your bulk delete requests to a delete package if you wish to continue using the background delete features as the bulk delete request feature will be removed in a future release.
</div>

This page has been replaced by [Record Delete Attempts](#record-delete-attempts).


---

[^1]: We would love to have made the reorder option a part of the delete package lines page, but it was simply not possible because a subpage is not able to call back to the parent page to which it belongs. Shame 🙁.
