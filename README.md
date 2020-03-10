# node-sass-bindings
This is to access a zipped version of node-sass-bindings. Otherwise downloading binding files over corporate proxy can be blocked.
you can end up with node-gyp downloading and caching a corrupted version of the binding file - ie it looks like some xml file with errors at about 2mb
the actual files are about 2.4mb.

# references to install over corporate proxy
- https://github.com/sass/node-sass/issues/2133

# unzip files and place relative to your npm cache file like this
- C:\Users\[your name]\AppData\Roaming\npm-cache\node-sass\4.13.1\win32-x64-67_binding.node

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
