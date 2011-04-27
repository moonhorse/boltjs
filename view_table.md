---
title: Table View
layout: default
sectionview: true
---

<h1>Table View</h1>

The Table view is possibly the most complex view in Bolt.  It is a highly performant infinite scrolling widget which utilises progressive rendering and CSS transforms to scroll quickly through any amount of data.

{% highlight javascript %}
// implement the table delegate protocol
var tableDelegate = (function() {
  return {

    sectionHeaderAtIndex: function() {
      return null;
    },

    heightForSectionHeader: function(section) {
      return 0;
    },

    heightForRowInSection: function(row, section) {
      return 51;
    },

    numberOfSections: function() {
      return 1;
    },

    numberOfRowsInSection: function() {
      return 100000;
    },

    cellForRowInSection: function(row, section) {
      return buildRandomRow(row)
    },
  };
})();

// configure a table with our delegate
var table = new Table({
  height: '480px',
  width: '320px',
  style: {
    background: '#ccc'
  },
  delegate: tableDelegate
});

var example = document.getElementById('example');
table.placeIn(example);
table.refresh();
{% endhighlight %}

