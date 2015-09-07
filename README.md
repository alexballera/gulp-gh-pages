#Desplegando proyecto node.js en GitHub gulp-gh-pages

Referencia: artículo publicado por [Charlie Gleason](http://charliegleason.com/articles/deploying-to-github-pages-with-gulp)  

##Getting started
###Creas el proyecto e inicias **npm**
```sh
$ npm init
```

###Agregas las dependencias: **gulp** y **gulp-gh-pages**
```sh
npm install gulp --save-dev
npm install gulp-gh-pages --save-dev
```

###Agregar en ```gulpfile.js``` el siguiente código:  
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
###```.gitignore```
```sh
node_modules
dist
```
###Subir cambios a GitHub y crear branch gh-pages
```sh
git checkout --orphan gh-pages
git rm -rf .
touch README.md
git add README.md
git commit -m "Init gh-pages"
git push --set-upstream origin gh-pages
git checkout master
```
Listo! con estos cambios, sólo nos falta ejecutar en la terminal:  
```gulp deploy```  

###Por último, configurar la url en GitHub:
```sh
username-github.io/repositorio
```
