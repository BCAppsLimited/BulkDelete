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

# Bulk Delete Request Card

![Image showing the Bulk Delete Request Card](/screenshots/usagescenarios/BlankBulkDeleteReqeustCard.png)

The **Bulk Delete Request Card** is used to configure a delete request (selecting a table, specifying the filters, and a time in minutes that the request can run before it is suspended).

If you select the **Bulk Delete** action from a list page such as **Customer List**, **Item List**, or **Vendor List**, the bulk delete request will be pre-populated with the correct **Table Id** and filters. The default 5 minutes is applied to allow the duration of a running delete to be limited.

After selecting the **Delete Now** action and confirming the dialog that shows how many records may be deleted, the **Deleted OK** and **Failed to Delete** cues will be updated to show the results.

You can drill-down into the cues to show the details of the records that were deleted or the error message that explains why an attempt to delete a record may have failed.

# Bulk Delete Requests

![Image showing the Bulk Delete Requests List](/screenshots/contexthelp/BulkDeleteRequests.png)

The **Bulk Delete Requests** list page shows all of the bulk delete request that are linked to your user. You can show all requests by clicking the **All Requests** action button. You can use this page to manage the request, such as deleting processed requests. You can also click the **New** action to create a new blank bulk delete request that you can configure for any table.

# Customer List

![Image showing the Bulk Delete action on the Customer List page](/screenshots/contexthelp/CustomerList.png)

A new action has been added to the **Customer List** page that will create a new bulk delete request for the currently selected filters.

# Delete Requests

![Image showing the results of an attempt to delete Items in the Delete Requests page.](/screenshots/contexthelp/DeleteRequests.png)

The **Delete Requests** page is shown when you drill down on a cue from the **Bulk Delete Request** list or card FactBox. The page shows the status of each record that a delete attempt was made on and the error message, if the delete request was unsuccessful.

# Item List

The **Item List** page has a new action called **Bulk Delete** that can be used to trigger the deletion of the selected or filtered items.

# Vendor List

The **Vendor List** page has a new action called **Bulk Delete** that can be used to trigger the deletion of the selected or filtered vendors.

---

