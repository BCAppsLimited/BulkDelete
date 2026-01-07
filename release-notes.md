---
# Page settings
layout: default
keywords:
comments: true

# Hero section
title: Release Notes
description:  This section provides the easiest way to catch up on what's new in the latest release.

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
        content: Support
        url: /support
    next:
        content: 
        url: 
---

# What's New in Version 2.0.19.0

## Licensing Changes

The quick Bulk Delete action on Customers, Vendors, Items, and Fixed Assets remain available to all users for free without a license. The advanced features of delete package management can be configured by any user with the appropriate permissions, but only those uses with at Bulk Delete Standard license will be able to run the delete operations.

## Delete Packages

In this release we've had a complete rethink of how the Bulk Delete processing should work and have come up with a new system which we are calling *Delete Packages*. Here's an overview of the changes.

- Delete Packages allow you to define a set of tables that will be processed in a single package.
- Unlike Bulk Delete Requests which could not be edited after the first run, Delete Packages can be changed at any time.
- Tables within a package (called **Delete Package Lines**) can be reordered using **Move Up** and **Move Down** actions to change the execution order.
- A **Delete Action** for each line replaces the **Store After Delete OK** option (which included *Record Identifier Only* and *Nothing* as choices) which allows delete actions of *Delete and Log*, *Delete Only*, and *Truncate*. The truncate option does not run the standard delete triggers and is therefore only available in a Sandbox environment.
- A single Job Queue Entry codeunit will process all Delete Packages where the **Job Queue Filter** is set to **Available for Processing**. The **Parameter String** on the Job Queue Entry can be used as a filter for Delete Packages to be processed allowing a single Job Queue Entry to process all available packages or only those that match the filter.
- An option to add the delete history (the **Delete Package Run** details) to a package so that it will keep the log data under control.
- The progress dialog when deleting as a foreground task has been removed and has resulted in a noticeable performance increase.
- The counting of records now happens as a page background task meaning the page will render even if there are many millions of records that match the filter. Previously extremely large tables could have a significant delay when waiting for the record count to complete.
- Delete Package definitions can now be exported and imported which is a useful way to preserve "data clean-up" packages that get lost when a Sandbox is overwritten with a copy of Production.




# What's New in Version 1.0.16.0

We've made the Bulk Delete option from Customer, Vendor, Item, and Fixed Asset lists even easier to use. After a confirmation dialog, the process shows a progress dialog as it deletes the selected records. Any errors are shown in the error details page after the delete has completed.

# What's New in Version 1.0.15.0

## DateTime Filtering

