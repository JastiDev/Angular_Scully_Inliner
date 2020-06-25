# How to make angular app to a single html file

## install
### 1. [scully](https://scully.io/docs/getting-started/)
- Add scully inside your angular app.
  `ng add @scullyio/init`
- do some route configuration in `./scully.<projectName>.config.ts` file.

### 2. [inliner](https://github.com/remy/inliner)
`npm install -g inliner`

### 3. Node/Express server to do inliner convert.
`npm init scully-inliner`
`cd scully-inliner`
`npm install express`

- create server.js
`
  var Inliner = require('inliner');
  var fs = require('fs');
  const express = require('express');
  const app = express();
  const port = 3000;


  app.use(express.static('public'));


  app.listen(port, () => {
    console.log(`listening on port ${port}!`);

    new Inliner(`http://localhost:${port}`, function (error, html) {
      // compressed and inlined HTML page

      fs.appendFile('result.html', html, function (err) {
        if (err) throw err;
        console.log('Combiled result Saved as result.html!');
      });
    });

  });
`

## Workflow
- Make static site from angular build using scully. Angular build result itself is not a static site, so scully is there.
`ng build`
`npm run scully`
- ./dist/static folder will contain the result. If you click index.html, you will see the page works exactly same as the angular app.
- copy those files inside the node server app's public folder.
- Run `node server` to get inliner result.





