how to publish qt applications
------------------------------

from: https://blog.qt.io/blog/2012/04/03/how-to-publish-qt-applications-in-the-mac-app-store-2/

Code signing

Prior to codesigning the application bundle, use macdeployqt to copy the Qt frameworks and plug-ins into the bundle. If you know that your application does not use certain Qt frameworks or plug-ins, you can remove them from the bundle to reduce its total size. Besides the application bundle, you should also sign the frameworks and plug-ins in the bundle; at the time of writing, this is not required for App Store approval, but warnings about unsigned frameworks are issued. Instructions for obtaining the code signing certificates can be found in the “Submitting to the Mac App Store” document on the Apple developer website.

Frameworks are code signed with e.g.

  codesign -s "3rd Party Mac Developer Application: Developer Name" MyApp.app/Contents/Frameworks/QtCore.framework/Versions/4/QtCore
