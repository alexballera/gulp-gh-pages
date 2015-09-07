#Desplegando proyecto node.js en GitHub gulp-gh-pages

Referencia: artículo publicado por [Charlie Gleason](http://charliegleason.com/articles/deploying-to-github-pages-with-gulp)  

##Getting started
###Creas el proyecto e inicias **npm**
```sh
$ npm init
```

###Agregamos las dependencias: **gulp** y **gulp-gh-pages**
```sh
npm install gulp --save-dev
npm install gulp-gh-pages --save-dev
```

###Agregamos la tarea **deploy** en ```gulpfile.js```:  
```sh
var gulp        = require('gulp');
var deploy      = require('gulp-gh-pages');

/**
 * Push build to gh-pages
 */
gulp.task('deploy', function () {
  return gulp.src("./dist/**/*")
    .pipe(deploy())
});
```
###Configuramos ```.gitignore```
```sh
node_modules
dist
```
###Subimos los cambios a GitHub y creamos branch ```gh-pages```  
```sh
git checkout --orphan gh-pages
git rm -rf .
touch README.md
git add README.md
git commit -m "Init gh-pages"
git push --set-upstream origin gh-pages
git checkout master
```
###Actualizamos los cambios en la rama ```gh-pages```  
```$ gulp deploy```  
###Automatizamos los cambios a **```master```** y a **```gh-pages```**  
```
$ cd .git/hooks
```

Creamos archivo **post-commit**
```
$ touch post-commit
```

Agregamos las siguientes líneas en el archivo **post-commit**:  
```
#!/bin/sh
gulp deploy
git push origin master
```

Otorgamos privilegios
```
$ chmod +x post-commit
``` 
###Por último, configurar la url en GitHub:
```sh
username-github.io/repositorio
```
