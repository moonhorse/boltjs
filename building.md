---
title: Building Bolt Packages
---

<h1>Building Bolt Packages</h1>
Bolt includes a build system that allows you to generate single file packages for your css and js files. A bolt-build.json manifest tells the build script what files to include in your package.

Here is an example bolt-build.json file:
<code>
[
  {
    "provide_common_js_require_function": true
    sources: [
      ["module_name", "path/to/module.js"],
      ["namespace", "../directory/outside/my/project"]
      "another_module.js"
      "a_directory"
    ],
    "package_target": "path/to/package/directory",
    "package_name": "my_package"
  },
  {
    ...
    multiple configs can be provided in a single file
  }
]
</code>

<b>Key points</b>
<ul>
  <li>all file references are relative to the location of the bolt-build.json</li>
  <li>multiple configurations can be provided as a json array</li>
  <li>provide_common_js_require_function should only be included by the bolt package. Eventually we may put everything into one package; however, for now it's important that only the bolt framework package includes this file</li>
  <li>directory references in the bolt-build.json will cause all files to be recursively included within that directory.</li>
  <li>if a namespace is provided in the sources (e.g. ["module_name", "directory"]) files within that directory will be required as require('module_name/path/to/file/from/directory.js').</li>
  <li>any images in a directory you specify in sources will be copied into the package_target directory. This means your css files should be able to reference the images relatively as if they are alongside the css file.</li>

<b>Running bolt-build</b><br/>
Once you run npm-link on your bolt checkout, you'll have access to the bolt-build command. bolt-build takes a few options:
<ul>
  <li> -w : run the build continuously watching for changes to files</li>
  <li> -c : specify an alternate config file other than the default bolt-build.json</li>
  <li> -m: minify the output using uglify.js. package files will be names as package_name.min.js package_name.min.css</li>
</ul>

<h2>Bolt Core</h2>

<b>Views</b>

<ul>
  <li>View: base level view class that provides life cycle, configuration, data binding, and dom access</li>
  <li>Container: base level view class that can contain other views and manage them as a set </li>
  <li>CollectionView: Container view that can be data-bound to a Collection</li>
</ul>

<b>Models</b>
<ul>
  <li>Model: Base level object with observable properties. These should be sub-classed to model the domain of your application</li>
  <li>Collection: Manage a set of models and provide notifications of membership changes.</li>
</ul>

<b>Controllers</b>
<ul>
  <li>Not yet defined in Bolt. Should be lightweight and provide the facility of connecting models and views prior to data-binding.</li>
</ul>

<b>Utilities</b>
<ul>
  <li>Javelin: DOM, Ajax, Class Inheritance, Events (data/DOM) </li>
  <li>Underscore: iterators</li>
  <li>Build System: nodejs script provides CommonJS module api and packages resources into single files</li>
</ul>

