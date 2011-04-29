---
title: Getting Started with BoltJS
layout: default
---

<h1>Getting Started</h1>

<h2>Checking out the code</h2>
<p>
  The first step to working with Bolt is to check out the code.  Bolt will soon be available on GitHub, but for now you must be a Facebook developer to get it.  Search for instructions on downloading it on the internal wiki.
</p>

<h2>Installing Node</h2>
<p>
  Bolt uses a build script to create it's packaged files, and to build a single package file for individual HTML5 apps.  This script is written in JavaScript and is executed using <a href="http://nodejs.org">NodeJS</a>.  The current version of Node, v0.4.7, runs on Mac and Linux, and can work on Windows through CygWin.  For this reason, it's easier to work with Bolt if you're not on Windows.  This is a situation we're looking into, but Joyent (Node maintainers) are working hard to get it working on Windows too, so this issue might just solve itself soon. 
</p>

<p>
  So, go ahead and <a href="https://github.com/joyent/node/wiki/Installation">install Node</a>.
</p>

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

<h2>Setting Up An Application</h2>

<p>
  
</p>
