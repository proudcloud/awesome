# Ember

##Development

###Tools
- [Ember-cli](http://www.ember-cli.com/) for project management
- [ES2015/Babel](https://babeljs.io/) as our JS flavor
- [Sass](http://sass-lang.com/) as our CSS flavor
- [Emblem](http://emblemjs.com/) for templates
- [Ember-data](https://github.com/emberjs/data) for data management

###Practices
- Favor [Ember Object Model](http://guides.emberjs.com/v1.11.0/object-model/classes-and-instances/) over plain javascript

####Routes
- Ember routes are tightly coupled with view rendering, but let's maintain restful routing as much as possible

####Models
- Use [ActiveModel Adapter](http://emberjs.com/api/data/classes/DS.ActiveModelAdapter.html) for data serialization/deserialization
- Load data in store as needed
- Set relationships as async true as needed (be mindful that setting relationships as async true changes the behavior of certain functions)

```javascript
//in models/sample.js
export default DS.Model.extend({
  sampleRelationship: DS.belongsTo('anotherModel', {async: true}),
});

sampleInstance.get('sampleRelationship'); //Will return a promise object

//set to async:false
sampleInstance.get('sampleRelationship') //Will return the model

```

####Controllers
- Keep application level logic in controllers.

```javascript
//route transitions
this.transitionToRoute('sample.route');

//data manipulation
sampleModel.save();
sampleModel.destroy();

//ajax requests
Ember.$.ajax('/sample_url');
```

- Keep api requests logic in one mixin/class and just require it in controllers as needed.

####Templates

####Components
- favor components over views
- always declare your component's name in its classNames property

```javascript
//in sample-component.js
export default Ember.Component.extend({
  classNames: ['sample-component']
});
```

- always declare layout related classes in component instantation

```javascript
//in sample-component.js
export default Ember.Component.extend({
  //Don't do this
  classNames: ['sample-component', 'col-md-5']
});

//instead do it this way
//in page.emblem
sample-component class='col-md-5'
```

- Avoid application level logic here

##Helpful Resources
- ember-cli 101 by Adolfo Builes
- Ember [Blog](http://emberjs.com/blog/) - Ember is in active development, we need to sync our practices with new trends.
