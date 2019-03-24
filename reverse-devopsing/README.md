# Foreword 

 I ([me](https://github.com/Jean-Baptiste-Lasselle)) created this folder on top of my fork of https://github.com/unpkg/unpkg.com, so I can 
 store in here my resources on this tech discovery workshop.
 
 In the ./reverse-devopsing/docuementations/images/  will be nested images referenced everywhere in me markdown files.
 
 I addded
 
 # Study
 
 ## Goals
 
 * to be able to spawn up a peivate unpkg.com instance,
 * with all std operations as code
 * consider coupling with varnish
 * test the varnish option within a pipeline, and within to feel the ease
 * test the varnish option with https://github.com/Jean-Baptiste-Lasselle/grapejs-server, to make the experience exciting as hell up to MJML
 

# What the build?*:o

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

About Babel : 

Some   files in the  `./modules` folder obviously need transpilation : 
* For instance at [this line ine the `modules/server.js` file](https://github.com/Jean-Baptiste-Lasselle/fruity-unpkg.com/blob/ab78e4f64e98fc743f3a1419d243948c033806ac/modules/server.js#L1), you can read : 

```ES6
import express from 'express';
```

Which is pretty much `ES6` -like, at any rate, will make the startup command fail :

```JavaScript
node modules/server.js
# n.b.: my guess that it's how https://github.com/unpkg/unpkg.com  should be started
```
All in all , I end up with the following error when I try and use `babel-cli`, on the `modules` directory : 

![unpkg.com babel build fail 1](ccc)
![unpkg.com babel build fail 2](ccc)



 
