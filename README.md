# Utilisation

### Start the app 


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

Aboput Babel : 

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




# Début du `README.md` original
=======================================

# unpkg [![Travis][build-badge]][build]

[build-badge]: https://img.shields.io/travis/unpkg/unpkg.com/master.svg?style=flat-square
[build]: https://travis-ci.org/unpkg/unpkg.com

[unpkg](https://unpkg.com) is a fast, global [content delivery network](https://en.wikipedia.org/wiki/Content_delivery_network) for everything on [npm](https://www.npmjs.com/).

### Documentation

Please visit [the unpkg website](https://unpkg.com) to learn more about how to use it.

### Sponsors

unpkg is made possible by generous donations from [Cloudflare](https://cloudflare.com) and [Angular](https://angular.io).
