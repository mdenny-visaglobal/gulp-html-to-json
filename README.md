# [gulp](http://gulpjs.com)-html-to-json

>Makes inclusion of files easy and fast.
Generates angular module for templateCache.
Compile html files and wrap it all in a single json file.
Enables you to include only the files you want.

>Can be useful if you want to generate various groups of templates and
include only the html files you want for that specific group. Can be use in backbone and angular

> To run Demo:
>
```
$ cd demo
$ gulp compileD
```
Just make sure the you already install all node modules including Dev Dependencies

Install :traffic_light:
-------

```bash
$ npm install gulp-html-to-json --save
```


## Pipe :neckbeard:

Like any other gulp plugin, transformed source files will flow onward to the destination of your choice.

In your gulpfile.js

**`/gulpfile.js`**

```javascript
var gulp = require('gulp');
var htmltojson = require('gulp-html-to-json');

gulp.task('markdown', function(){
        gulp.src('path/to/your/**/*.tpl')
            .pipe(htmltojson({
                filename: "filenameyouwant" //without file extension
                , useAsVariable: true
                , isAngularTemplate : true
                , prefix : "yourprefix"
                , includePaths: ['base/path']
            }))
            .pipe(gulp.dest('.'))


```

## Options

As of now, there are two options that you can use:

* `filename` (optional)
    * filename of the json file
    * should use only if you have 1 group template.
* `useAsVariable` (optional)
    * default false
    * If set to true, it will output your file as a javascript variable. Otherwise, json file
* `isAngularTemplate` (optional)
    * default false
    * If set to true, it will output your file as an angular template cache.
* `prefix` (optional)
    * set the prefix on your angular module name

* `includePath` (optional)
    * Takes a String or an Array of paths.
    * If set, gulp-html-to-json will use these folders as base path when searching for files.



Sample outpus if useAsVariable = false;

```javascript
{
    "key.name" : "<div>your html content</div>"
}

```
output file is filename.json


Sample output if useAsVariable = true;

```javascript
var filename = {
    "key.name" : "<div>your html content</div>"
}

```
output file is filename.js


Sample output if isAngularTemplate = true;

```javascript

    angular.module("prefix.filename").run(['$templateCache',
      function($templateCache) {
        $templateCache.put("key.name",
            // keyname.html content (escaped)
        );
        $templateCache.put("key2.name",
            // keyname2.html content (escaped)
        );
        // etc.
      }
    ]);

```
output file is filename.js


## Usage

In the file where you want want to compile you html, add a comment similar to this:

```javascript
//= key.name : relative/path/to/file.html
```

where key.name is the name want to associate with the html content in your json object.

If you use * as your key name like this :

```javascript
//= * : relative/path/to/file.html
```

It will automatically use the filename of your html as its key name.

If you want to use glob similar to commonly used in GruntJS, you may also to that like this:

```javascript
//= * : relative/path/to/**/*.html
```

Suggested key name is * so the it will use the filename as the keyname.

First sample code output:

```json
{
    "key.name" : "<div>your html content</div>"
}
```

Second sample code output:

```json
{
    "file" : "<div>your html content</div>"
}
```

Third sample will look into all html content inside the directory and output it like this:

```json
{
    "file" : "<div>your html content</div>",
    "file2" : "<div>your html content 2</div>"
}
```




----
**[MIT](LICENSE) LICENSE** <br>
copyright &copy; 2016 Scripts and Pixels.
