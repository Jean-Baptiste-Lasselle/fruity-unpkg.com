# Foreword 

 I ([me](https://github.com/Jean-Baptiste-Lasselle)) created this folder on top of my fork of https://github.com/unpkg/unpkg.com, so I can store in here my resources on this tech discovery workshop.
 
 In the [./reverse-devopsing/docuementations/images/](/reverse-devopsing/docuementations/images/)  will be nested images referenced everywhere in me markdown files.
  
# Study
 
## Goals
 
* to be able to spawn up a peivate unpkg.com instance,
* with all std operations as code
* consider coupling with varnish
* test the varnish option within a pipeline, and within to feel the ease
* test the varnish option with https://github.com/Jean-Baptiste-Lasselle/grapejs-server, to make the experience exciting as hell up to MJML
 

# What the build?*:o


### Build the app

```bash
# https://github.com/unpkg/unpkg.com
export URI_DE_CE_REPO=https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com

git clone "$URI_DE_CE_REPO"

cd ./fruity-unpkg.com
npm install
# triggers [npm rollup -c .]
npm build .
# now the babel transpilation : some ./modules   files obviously need transpilation see [https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/blob/ab78e4f64e98fc743f3a1419d243948c033806ac/modules/server.js#L1] 
# just getting rid of old things in the old package.json
npm uninstall babel
npm install --save-dev babel-cli
which babel
babel  ./modules --experimental --source-maps-inline -d ./dist
export PORT=3000 && node modules/server.js
```


### _About Babel and [unpkg.com](https://github.com/unpkg/unpkg.com)_

Some   files in the  `./modules` folder obviously need transpilation : 
* For instance at [this line ine the `modules/server.js` file](https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/blob/ab78e4f64e98fc743f3a1419d243948c033806ac/modules/server.js#L1), you can read : 

```ES6
import express from 'express';
```

Which is pretty much `ES6`-like, at any rate, will make the startup command fail :

```JavaScript
node modules/server.js
# n.b.: my guess that it's how https://github.com/unpkg/unpkg.com  should be started
```

All in all , I end up with the following error when I try and use `babel-cli`, on the `modules` directory : 

![unpkg.com babel build fail 1](https://raw.githubusercontent.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/master/reverse-devopsing/documentations/images/UNPKG.COM_BABEL_BUILD_FAIL_2019-03-24%2002-21-31.png)

To get the error above, here is exactly what I executed on Katacoda : 

```bash
# 
export URI_OF_GUESS_WHAT=https://github.com/unpkg/unpkg.com

rm -rf ./fruity-unpkg.com
mkdir -p ./fruity-unpkg.com
git clone "$URI_OF_GUESS_WHAT" ./fruity-unpkg.com
cd ./fruity-unpkg.com
npm install
# [never mind about the rollup]
# now the babel transpilation : some ./modules   files obviously need transpilation see [https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/blob/ab78e4f64e98fc743f3a1419d243948c033806ac/modules/server.js#L1] 
# just getting rid of old things in the old package.json
npm uninstall babel
npm install --save-dev babel-cli
which babel
babel  ./modules --experimental --source-maps-inline -d ./dist

```


### Start the app

My guess that it's how https://github.com/unpkg/unpkg.com  should be started

```JavaScript
node modules/server.js
```
So why is there not a : 

```json

  scripts: {
    start : "node modules/server.js"
  }
```
?


# Latest Hunt

Got me there (Github sgested me to look at all the babel relatd issues, while I began typing.. qite a wise piece of advice, which I will foloow on the next episode) : 

[![screenshot suggestion github vers exemple issue 151](https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/raw/master/reverse-devopsing/documentations/images/GITHUB_AVOID_OPENING_AN_ISSUE_2019-03-24%2003-01-16.png)](https://github.com/unpkg/unpkg.com/issues/151)

https://github.com/unpkg/unpkg.com/issues/151

### Prepared Issue Template

> 
> BABEL_BUILD_ERROR
> 
> Hi, I have an error, and probably a question about how to build and run thsi node app : 
> 
> * My problem happened trying to trnaspile using `babel-cli`
> * you wil find full details about my error, including screenshots of logs and bug reproductibility with a recipe , here : https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/blob/master/reverse-devopsing/README.md#about-babel-and-unpkgcom
> 
> Thank you so much in advance for any info
> 

# Next move

Try : 

```bash
# 
export URI_OF_GUESS_WHAT=https://github.com/unpkg/unpkg.com

rm -rf ./fruity-unpkg.com
mkdir -p ./fruity-unpkg.com
git clone "$URI_OF_GUESS_WHAT" ./fruity-unpkg.com
cd ./fruity-unpkg.com
npm install
# [never mind about the rollup]
# now the babel transpilation : some ./modules   files obviously need transpilation see [https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/blob/ab78e4f64e98fc743f3a1419d243948c033806ac/modules/server.js#L1] 
# just getting rid of old things in the old package.json
npm uninstall babel
npm install --save-dev babel-cli
which babel
# babel  ./modules --experimental --source-maps-inline -d ./dist

# NEXT MOVE  suggested by issue https://github.com/unpkg/unpkg.com/issues/151
npm install --save-dev @babel/plugin-syntax-dynamic-import
npm install --save-dev @babel/plugin-syntax-import-meta

# then I'll try again and babel..

babel  ./modules --experimental --source-maps-inline -d ./dist

```
