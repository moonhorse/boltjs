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
