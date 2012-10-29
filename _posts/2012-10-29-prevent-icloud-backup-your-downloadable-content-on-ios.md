---
layout: post
title: "Prevent iCloud backup your downloadable content on iOS"
category:
tags:
- iOS
---
{% include JB/setup %}

Today, I got our company ebook application been rejected AGAIN.

Approving application is a process of really wasting of time, and you need to got result after an week, even don't know if will pass or not, so let's learn more experience from the failure.

The reason that this application been rejected is:
Item 2.23 in the "Apple Store Review Guidelines" - Should not allow iCloud backup files which is not User generated.

Since it's ebook application we will download ebook content from server which is called "downloadable" and "not user generated" content. So according to the "iOS Data Storage Guidelines", we should put those files into "<Application_Home>/Library/Caches", although those files will be deleted by iOS system when there is no space. But since it's re-downloadable in your application should has this feature to detect file existence and to re-download the file when the file been deleted.

Our ebook application was persisted files in "<Application_Home>/Documents" before, which will be backed up by iCloud automatically everyday, and apple found those files are not user generated so the rejected.

Why the second submission been rejected is: because we set the "Deployment version target" to 4.3 which is not support one important feature "'do not back up' attribute" for files, that's why my solution, which just set attribute for downloaded ebook files as "do not back up", was rejected again.

Files won't be backed up only when been placed into:
1. the application bundle itself
2. the caches directory
3. temp directory

So finally we used one solution is:

1. Set the "Deployment target version" to 5.1 above (5.0 or earlier not support applying file attribute.)
2. Move the ebook downloading files into "<Application_Home>/Library/<Application Support|Custom Dir>"
3. Apply the "com.apple.MobileBackup" extended attribute to the download folder.


--------------------------------------
Some references:

* ["iOS Data Storage Guidelines"](https://developer.apple.com/icloud/documentation/data-storage/)

* ["File System Basics"](http://developer.apple.com/library/mac/#documentation/FileManagement/Conceptual/FileSystemProgrammingGUide/FileSystemOverview/FileSystemOverview.html)

* ["How do I prevent files from being backed up to iCloud and iTunes?"](https://developer.apple.com/library/ios/#qa/qa1719/_index.html)

* ["App Store Review Guidelines"](https://developer.apple.com/appstore/resources/approval/guidelines.html#functionality)
