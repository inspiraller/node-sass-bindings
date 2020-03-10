# How to fix node-gyp errors when installing node-sass over a corporate proxy
The problem is caused often due to an attempt to dynamically download the node-sass binding files over the network, but in doing so it cannot access the node-binding file and instead you end up with a corrupted file. It's deceptive because the file download is very similar in size to the true binding file at about 2mb but the actual files are about 2.4mb. You can even try to access this file yourself by going to the web browser and clicking to download it, but you will see instead an xml file which is not the binding file.

# Using this repo node-sass binding files?
You can use this repo as an example, but you may have a different operating system so may need to follow a similar example but download the binding files you need instead.
Which binding files do you need? Look at your errors:

- Download Binary from .... /v4.13.0/win32-x64-67\binding.node
- Binary saved to .... C:\Users\[your name]\AppData\Roaming\npm-cache\node-sass\4.13.1\win32-x64-67_binding.node
- Binary has a problem: Error ... win32-x64-67\binding.node

# Delete any existing created node-sass folder that may have already been corrupted:
- C:\Users\[your name]\AppData\Roaming\npm\node-sass files...
- C:\Users\[your name]\AppData\Roaming\npm\node_modules/node-sass

# Download and unzip files from either this repo or your own created repo and place relative to your npm cache file like this
- C:\Users\[your name]\AppData\Roaming\npm-cache\node-sass\4.13.1\win32-x64-67_binding.node
- Be sure to use the same folder directory as your error has stated above.
ie 4.13.1 as in this example. Yours maybe different.

# npm install globally first to see the install work first.
```
npm i node-sass@4.13.1 -g
```

# troubleshooting - if node-gyp error
## missing specific win32-x64-67_binding.node file
Look at the error that node-gyp says. It may have tried to download the binding file anyway and place it into your npm cache -
- C:\Users\[your name]\AppData\Roaming\npm-cache\node-sass\4.13.1\win32-x64-67_binding.node

If that has happened, it is because node-gyp is trying to find a win32-x64-67_binding.node, but you only have win32-x64-64_binding.node or some other version in your node-sass/4.13.1 folder. Node-gyp tries to download the broken xml output, and therefore the installation fails.
- Solution:
Now you know which one it is trying to get, you will need to zip that specific file before downloading it over the corporate network.
Place that specific file into your npmcache like this:
- C:\Users\[your name]\AppData\Roaming\npm-cache\node-sass\4.13.1\win32-x64-67_binding.node
- try npm install again
```
npm i node-sass@4.13.1 -g
```
## troubleshooting - existing corrupted built node-sass file.
Another error that might happen is that now you have tried to make it work, but node-gyp has already created a corrupted node-sass file.
It tries to use that version, and doesn't attempt to download or use your cache.
- Solution:
Delete both:
 - C:\Users\steve\AppData\Roaming\npm\node-sass.cmd
 - C:\Users\steve\AppData\Roaming\npm\node_modules\node-sass
Now try to install again
```
npm i node-sass@4.13.1 -g
```
This should work.

# Now if you want to install node-sass specific to your project, just install node-sass relative to your project  and it should use the global version
```
npm i node-sass@4.13.1 -D
```

# Worse case scenario - If this is still a problem - an alternative is using create-react-app - then ejecting and copying the node_modules folder into your project or in global roaming space
```
npx create-react-app myproject --use-npm
npm run eject
```



# Useful references to install over corporate proxy
- https://github.com/sass/node-sass/issues/2133