Thanks to your feedback we discovered that it is not possible to use formulae to filter DateTime fields. This is a common requirement for bulk delete scenarios where we want to delete records that were created more than a month ago. Typically we would use "<t-1m" as our filter value and expect this to resolve to "<27/09/25 12:00 AM" (where 27/10/2025 is today's date and you are using a region that has dd/MM/yy as a date formatting default).

We've added some magic to the app so you can now use the same date formulae in a *DateTime* field that you would use in a *Date* field and it will get translated.

## Counting Records

Although we fixed the ability to enter incorrect filter fields by validating filter entry, there were still problems if you had old invalid data which caused the **Bulk Delete Request Card** page to fail when trying to calculate the **Filtered Records Count**. Now the system will simply show "Invalid Filters" in the count field which allows you to continue using the page as normal.

## CountApprox

Bulk Delete is being used in the real world where some tables have millions of records and we noticed a delay showing the page and the prompt to confirm deletion when there are large numbers of records to count. Now if there is more than a million records, we will use the *CountApprox* command instead of the *Count* which improves performance. This is only the first step in solving this issue when we are looking to see if a background task can be used to make more improvements. We will use CountApprox when there are more than a million records and the **Filtered Records Count** will show "(approx)" after the count.

## Created At Captions

As a minor tidy up, we've fixed captions on some pages that show SystemCreatedAt fields that now show *Create At* as the field caption.

# What's New in Version 1.0.14.0

## Name

We've added a **Name** field to the bulk delete request which makes it easier to identify saved requests that run regularly. The field is also available on the **Bulk Delete Runs** page showing you the **Bulk Delete Request Name** and allowing a drill-down action to take you to the related request.

## Improved Filtering

We've fixed an issue where invalid filters entered for a bulk delete request would cause an error when the page opened and essentially make the bulk delete request unusable. Now when you enter a filter the entered value is validated and must be corrected if it is invalid. It's always been possible to use placeholders in your filters but now you will receive immediate feedback if the filter you have entered is not valid. Filters that use placeholders will have the current value of the resolved filter shown in a new resolved filter field.

## Resolved Filters

We've added a new **Resolved Filter** field to the filters section of the bulk delete request card which allows you to see how any placeholders you have entered into the filter will resolve. Use placeholders in date fields like **t** for today, or date formulae like **<t-90d** to mean less than 90 days prior to today's date. You can also use placeholders such as **%mycustomers**, **%myvendors**, or **%me** to resolve to the customer or vendor codes in your favourites or your own user name. See [Using Filter Tokens](https://learn.microsoft.com/en-us/dynamics365/business-central/ui-enter-criteria-filters#FilterTokens) in Microsoft Learn for more details on using filter tokens as placeholders.

In addition to showing how an individual filter will resolve, we've added a **Resolved Filters** fact box to the bulk delete request run page to show which filters were applied when the run was carried out.

## Estimated Time Fix

We've fixed a bug in the estimated time to complete on the bulk delete request run fact box where the value was not being calculated correctly.

# What's New in Version 1.0.11.0 

We've introduced an option on the Bulk Delete Request card that controls what should be stored when a record is successfully deleted. You can now minimise the records created by the bulk delete by selecting "Nothing" or leave the default as "Record Identifier Only". 

![Image showing the Store After Delete OK option.](/screenshots/releasenotes/StoreAfterDeletedOK.png)

We've also added an option to the Bulk Delete Requests list page that allows you to select multiple requests and delete them making it even easier than ever to keep your database tidy.

![Image showing the Delete Selected action on the Bulk Delete Requests list page.](/screenshots/releasenotes/DeleteSelected.png)

# What's New in Version 1.0.10.0 

Based on feedback from users of version 1.0.7.0, we've had a complete rethink of the Bulk Delete app and have made some great improvements.

- New progress details for **Delete Now**
- **Delete in Background** option
- Requests can have **multiple runs**
- **Cancel** a delete in progress
- **Refresh** progress with **Estimated time remaining**
- **Copy Request** feature
- Schedule deletes via the **Job Queue**
- Bulk Delete action added to **Fixed Assets** list

## Delete Now Progress Details

The previous version of our app was designed to be simple, but it became clear that some users wanted to use it to delete records in their thousands and, as a result, the old user interface design wasn't really up to the job. We've added a progress dialog pop-up that shows you the number of records deleted without error, the number of records that failed to delete, and a calculated estimated time remaining.

![Image showing the progress of the Delete Now action.](/screenshots/releasenotes/ProgressDialog.png)

Notice that there is a close button in the top right corner of the dialog page. If you click that, you get a prompt asking if you want to cancel the process, and if you agree, the delete process will be stopped. The records that had been deleted prior to cancelling are still deleted so, as always, make sure you really want to delete the records before you start.

## Delete in Background

The **Delete Now** option has been replaced with a split button that includes many options for deleting your data. You can now click the drop-down icon to the right of the **Delete Now** button and select from related actions, such as **Delete in Background**.

![Image showing the Delete Now split button with Delete in Background action.](/screenshots/releasenotes/DeleteNowSplitButton.png)

This will schedule a background task to carry out the delete which allows you to continue working in Business Central. The progress of the background task can be seen in the new **Latest Run Details** section on the **General** tab of the **Bulk Delete Request Card**.

![Image showing the Latest Run Details.](/screenshots/releasenotes/LatestRunDetails.png)

The page will not constantly refresh to show progress, but if you want to see the latest state, click the **Refresh** action. You can click on the drill down in the **Status** field and this will take you to the latest run associated with this delete request.

## Multiple Runs

The **Bulk Delete Request Card** has become the place where the records to be deleted are defined and the history of the delete is now stored on a bulk delete run. To see the runs associated with a bulk delete request, simply click the drill down on the **Run Count** field which is in the **Results** group on the **General** tab.

![Image showing the Bulk Delete Runs page.](/screenshots/releasenotes/BulkDeleteRuns.png)

This list has a fact box that shows the status of the run. You'll notice that there is a also a **Cancel Run** action that can be used to cancel a run that is running via a background task.

## Cancel Delete in Progress

We've already seen how a **Delete Now** can be cancelled, but what about when we use **Delete in Background**. If the background task is still running, simply navigate to the run (either by click on the **General > Latest Run Details > Status** field or the **General > Results > Run Count** field drill down) and select the **Cancel Run** action.

Note that there is no "are you sure?" prompt when you decide to cancel a run, but that's OK, you can always start the delete again if you want to continue. A bulk delete request can be run multiple times now.

## Refresh Progress

We've already seen how the **Refresh** action can be used to update the **General > Latest Run Details** fields. This is useful when our delete process is either running as a background task or running via the job queue.

## Copy Request

Once a delete operation has been carried out on a bulk delete request, it is no longer possible to edit the filter fields. If you want to try the delete again but with a slight change to the filtering, you can now use the **Copy Request** action to create a new bulk delete request that uses the same table and filtering options.

## Delete via Job Queue

The ability to delete in the background has already been covered and this is useful, but what if you want the delete to happen in the background at a scheduled time? You can now use the **Delete via Job Queue** option to create a job queue entry that is linked to a given bulk delete request.

The system will create a new job queue entry for Codeunit BC_ProcessBulkDeleteRequest with the record of the job queue entry pointing to the bulk delete request. You can now set the scheduled start time or set up a recurring job as you would normally do for a job queue entry. After creating a job queue entry for a bulk delete request, the bulk delete request card shows a section with the status of the related Job Queue Entry.

![Image showing the Job Queue Details section.](/screenshots/releasenotes/JobQueueEntryStatus.png)

The **General > Job Queue Details > Status** field allows you to drill down to display the linked record in the list of **Job Queue Entries**. There is also an action in the related action group that will take you directly to the **Job Queue Entry Card** for this particular bulk delete request.

## Fixed Assets

In addition to the customer, vendor, and item lists, there is now a **Bulk Delete** action on the **Fixed Assets** list page.