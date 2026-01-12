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

## Free Features

You can install Bulk Delete without needing to purchase a license and can use the quick bulk delete features for free. For details on how to install without a license, see the [Install Without a License topic in the Install Guide](/BulkDelete/install-guide/#install-without-a-license).

There are some list pages in Business Central where you can only delete records one at a time. For example:

- **Items**
- **Customers**
- **Vendors**
- **Fixed Assets**

The Bulk Delete app adds a new **Bulk Delete** action to the Items, Customers, Vendors, and Fixed Assets list pages that will allow you to delete a selection of records.  Any errors for records that could not be deleted are logged for you to review later. Simply select the records you want to delete and select the Bulk Delete action. For more details, see the [Delete Selected Records topic in the Usage Scenarios](/BulkDelete/usage-scenarios/#delete-selected-records).

# Permissions and Checks

The Bulk Delete app does not grant a user additional permissions, so you'll only be able to delete records you actually have permission to delete. Also, if there are validation checks performed when you attempt to delete the record, these will always be performed. The Bulk Delete app is designed to do exactly the same as manually deleting each record, only faster.

# Bulk Delete Any Table

There are also occasions where you want to delete a whole bunch of records quickly. Or maybe you need to delete a huge amount of records but want the system to take care of it, quietly, while no-one else is using the system.

As well as manually processing bulk delete requests from the Items, Customers, Vendors, and Fixed Assets list pages, you can create a new Delete Package and pick select which tables you want to delete. In order to use the delete packages feature to control your database size, you must have a license for Bulk Delete. There is a free trial option which will allow you to trial the product for thirty days.

Just in case you're not sure how to get started and install the product, checkout our [Install Guide](/BulkDelete/install-guide). For a more in-depth look at the features, see our [Usage Scenarios](/BulkDelete/usage-scenarios).

---

[^1]: Well, you could restore a point-in-time backup of your environment and export the lost data and then, restore back to after you deleted the data and re-import the data, but this would be a serious nuisance. If you find yourself in this unfortunate situation, please contact your partner.