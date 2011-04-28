---
title: Building Views
section: view
layout: default
---

<h1>Building Views</h1>

<p>
  Bolt uses the concept of a <b>Builder</b> to instantiate views, making it very easy and concise to create both simple views and highly complex nested user interfaces.  The <b>Builder</b> also makes it simple to add listeners to views, both for DOM and custom events, as well as setting initial values for a views properties.
</p>

<p>
  A simple example is creating a Button view.  Call the builders <b>build</b> function, telling it the type of view to create, <b>Button</b>, the initial value of it's <b>value</b> property, and what to do when it is clicked or tapped using the <b>action</b> property.
</p>

{% highlight javascript %}
  var Button = require('views/button').Button;
  var builder = require('builder');

  var myButton = builder.build({
    // Define the type of view to build
    view: Button,

    // Set the initial value of the 'value' property
    value: 'Click Me',

    // Define an action to perform when this button is clicked or tapped.
    action: function(button, event) {
      alert('You clicked the button with the value ' + button.getValue());
    }
  });
  myButton.placeIn(document.body);

{% endhighlight %}

<h2>Building Nested Views</h2>

<p>
  The example above is quite simple, showing how to build a single view.  However, the real power of the <b>Builder</b> begins to show when constructing many views in a hierarchical layout.
</p>

<p>
  The example below shows a more complex example.  It uses the 
<a href="view_layouts.html">VBox and HBox layout views</a> to create 

<ul>
  <li>a header at the top</li>
  <li>two buttons in the middle</li>
  <li>two panes, each of which are hidden or shown when one of the buttons is pressed</li>
</ul> 
</p>

{% highlight javascript %}

  var VBox = require('views/layout/vbox').VBox;
  var HBox = require('views/layout/vbox').HBox;

  // Define a new view called MyPaneLayout
  require('javelin/core').createClass({
    
    name: 'MyPaneLayout',

    extend: VBox,

    members: {
      render: function() {

        // Call the setLayout function, which uses the builder to create
        // it's sub views
        this.setLayout([
          {
            className: 'header',
            content: 'Choose A Pane'
          },
          {
            // Define a horizontally laid out container with two buttons
            view: HBox,
            childViews: [
              // Create two buttons.  Note how the 'action' is bound to
              // 'onSelectPane'.  Because the 'MyPaneLayout' view is creating
              // the Button, a listener can be added to the Button as a 
              // string telling it the name of the funtion on the Buttons
              // owner to call
              {
                view: Button,
                value: 'Pane 1',
                action: 'onSelectPane'
              },
              {
                view: Button,
                value: 'Pane 2',
                action: 'onSelectPane'
              }
            ]
          },
          // Define the two panes which will be shown/hidden when a button
          // is clicked.  Since no view type or tagName is provided, these
          // default to being simple DIV elements
          {
            ref: 'pane1',
            style: {
              height: '200px',
              backgroundColor: '#bbb'
            },
            content: 'This is Pane 1'
          },
          {
            ref: 'pane2',
            style: {
              height: '200px',
              backgroundColor: '#333',
              color: 'white',
              display: 'none'
            },
            content: 'This is Pane 2'
          }
        ]);
      },

      onSelectPane: function(button, event) {
        var value = button.getValue();

        // Check which button was clicked, and show/hide the
        // the panes  
        if (value == 'Pane 1) {
          this.findRef('pane1').setStyle({display: ''});
          this.findRef('pane2').setStyle({display: 'none'});
        } else {
          this.findRef('pane1').setStyle({display: 'none'});
          this.findRef('pane2').setStyle({display: ''});
        }
      }
    }
  });

  require('builder').build({
    view: 'MyPaneLayout'
  }).placeIn(document.body);



  

{% endhighlight %}
