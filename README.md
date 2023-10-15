# How to create destributable .pkg (or .dmg): step-by-step guide

Hello young macOS developers! 

Have you finished coding your shiny MacOS app? And now want to wrap it into .pkg (or .dmg) and destribute it NOT usnig App Store? If the answer is 'yes' this guide is for you.

So, if you're ready, lauch Xcode with your app and follow these 4 simple steps!

### 0. Buckle up!

 First of all, you need to make sure you have:
- Developer ID Application Certificate (with corresponding private key)
- Developer ID Installer Certificate (with corresponding private key)
- Provisioning Profile
- App-specific password (you can create one at https://appstoreconnect.apple.com)
    
Also you need to be a part of Development Team.

## 1. Get your .app notarized

Build your Mac application via Xcode. Make sure you set architectures right (**Standard** (both Silicon and Intel) or just **Silicon**) for both app target and all pods targets.

Perform: 
1. *Archive*
2. *Destribute* -> *Custom* -> *Developer ID* -> *Upload: Send to Apple Notary Service*
3. Wait for your .app to *Export*
    
Now you have your .app **signed** and **notorized** by Apple.

## 2. Create your .pkg

There are multiple ways to create .pkg files. I've used *Packages* app:

Download: http://s.sudre.free.fr/Software/Packages/about.html



Guide: http://s.sudre.free.fr/Software/documentation/Packages/en_2017/index.html
    
Hope you're doing grate and got your fancy .pkg!

## 3. Sign and notorize your .pkg

Before you share your package or .dmg *(next step)* with people you have to make these two steps (or macOS won't let others open your package, protecting them from possible malware):
1. Sign your package with Developer ID Installer Certificate:
    
        productsign [options] --sign <team-id> <input-product-path.pkg> <output-product-path.pkg>

    You can read more about `[options]` typing

        man productsign
    
    in your terminal.
    
2. Notorize your package after signing:
    
        xcrun notarytool submit <input-product-path.pkg> --wait --apple-id=<developer-apple-id> --team-id=<team-id> --password=<app-specific-password>

    You can read full `notarytool` usage typing 

        man notarytool
    
    in your terminal.

After that you'll have **signed** and **notarized** .pkg you can share with people. 

## 4. Finally, build and sign .dmg

If you need to share multiple files, you probably will use disk image for this. Easiest way to build it is to use macOS build-n app *Disk Utility*. To sign your .dmg use command:

    codesign --sign [options] <developer-id-application-cert> <input-product-path.dmg>

You can read full `codesign` usage typing

    man codesign

in your terminal.


So, that's all :) 

Hope my article helped you and saved some time!

Happy coding,

FinickyPrune.
