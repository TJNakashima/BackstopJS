# BackstopJS
BackstopJS automates visual regression testing of your responsive web UI by comparing DOM screenshots over time. More info can be found on https://github.com/garris/BackstopJS/blob/master/README.md.

## Report
![BackstopJS browser report](http://garris.github.io/BackstopJS/assets/backstopjs_new_ui_.png)
![BackstopJS cli report](http://garris.github.io/BackstopJS/assets/cli-report.png)

## Install BackstopJS now
$ npm install -g backstopjs

### Getting started
**If you don't already have BackstopJS set up...**
BackstopJS can create a default configuration file and project scaffolding in your current working directory. Please note: this will overwrite any existing files!

`cd` to your project's directory and run...

```sh
$ backstop init
```

### Working with your config file

By default, BackstopJS places `backstop.json` in the root of your project. And also by default, BackstopJS looks for this file when invoked.

#### Required config properties

As a new user setting up tests for your project, you will be primarily concerned with these properties...

**`id`** – Used for screenshot naming. Set this property when sharing reference files with teammates -- otherwise omit and BackstopJS will auto-generate one for you to avoid naming collisions with BackstopJS resources.

**`viewports`** – An array of screen size objects your DOM will be tested against.  Add as many as you like -- but add at least one.

**`scenarios`** – This is where you set up your actual tests. The important sub properties are...

- **`scenarios[n].label`** – Required. Also used for screenshot naming.
- **`scenarios[n].url`** – Required. Tells BackstopJS what endpoint/document you want to test.  This can be an absolute URL or local to your current working directory.
- **`scenarios[n].viewports`** – An array of screen size objects your DOM will be tested against. This configuration will override the ones provided by default configuration.

_TIP: no other SCENARIO properties are required. Other properties can just be added as necessary_

### Generating test bitmaps

```sh
$ backstop test
```

This will create a new set of bitmaps in `bitmaps_test/<timestamp>/`

Once the test bitmaps are generated, a report comparing the most recent test bitmaps against the current reference bitmaps will display.

Pass a `--config=<configFilePathStr>` argument to test using a different config file.

**Tip** To use a js-module as a config file, just explicitly specify your config filepath and point to a `.js` file. _Just be sure to export your config object as a node module._

Pass a `--filter=<scenarioLabelRegex>` argument to just run scenarios matching your scenario label.

Pass a `--docker` flag to render your test in a Docker container -- this will help with consistency if you are attempting to compare references across multiple environments.

### Approving changes

```sh
$ backstop approve
```

When running this command, all images (with changes) from your most recent test batch will be promoted to your reference collection. Subsequent tests will be compared against your updated reference files.

Pass a `--filter=<scenarioLabelRegex>` argument to promote only the test captures matching your scenario label.

**Tip**: Remember to pass a `--config=<configFilePathStr>` argument if you passed that when you ran your last test.

## Steps to use
1. Copy package.json
2. npm install
3. node ./node_modules/backstopjs/cli/index.js init
4. node ./node_modules/backstopjs/cli/index.js test
5. node ./node_modules/backstopjs/cli/index.js approve
6. node ./node_modules/backstopjs/cli/index.js test*
