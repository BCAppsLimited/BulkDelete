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

# Delete Items, Customers, or Vendors

In this topic we'll cover how to perform a bulk delete on a list of items, although the same process can be followed for customers or vendors using the appropriate pages.

From the **Item List** page, select the records you wish to delete either by selecting multiple records as shown in the following image or applying a filter to match the records you want to delete.

![Image showing the Item List page with the Bulk Delete Action being selected.](/screenshots/usagescenarios/ItemListBulkDelete.png)

From the Actions, select the **Bulk Delete** option. The system will create a new bulk delete request using the information you selected and show you the **Bulk Delete Request Card**.

![Image showing the Bulk Delete Request Card with the select item records.](/screenshots/usagescenarios/ItemPendingBulkDeleteRequestCard.png)

The system has converted the records you selected into a filter for the **No.** field on the **Item** table. You can see that the **Filtered Records Count** field shows a count of four records to be deleted.

Once you are ready to proceed and delete the records, click the **Delete Now** action.

The system will display a confirmation dialog to ensure you really want to delete the selected records.

![Image showing the confirmation dialog for deleting four selected records.](/screenshots/usagescenarios/ConfirmDeleteFourItems.png)

Select **Yes** to continue with the delete. The system will attempt to delete each record in turn and record whether the delete succeeded or failed. You can see the results in the **Latest Run Details** group.

![Image showing the results of the bulk delete.](/screenshots/usagescenarios/LatestDeleteRun.png)

You can review the reasons why the records failed to delete by clicking the drill down on the **Failed to Delete** count to see the **Delete Requests** page.

![Image showing the four records that failed to delete.](/screenshots/usagescenarios/DeleteRequestsWithFourErrors.png)

If you are finished with the Bulk Delete Request, you can return to the Bulk Delete Request Card and delete the record. This will prompt for deletion.

![Image showing the confirmation dialog for deleting a Bulk Delete Request record.](/screenshots/usagescenarios/DeleteBulkDeleteReqeuestConfirmation.png)

Select the **Yes** button and the system will delete the Bulk Delete Request record and the associated filter lines and results records.

# Bulk Delete Any Table

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


# For Developers

If you want to add the **Bulk Delete** action to your own extensions, you can simply add the Bulk Delete app as a dependency to your project as follows.

```
    {
      "id": "f6ed7976-9eb2-4854-b0e3-ab8a4a3f23ea",
      "name": "Bulk Delete",
      "publisher": "BC Apps Limited",
      "version": "1.0.0.0"
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
                    BulkDeleteManager: Codeunit BC_BulkDeleteManager;
                begin
                    CurrPage.SetSelectionFilter(CustomerToDelete);
                    BulkDeleteManager.BulkDeleteSelectedRecords(CustomerToDelete);
                end;
            }
        }
    }
```

---

[^1]: Well, you could restore a point-in-time backup of your environment and export the lost data and then, restore back to after you deleted the data and re-import the data, but this would be a serious nuisance. If you find yourself in this unfortunate situation, please contact your partner.
