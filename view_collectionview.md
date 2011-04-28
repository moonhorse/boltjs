---
title: Collection Views
section: view
layout: default
---

<h1>Collection Views</h1>

<p>
  A <b>CollectionView</b> is a which constructs child views by listening to membership events on a <a href="collection.html">Collection</a>.  When a model is added, removed or updated in a collection, the <b>CollectionView</b> will add, remove or update the corresponding child view.
</p>

<p>
  There are two ways to use CollectionView, programmatic and declarative.  Which you use depends on the situation.
</p>

<h2>Programmatic View Declaration</h2>
<p>
  <b>CollectionView</b> contains the method <b>viewForModel</b> which can be overridden by a child class to define what view should be created when a given <a href="model.html">Model</a> is added to the <a href="collection.html">Collection</a>.  The <b>CollectionView</b> then takes care of inserting that <a href="view.html">View</a> in the correct position.  If the model that was used to create that View is ever removed from the Collection, the View will also be cleanly removed from the CollectionView.  The example shows a simple example of this.
</p>

{% highlight javascript %}
  var CollectionView = require('collection_view').CollectionView;
  var Collection = require('collection').Collection;
  var Model = require('model').Model;

  // Declare two models, containing a 'type' and a 'value'
  var model1 = new Model({type: 'url', value: 'http://facebook.com'});
  var model2 = new Model({type: 'email', value: 'helpdesk@facebook.com'});

  var InputCollectionView = require('javelin/core').createClass({

    // Call this class InputCollectionView
    name: 'InputCollectionView',

    // Extend the base CollectionView class
    extend: CollectionView,

    members: {

      // Define the viewForModel function.  This should be all you need to define
      // and the CollectionView class will take care of the rest
      viewForModel: function(model) {
        // Get the type of the model, which we set above
        // This is used to decide which view we create
        var type = model.get('type');
        var view;

        switch(type) {
          
          case 'url':
            view = this.build({
              // Assume that we have some custom input for urls
              view: CustomUrlInput
            });
            break;
          case 'email':
            view = this.build({
              // Assume that we have some custom input for emails
              view: CustomEmailInput
            });
            break;
        }

        // Bind the model to the view so that any changes to its value will
        // be reflected in the view
        view.setBinding(model, [{property: 'value'}]);

        return view;
      }
    }
  });

  // Create an instance of our customized CollectionView
  var collView = new InputCollectionView();

  // Insert it into the DOM
  collView.placeIn(document.body);

  // Get the default Collection from the CollectionView.  It is also possible
  // to pass an existing Collection to the CollectionView
  var coll = collView.getCollection();

  // Add the two models to the Collection.  This will cause two new Views to be
  // inserted into the InputCollectionView
  coll.add(model1);
  coll.add(model2);

{% endhighlight %}
