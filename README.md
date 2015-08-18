# Meteor Simple Todos
Small todo list app using Meteor JS

Meteor js

Interesting things to note:
can be run on iOS or Android
We can assign any properties to the task object, such as the time created, since we don't ever have to define a schema for the collection.

##Install/Run Android:
```js
meteor install-sdk android
meteor add-platorm android
meteor run android
```
References: Building Apps with Meteor.js (34:08 mins)
https://www.youtube.com/watch?v=SYqyWff6iMQ&list=PLpmzV7Tixihrz8lOOv2xfRb-pnCr0dV4C&index=4&spfreload=10

##Installing JDK
https://github.com/meteor/meteor/wiki/Mobile-Dev-Install:-Android-on-Mac#jdk

##Run Android Device:
enable USB Debugging and make sure you quit the Android emulator
```js
meteor run android-device
```

If you want to point your app to the server you deployed in the previous step, run:
```js
meteor run android-device --mobile-server my_app_name.meteor.com
```

##Install/Run iOS:
```js
meteor install-sdk ios
meteor add-platform ios
meteor run ios
```

##Templates:
in view
```js
{{> templateName}}
```
in javascript
```js
Template.templateName
```

##View logic:
```js
{{#each}}
```
or 
```js
{{#if}}
```
ex.
```js
{{#each tasks}}

{{/each}}
```

##Mongo:
###Collections:
in js create new collection
```js
Tasks = new Mongo.Collection("tasks”);
```
assign it to a variable
```js
tasks: function () {
      return Tasks.find({});
    }
```

##Console:
```js
meteor mongo
```
insert a new record
```js
db.tasks.insert({ text: "Hello world!", createdAt: new Date() });
```

##Event Listeners:
Add listener to template by adding this in your js
```js
Template.templateName.events(…)
```
ex. submit event on .new-task . “event.target” is our form element and the value is “event.target.text.value"
```js
Template.body.events({
    "submit .new-task": function (event) {
	// Some JS code
	}
});
```
this is for this form
```js
<form class="new-task">
  <input type="text" name="text" placeholder="Type to add new tasks" />
</form>
```

##Sorting:
pass in the sort option with the variable you want to sort by
```js
Tasks.find({}, {sort: {createdAt: -1}});
```
ex.
```js
tasks: function() {
	return Tasks.find({}, {sort: {createdAt: -1}});
}
```

this:
this refers to an individual task object. In a collection, every inserted document has a unique _id field that can be used to refer to that specific document
```js
this._id
```

##Update:
takes 2 arguments. first the selector, second is what to do with that object. “$set” used to toggle checked field
```js
Tasks.update(this._id, {
	$set: {checked: ! this.checked}
});
```

##Delete:
```js
Tasks.remove(this._id)
```

##Deploying:
give it a name and deploy to meteor for testing
```js
meteor deploy my_app_name.meteor.com
```
ex.
```js
http://ac-simple-todos.meteor.com/
```

##Session Variables:
Use the Session object along with “get” and “set” functions
```js
Session.set(“variableName", value);
```
ex. 
```js
Session.set("hideCompleted", event.target.checked);
```
or
```js
Session.get("hideCompleted”)
```












