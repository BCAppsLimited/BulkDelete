---
# Page settings
layout: default
keywords:
comments: true

# Hero section
title: Usage Scenarios
description:  In this section you'll find a number of common usage scenarios explained in detail.

# Author box
author:
    title: 
    title_url: 
    external_url: false
    description: 

# Micro navigation
micro_nav: true

# Page navigation
page_nav:
    prev:
        content: Install Guide
        url: /install-guide
    next:
        content: Context Sensitive Help
        url: /context-sensitive-help
--- 

# Delete Selected Records

In this topic we'll cover how to perform a bulk delete on a list of items, although the same process can be followed for customers, vendors, or fixed assets using the appropriate pages.

From the **Item List** page, select the records you wish to delete by selecting multiple records as shown in the following image.

![Image showing the Item List page with the Bulk Delete Action being selected.](/screenshots/usagescenarios/ItemListBulkDelete.png)

From the Actions, select the **Bulk Delete** option. The system will display a confirmation dialog to ensure you really want to delete the selected records.

![Image showing the confirmation dialog for deleting four selected records.](/screenshots/usagescenarios/ConfirmDeleteFourItems.png)

Select **Yes** to continue with the delete. The system will attempt to delete each record in turn and record whether the delete succeeded or failed. The dialog box will show the progress of the delete action and an estimated time to complete.

If any of the selected records failed to delete, you will see a dialog box asking if you would like to review the error messages for the failed delete attempts.

![Image showing the results of the bulk delete.](/screenshots/usagescenarios/CompleteWith1OK3Fail.png)

You can review the reasons why the records failed to delete by clicking the drill down on the **Failed to Delete** count to see the **Delete Requests** page.

![Image showing the four records that failed to delete.](/screenshots/usagescenarios/DeleteRequestsWithFourErrors.png)

If you are finished with the Bulk Delete Request, you can return to the Bulk Delete Request Card and delete the record. This will prompt for deletion.

![Image showing the confirmation dialog for deleting a Bulk Delete Request record.](/screenshots/usagescenarios/DeleteBulkDeleteReqeuestConfirmation.png)

Select the **Yes** button and the system will delete the Bulk Delete Request record and the associated filter lines and results records.

# Bulk Delete Any Table

<div class="callout callout--warning">
The new version of Bulk Delete uses <b>Delete Packages</b> which will replace the old <b>Bulk Delete Request</b> options. You should transfer your bulk delete requests to a delete package if you wish to continue using the background delete features as the bulk delete request feature will be removed in a future release.
</div>

As well as creating bulk delete requests from the Items, Customers, and Vendors list pages, you can create a new Bulk Delete Request and pick from any of the available tables.

Search for the **Bulk Delete Requests** page. You should see a list of all the Bulk Delete Requests you have previously created. The page is filtered to only show requests that you created, but you can select the **All Requests** action to show requests created by other users.

![Image showing the Bulk Delete Requests list page.](/screenshots/usagescenarios/BulkDeleteRequests.png)

Click the **New** button to create a new bulk delete request.

![Image showing a blank Bulk Delete Request card.](/screenshots/usagescenarios/BlankBulkDeleteReqeustCard.png)

A new bulk delete request is created. If you know the Table Id, type the number in to the **Table Id** field, or use the drop-down to select from a list.

![Image showing using the drop-down to select a new Table Id](/screenshots/usagescenarios/SelectingANewTableId.png)

The **Filtered Records** field will update to show the number of records that match your existing filter. To set filters, click in to the **Filters** sub-page and use the assist button to select from the list of available fields.

![Image showing the filter Field No.](/screenshots/usagescenarios/SelectAFilterFieldNo.png)

Once you have selected the field number, enter a filter that should be applied to this field.

![Image showing applying a filter on Posting Date.](/screenshots/usagescenarios/FilterOnPostingDate.png)

Notice how the **Filtered Records Count** has changed to reflect the number of records that match the filters you have created.

Now continue as normal and use the **Delete Now** action as described in the previous usage scenario.

# Creating a Delete Package

**Delete Packages** allow you to create a package and select multiple tables that will be deleted in the order in which they appear.

# Background Processing via the Job Queue

To process delete packages via the job queue, create a job queue entry for Codeunit 71922936 BC_ProcessAvailablePackages. This will find any delete packages with a **Job Queue Filter** field set to **Available for Processing** and process the package in the background.

One single job queue entry will process all available packages, however you can use the Parameter String field on the job queue entry to provide additional filters that will be applied to the delete package code.

# For Developers

If you want to add the **Bulk Delete** action to your own extensions, you can simply add the Bulk Delete app as a dependency to your project as follows.

```
    {
      "id": "f6ed7976-9eb2-4854-b0e3-ab8a4a3f23ea",
      "name": "Bulk Delete",
      "publisher": "BC Apps Limited",
      "version": "2.0.19.0"
    }
```
Then on the list page, simply add the following action. Please note that this is for deleting Item records from the Item Card page. You should replace the BC_BulkDelete with your own action name that uses your own prefix, you should change the ItemToDelete variable declaration and name to refer to the record you are actually deleting. The option will use the multi-select as the required records to delete if the user has selected more than one record, otherwise it will copy the filters from the record.

```
    actions
    {
        addlast(processing)
        {
            action(BC_BulkDelete)
            {
                Caption = 'Bulk Delete';
                Ellipsis = true;
                ToolTip = 'Triggers the deletion of the selected records.';
                Image = DeleteRow;
                ApplicationArea = All;

                trigger OnAction()
                var
                    CustomerToDelete: Record Customer;
                    ProcessSelection: Codeunit BC_ProcessSelection;
                begin
                    CurrPage.SetSelectionFilter(CustomerToDelete);
                    ProcessSelection.DeleteSelectedRecords(CustomerToDelete);
                end;
            }
        }
    }
```
