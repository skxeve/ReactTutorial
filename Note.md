
プロジェクト作成ログ
いくつか警告が出た
```
$ create-react-app my-app

Creating a new React app in /Users/user-name/git/github.com/skxeve/ReactTutorial/my-app.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts...


> fsevents@1.2.4 install /Users/user-name/git/github.com/skxeve/ReactTutorial/my-app/node_modules/fsevents
> node install

  SOLINK_MODULE(target) Release/.node
  CXX(target) Release/obj.target/fse/fsevents.o
In file included from ../fsevents.cc:6:
../../nan/nan.h:1064:44: warning: 'ToString' is deprecated: Use maybe version [-Wdeprecated-declarations]
      v8::Local<v8::String> string = from->ToString(v8::Isolate::GetCurrent());
                                           ^
/Users/user-name/.node-gyp/11.1.0/include/node/v8.h:2537:3: note: 'ToString' has been explicitly marked deprecated here
  V8_DEPRECATED("Use maybe version",
  ^
/Users/user-name/.node-gyp/11.1.0/include/node/v8config.h:326:29: note: expanded from macro 'V8_DEPRECATED'
  declarator __attribute__((deprecated(message)))
                            ^
../fsevents.cc:63:6: warning: field 'async_resource' will be initialized after field 'lockStarted' [-Wreorder]
   : async_resource("fsevents:FSEvents"), lockStarted(false) {
     ^
2 warnings generated.
  SOLINK_MODULE(target) Release/fse.node
ld: warning: text-based stub file /System/Library/Frameworks//CoreFoundation.framework/CoreFoundation.tbd and library file /System/Library/Frameworks//CoreFoundation.framework/CoreFoundation are out of sync. Falling back to library file for linking.
ld: warning: text-based stub file /System/Library/Frameworks//CoreServices.framework/CoreServices.tbd and library file /System/Library/Frameworks//CoreServices.framework/CoreServices are out of sync. Falling back to library file for linking.
ld: warning: text-based stub file /System/Library/Frameworks//CFNetwork.framework/Versions/A/CFNetwork.tbd and library file /System/Library/Frameworks//CFNetwork.framework/Versions/A/CFNetwork are out of sync. Falling back to library file for linking.
ld: warning: text-based stub file /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/OSServices.framework/Versions/A/OSServices.tbd and library file /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/OSServices.framework/Versions/A/OSServices are out of sync. Falling back to library file for linking.
ld: warning: text-based stub file /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/LaunchServices.tbd and library file /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/LaunchServices are out of sync. Falling back to library file for linking.
ld: warning: text-based stub file /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/SharedFileList.framework/Versions/A/SharedFileList.tbd and library file /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/SharedFileList.framework/Versions/A/SharedFileList are out of sync. Falling back to library file for linking.
  COPY /Users/user-name/git/github.com/skxeve/ReactTutorial/my-app/node_modules/fsevents/lib/binding/Release/node-v67-darwin-x64/fse.node
  TOUCH Release/obj.target/action_after_build.stamp
+ react@16.6.1
+ react-dom@16.6.1
+ react-scripts@2.1.1
added 1766 packages from 678 contributors in 52.443s

Success! Created my-app at /Users/user-name/git/github.com/skxeve/ReactTutorial/my-app
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd my-app
  npm start

Happy hacking!

```
