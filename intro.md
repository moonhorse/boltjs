---
title: Introduction
layout: default
---

Introduction to BoltJS
======================

BoltJS is a UI framework designed to be compact, fast and powerful.  It is written entirely in JavaScript and runs in the browser, needing no server backend.  While BoltJS can be used in a progressive enhancement approach, it is primarily designed for UIs that are built mostly, if not completely, in the browser.

<b>Built on Javelin</b>

Bolt is built on top of Javelin (http://javelinjs.com), from which it uses the event delegation and class declaration features, as well as various utility methods.  This ensures that Bolt does not duplicate code already present in the Facebook codebase, helping it stay lightweight and reuse patterns familiar to Facebook developers. 	

<b>Highly Targeted</b>

Bolt is highly targeted, supporting everything Buffy and Facebook need, and nothing it doesn't.  Bolt is not a complete JavaScript toolkit, and doesn't include every single utility function a developer will ever need.  Instead it is a view (or widget) compositing and data binding framework.

<b>Modules and CommonJS</b>

Bolt modules are defined using a popular standard called CommonJS, first popularized by the NodeJS community.  This ensures that each module is completely self contained, with no global variables being created.  CommonJS has been integrated with Haste on the server side, and so is also very easy to deploy in a non-mobile app context.
<a href="http://wiki.commonjs.org/wiki/Modules/1.1.1">Common JS Module Specification</a>

<b>Complex Widgets Made Simple(r)</b>

Bolt makes it very simple to composite many different widgets together, lay them out in a reliable fashion, listen to their events and synchronize their data models.  This is achieved using
<ul>
  <li>A Builder which creates an infinitely deep hierarchy of child widgets using a JSON schema. </li>
  <li>Layout classes that position their child elements in either horizontal or vertical positions, complete with support for relative sizing of child elements</li>
  <li>Combining the Javelin event delegation framework with the concept of view "owners".  Any view that creates child views automatically becomes the "owner" of this views, and can add event listeners to it's children during the build process. </li>
  <li>A flexible data-binding framework with support for individual models and collections of models.</li>
</ul>

