minijasminenode-relaunchable
============================

Experimental hack on minijasminenode v1.1.1 originally by Julie Ralph ju.ralph@gmail.com, part of protractor v1.3.1, used by package asyncshell http://github.com/carrascoMDD/asyncshell to reset state kept in certain properties, such that it allows relaunching protractor multiple times within the same NodeJS operating system process.

original work
-------------

[See original minijasminenode](https://github.com/juliemr/minijasminenode)



Based on Jasmine-Node, but minus the fancy stuff. This node.js module makes Pivotal Lab's Jasmine (http://github.com/pivotal/jasmine) spec framework available in node.js or via the command line.


features
--------

MiniJasmineNode exports a library which
- places Jasmine in Node's global namespace, similar to how it's run in a browser
- adds asynchronous testing with done().
- adds result reporters for the terminal.
- adds focused testing with `iit` and `ddescribe`.
- adds the ability to load tests from file.

The module also contains a command line wrapper that can be run with

    minijasminenode specDir/mySpec1.js specDir/mySpec2.js

For more info on the command line wrapper

    minijasminenode --help

installation
------------

Get the library with

    npm install minijasminenode

Or, install globally

    npm install -g minijasminenode

If you install globally, you can use minijasminenode directly from the command line

    minijasminenode mySpecFolder/mySpec.js

usage
-----

```javascript
    var miniJasmineLib = require('minijasminenode');
    // At this point, jasmine is available in the global node context

    // Add your tests by filename.
    miniJasmineLib.addSpecs('myTestFolder/mySpec.js');

    // If you'd like to add a custom Jasmine reporter, you can do so. Tests will
    // be automatically reported to the terminal.
    miniJasmineLib.addReporter(myCustomReporter);

    // Run those tests!
    miniJasmineLib.executeSpecs();
```

You can also pass an options object into `executeSpecs`

````javascript
    var miniJasmineLib = require('minijasminenode');

    var options = {
      // An array of filenames, relative to current dir. These will be
      // executed, as well as any tests added with addSpecs()
      specs: ['specDir/mySpec1.js', 'specDir/mySpec2.js'],
      // A function to call on completion.
      // function(runner, log)
      onComplete: function(runner, log) { console.log('done!'); },
      // If true, display spec and suite names.
      isVerbose: false,
      // If true, output nothing to the terminal. Overrides other printing options.
      silent: false,
      // If true, print colors to the terminal.
      showColors: true,
      // If true, include stack traces in failures.
      includeStackTrace: true,
      // Time to wait in milliseconds before a test automatically fails
      defaultTimeoutInterval: 5000,
      // If true, print timestamps for failures
      showTiming: true,
      // Print failures in real time.
      realtimeFailure: false
    };
    miniJasmineLib.executeSpecs(options);
````

to run the tests
----------------
`./specs.sh`

This will run passing tests as well as show examples of how failures look. To run only passing tests, use `npm test` or `./bin/minijn spec/*_spec.js`
