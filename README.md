# node-sass-bindings
This is to access a zipped version of node-sass-bindings. Otherwise downloading binding files over corporate proxy can be blocked.

# references to install over corporate proxy
- https://github.com/sass/node-sass/issues/2133

# unzip files and place relative to your npm cache file like this
- C:\Users\[your name]\AppData\Roaming\npm-cache\node-sass\4.13.1\win32-x64-67_binding.node

# npm install 
```
npm i node-sass@4.13.1 --save
```
or 
```
npm run rebuild node-sass
```

# If this is still a problem - an alternative is using create-react-app - then ejecting and copying the node_modules folder into your project or in global roaming space 
```
npx create-react-app myproject --use-npm
npm run eject 
```

# copy myproject/node_modules/node-sass into your project folder node_modules  - or copy it globally into - 
- ( if you can't see AppData - turn on hidden files in folder view settings of file explorer )
- C:\Users\[your user]\AppData\Roaming\npm\node_modules



