---
# Page settings
layout: default
keywords:
comments: true

# Hero section
title: Overview
description:  In this section you'll find basic information about the Bulk Delete extension, what it does, and how to use the features. Read this section to help you decide if this is the right extension for you.

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
        content: Home
        url: /
    next:
        content: Install Guide
        url: /install-guide
---

# An Important Warning

It feels important that we get something straight before we start, so please read the following warning...

<div class="callout callout--danger">
<p><strong>There Is No Undo</strong></p>
If you've used Business Central, you know that when you delete a record, whether you intended to or not, as long as the validation logic passes, the record will get deleted and you cannot get it back. There is no undo. There is no undelete. The record is gone, vamooshed, it is no more. You get the point...
</div>

If you delete something you didn't mean to delete using our extension, you're on your own. There is no magic undelete[^1] feature, so please be careful. Right. Now we have that straight, let's talk about what the app *does* do.

# What is Bulk Delete?

There are some list pages in Business Central where you can only delete records one at a time. For example:

- **Items**
- **Customers**
- **Vendors**

There are also occasions where you want to delete a whole bunch of records and you don't really want to sit there hitting the delete button, waiting for the related card page to launch with a question asking if you want to delete the record, selecting yes, waiting for the delete to succeed or fail, reviewing the error messages, etc.

The Bulk Delete app adds a new **Bulk Delete** action to the Items, Customers, and Vendors list pages that will create a bulk delete request which you can review before continuing. Any errors for records that could not be deleted are logged for you to review later.

# Permissions and Checks

The Bulk Delete app does not grant a user additional permissions, so you'll only be able to delete records you actually have permission to delete. Also, if there are validation checks performed when you attempt to delete the record, these will always be performed. The Bulk Delete app is designed to do exactly the same as manually deleting each record, only faster.

# Bulk Delete Any Table

As well as creating bulk delete requests from the Items, Customers, and Vendors list pages, you can create a new Bulk Delete Request and pick from any of the available tables.

# How Much?

## It's Free

This extension is fully featured and completely free for you to use. If you find it useful, please leave a review on [Microsoft's AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365-business-central/PUBID.bcappslimited1693858041247%7CAID.bulk-delete%7CPAPPID.f6ed7976-9eb2-4854-b0e3-ab8a4a3f23ea?tab=Overview) and link to the app on LinkedIn.

Just in case you're not sure how to get started and install the product, checkout our [Install Guide](/BulkDelete/install-guide). For a more in-depth look at the features, see our [Usage Scenarios](/BulkDelete/usage-scenarios).

---

[^1]: Well, you could restore a point-in-time backup of your environment and export the lost data and then, restore back to after you deleted the data and re-import the data, but this would be a serious nuisance. If you find yourself in this unfortunate situation, please contact your partner.