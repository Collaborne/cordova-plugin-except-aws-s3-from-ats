# cordova-plugin-except-aws-s3-from-ats
Cordova plugin that excepts access to S3 from App Transport Security (iOS9)

# Background
iOS9 introduced strict transport security rules ([ATS](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/)) which rejects the current S3 certificates. This blocks all
access from Cordova based apps to AWS S3, e.g. `<img src="https://xxx.s3.amazonaws.com/my-image.png" />` won't load.

AWS recommends to except the S3 domain via the -Info.plist ([link](https://forums.aws.amazon.com/thread.jspa?threadID=215371)):

> Recent changes, per Apple’s App Transport Security Technote, states using NSURLConnection, CFURL, or NSURLSession require TLS 1.2 and SHA256 (or > better) signed hash algorithms. S3 currently supports TLS 1.2. S3 endpoint certificates will continue to be based on SHA-1 until September 30th. We recommend specifying exceptions to the default ATS behavior by modifying the Info.plist file during the transition period. Later this year, when S3 SHA-256 certificates are deployed, we recommend testing and confirming your application works properly with the enabled ATS security settings.
> 
> All current apps will continue to function just fine. This applies specifically to those that are compiled with the new SDK, Xcode 7.

This plugin adds the required entry to -Info.plist.