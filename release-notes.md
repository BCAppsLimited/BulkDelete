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

![Image showing the Delete Now split button with Delete in Backgoround action.](/screenshots/releasenotes/DeleteNowSplitButton.png)

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