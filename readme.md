_This repository has been archived and is now read-only. Please contact one of the fluid-project maintainers if you’d like to request it be unarchived for further development. https://wiki.fluidproject.org/display/fluid/Get+Involved_

# grunt-eslint - Fluid Community Edition

This differs from the upstream version of [grunt-eslint](https://github.com/sindresorhus/grunt-eslint) in that

* It binds to [fluid-eslint](https://github.com/fluid-project/fluid-eslint) rather than [ESLint](https://github.com/eslint/eslint), in order to include a fully working fix for [issue 4931](https://github.com/eslint/eslint/issues/4931)
* It includes a fix for [issue 19](https://github.com/sindresorhus/grunt-eslint/issues/19), outputting the number of linted files, which the grunt-eslint maintainer has refused a fix for

> Validate files with [ESLint](http://eslint.org)

![](screenshot.png)


## Install

```
$ npm install --save-dev grunt-eslint
```


## Usage

```js
require('load-grunt-tasks')(grunt); // npm install --save-dev load-grunt-tasks

grunt.initConfig({
	eslint: {
		target: ['file.js']
	}
});

grunt.registerTask('default', ['eslint']);
```

## Examples

### Custom config and rules

```js
grunt.initConfig({
	eslint: {
		options: {
			configFile: 'conf/eslint.json',
			rulePaths: ['conf/rules']
		},
		target: ['file.js']
	}
});
```

### Custom formatter

```js
grunt.initConfig({
	eslint: {
		options: {
			format: require('eslint-tap')
		},
		target: ['file.js']
	}
});
```
## Two Common Configuration Needs

ESLint has [many configuration options available]([ESLint options](http://eslint.org/docs/developer-guide/nodejs-api#cliengine)); two common ones that are sometimes *gotchas*:

### Specifying valid globals in an individual Javascript file

This prevents ESLint from raising an error when a global expected to be included from another file (such as `fluid` or `jqUnit`) is not defined, as in this example error message:

```
 122:9   error  'fluid' is not defined  no-undef
```

Valid globals can be defined in comments at the top of an individual JS file:

```
/* global fluid, jqUnit */
```

### Specifying node as the environment in an individual Javascript file

There are [fulsome details on configuring the environment](http://eslint.org/docs/user-guide/configuring#specifying-environments), but a common need is to specify that a file should be linted for a node environment. Again, this can be done in comments at the top of an individual JS file:

```
/* eslint-env node, mocha */
```

## Options

See the [ESLint options](http://eslint.org/docs/developer-guide/nodejs-api#cliengine).

In addition the following options are supported:

### format

Type: `string`<br>
Default: `'stylish'`

Name of a [built-in formatter](https://github.com/nzakas/eslint/tree/master/lib/formatters) or path to a custom one.

Some formatters you might find useful: [eslint-json](https://github.com/sindresorhus/eslint-json), [eslint-tap](https://github.com/sindresorhus/eslint-tap).

### outputFile

Type: `string`<br>
Default: `''`

Output the report to a file.

### quiet

Type: `boolean`<br>
Default: `false`

Report errors only.

### maxWarnings

Type: `number`<br>
Default: `-1` *(means no limit)*

Number of warnings to trigger non-zero exit code.


## License

MIT © [Sindre Sorhus](https://sindresorhus.com)
