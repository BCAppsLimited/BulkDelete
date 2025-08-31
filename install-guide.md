---
# Page settings
layout: default
keywords:
comments: true

# Hero section
title: Install Guide
description:  In this section you'll find basic information about how to install the app and configure the permission sets.  If you're a first time user, you should read this Install Guide first.

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
        content: Overview
        url: /overview
    next:
        content: Usage Scenarios
        url: /usage-scenarios
---

# Installation

You can install this app from the [Bulk Delete page on AppSource](https://appsource.microsoft.com/en-us/product/dynamics-365-business-central/PUBID.bcappslimited1693858041247%7CAID.bulk-delete%7CPAPPID.f6ed7976-9eb2-4854-b0e3-ab8a4a3f23ea?tab=Overview) by clicking the **Get it now** button. This can only be used to install the app in your organisation's tenancy. If, on the other hand, you are installing this extension in your customer's tenancy, you can use the Business Central app to install the extension. 

Open your Business Central Sandbox environment and use the Alt+Q keypress or click the Search icon in the toolbar to bring up the search dialog which says *Tell me what you want to do* at the top of box. Type *appsource* in the box and you will see an option for **Microsoft AppSource apps**.

![Image showing the search box with the text appsource entered.](/screenshots/install/SearchForAppSource.png)

Select the option to launch the **Microsoft AppSource apps** page. This page can take a while to load as it needs to read a list of available apps from the AppSource API. If you have not used this page before, you may see a prompt asking you to allow a connection to an external service.

![Image showing the request to allow a connection to an external service.](/screenshots/install/AllowRequestToService.png)

Ensure *Allow Always* is selected and click **OK**.

When the **Microsoft AppSource apps** page has opened, use the search box at the top of the page to search for a specific app.

![Image showing the Microsoft AppSource apps page with the search box activated](/screenshots/install/SearchForAnApp.png)

Type *Bulk Delete* into the search box and you will see the app from publisher *BC Apps Limited* in the list of results.

Click on the contents of the **Name** field for the Bulk Delete app and you will be shown the **App overview** page.

![Image showing the App overview page for the selected app.](/screenshots/install/AppOverview.png)

Click the **Install App** action button at the top of the page.

![Image showing the install extension prompt.](/screenshots/install/InstallExtension.png)

Click the **Install** button at the bottom of the dialog to continue with the install.

The **Installing app** dialog will launch to show you that the app installation is in progress.

![Image showing the installing app dialog.](/screenshots/install/InstallingApp.png)

After a short while, you will see the message that your app is installed and ready to use.

![Image showing the app is installed and ready to use message.](/screenshots/install/AppIsInstalled.png)

Congratulations! The app is now installed in your environment and you can go ahead and configure the extension for the first time use.

# Configuration

## Grant Permissions

If you have SUPER then you'll be able to use the **Bulk Delete** options without needing to set up additional permissions. For a regular user, however, you must assign the **BC_BD_ALL** permission set so that they can use the bulk delete options.

That's all there is to it. For more details on how you can use the Bulk Delete extension, see the [Usage Scenarios](/BulkDelete/usage-scenarios) help topic.

---

[^1]: In a Production environment a user can only see the **Bank Validation Result** field if they have a Bulk Delete license assigned to them.