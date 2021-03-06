# gulp-sketch [![Build Status](https://travis-ci.org/cognitom/gulp-sketch.svg?branch=master)](https://travis-ci.org/cognitom/gulp-sketch) [![Stories in Ready](https://badge.waffle.io/cognitom/gulp-sketch.png?label=ready&title=Ready)](https://waffle.io/cognitom/gulp-sketch)

A [SketchTool](http://bohemiancoding.com/sketch/tool/) plugin for [gulp](https://github.com/wearefractal/gulp).


## Install

Download [SketchTool](http://sketchtool.bohemiancoding.com/sketchtool-latest.zip) and install it to your environment by hand or by using the script below.

```bash
$ curl -L https://raw.githubusercontent.com/cognitom/dotfiles/master/lib/sketchtool.sh | sudo sh
```

Then, install `gulp-sketch` plugin via `npm`.

```bash
$ npm install gulp-sketch --save-dev
```


## Usage

```javascript
var gulp = require("gulp");
var sketch = require("gulp-sketch");

gulp.task('sketch', function(){
  return gulp.src("./src/sketch/*.sketch")
    .pipe(sketch({
      export: 'slices',
      formats: 'png'
    }))
    .pipe(gulp.dest("./dist/images/"));
});
```

or write it in CoffeeScript.

```coffeescript
gulp = require 'gulp'
sketch = require 'gulp-sketch'

gulp.task 'sketch', ->
  gulp.src './src/sketch/*.sketch'
  .pipe sketch
    export: 'slices'
    formats: 'png'
  .pipe gulp.dest './dist/images/'
```


## Options

The options are the same as what's supported by `SketchTool`.

- `export`: pages,artboards,slices
- `formats`: png,jpg,pdf,eps,svg
- `scales`: 1.0,2.0
- `items`: List of artboard/slice names or ids to export. The default is to export all artboards/slices (optional).
- `bounds`:
- `saveForWeb`: Export web-ready images (optional, defaults to NO).
- `compact`: Export in compact form. Currently only relevant for SVG export. (optional, defaults to NO).
- `trimmed`: Export images trimmed. (optional, defaults to NO).

Additionally, it has `clean` option for exporting SVG.

- `clean`: Remove Sketch namespaces and metadata from SVG (optional, defaults to NO). See [clean-sketch](https://github.com/overblog/clean-sketch).


## Layer Naming

When exporting slices, the name of layer is the key to decide the name of the file exported.

- If you have the layer named `yellow` and export it with option `{ format:'png' }`, the exported file would be `yellow.png`.
- If you have the layer named `square/yellow` and export it with same option, the file would be exported as `yellow.png` under `square/` directory.

![Layer Naming](doc/layer-naming.png)

Bohemian Coding mentioned about it in [their article](http://bohemiancoding.com/sketch/support/documentation/11-exporting/2-slices.html).

> You can give each of your slices their own name, and this is the name that will be used when you save your slice to disk.
> A neat trick is that you if you include a slash (a '/') it will create subfolders for your first. For example, if you named your slice foo/bar.png, it would first create a folder named 'foo' and then create a image named 'bar.png' in there.
