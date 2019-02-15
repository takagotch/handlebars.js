### handlebars.js
---

https://github.com/takagotch/handlebars

https://github.com/wycats/handlebars.js

```js
var source = "<p>Hello, my name is {{name}}. I am from {{hometown}}. I have " + 
             "{{kids.length}} kids:</p>" +
             "<ul>{{#kids}}<li>{{name}} is {{age}}</li>{{/kids}}</ul>";
var template = Handlebars.compile(source);
var data = { "name": "Alan", "hometown": "Somewhere, TX",
             "kids": [{"name": "Jimmy", "age": "12"}, {"name": "Sally", "age": "4"}]};
var result = template(data);
```

```
npm install --handlebars
bower install --save handlebars
```

```js
require('handlebars');
require('handlebars/runtine');

var source = document.getElmentById("entry-template").innerHTML;
var template = Handlebars.compile(source);

var context = {title: "My New Post", body: "This is my first post!"}
var html = template(context);

Handlebrs.registerHelper('link', function(text, url){
  text = Handlebars.Utils.escapeExpression(text);
  url = Handlebars.Utils.escapeExpression(url);
  
  var result = '<a href="' + url + '">' + text + '</a>';
  
  return new Handlebars.SafeString(result);
});

Handlebars.registerHelper('list', function(items, options){
  var out = "<ul>";
  
  for(var i=0, l=items.length; i<l; i++) {
    out = out + "<li>" + options.fn(items[i]) + "</li>";
  }
  
  return out + "</ul>";
});

var context = {
  title: "My First Blog Post!",
  author: {
    id: 47,
    name: "Yehuda Katz"
  },
  body: "My first post. Wheeee!"
};

var context = {
  author: {firstName: "Alan", lastName: "Johnson"},
  body: "I Love Handlebars",
  comments: [{
    author: {firstName: "Yehuda", lastName: "Katz"},
    body: "Me too!"
  }]
};
handlebars.registerHelper('fullName', function(person){
  return person.firstName + "" + person.lastName;
});

var context = {
  items: [
    {name: "Handlebars", emotion: "love'},
    {name: "Mustache", emotion: "enjoy"},
    {name: "Ember", emotion: "want to learn"}
  ]
};
Handlebars.registerHelper('agree_button', function(){
  var emotion = Handlebars.escapExpression(this.emotion),
    name = Handlebars.escapeExpression(this,name);
  
  return new Handlebars.SafeString(
    "<button>[ agree. ]" + emotion + " " + name + "</button>"
  );
});

Handlebars.resigterPartial('userMessage',
  '<{{tagName}}>By {{author.firstName}} {{author.lastName}}</{{tagName}}>'
  + '<div class="body">{{body}}</div>');

var context = {
  author: {firstName: "Alan", lastName: "Johnson"},
  body: "I Love Handlers",
  comments: [{
    author: {firstName: "Yehuda", lastName: "Katz"},
    body: "Me too!"
  }]
};
```

```
<div class="entry">
  <h1>{{title}}</h1>
  <div class="body">
    {{body}}
  </div>
</div>

<script id="entry-template" type="text/x-handlebars-template">
<div class="entry">
  <h1>{{title}}</h1>
  <div class="body">
    {{body}}
  </div>
</div>
</script>

<div class="entry">
  <h1>{{title}}</h1>
  <div class="body">
    {{body}}
  </div>
</div>

<h1>Comments</h1>

<div id="comments">
  {{#each comments}}
  <h2><a href="/posts/{{../permalink}}#{{id}}">{{title}}</a></h2>
  <div>{{body}}</div>
  {{/each}}
</div>

{{permalink}}
{{#each comments}}
  {{../permalink}}
  
  {{#if title}}
    {{../permalink}}
  {{/if}}
{{/each}}

<p>{{./name}} or {{this/name}} or {{this.name}}</p>

<div class="entry">
  {{!-- only output author name if an author exists --}}
  {{#if author}}
    <h1>{{author.firstName}} {{author.lastName}}</h1>
  {{/if}}
</div>
```
