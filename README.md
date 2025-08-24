# 🏜️ arizona
> "reusable vanilla html components"
---
i wanted a system to easily create re-usable html elements and so i made it

add to your site (put in head):
```html
<script src="https://cdn.jsdelivr.net/gh/cabinfvr/arizona@stable/arizona.js"></script>
```

### examples
first, you define the component:
```html
<component>
  <meta name="greeting" username="Joe" />
  Hello, {{username}}!
</component>
```
> note the templating syntax, and the `<meta>` tag. this will be where the metadata for the component goes and also your templating defaults.

then, to call the thing we just made:
```html
<greeting username="World"></greeting>
```
and it will be rendered as:
```html
<div class="greeting">
  Hello, World!
</div>
```

### features
- **variable templating**: use `{{variable}}` syntax to insert dynamic content
- **conditional rendering**: wrap content with `{{#if condition}}...{{/if}}` blocks
- **loops**: iterate arrays with `{{#each items}}...{{/each}}` syntax
- **slots**: use `<slot></slot>` to include content from the component instance
- **attribute casting**: automatically converts "true", "false", numbers, and JSON to proper types
- **default values**: set defaults in the meta tag that can be overridden per instance

### more examples

**conditional rendering:**
```html
<component>
  <meta name="user-status" is_online="false" username="anonymous" />
  <div class="user">
    {{username}}
    {{#if is_online}}
      <span class="online-indicator">●</span>
    {{/if}}
  </div>
</component>

<user-status username="alice" is_online="true"></user-status>
```

**loops:**
```html
<component>
  <meta name="todo-list" items='["buy milk", "walk dog"]' />
  <ul>
    {{#each items}}
      <li>{{this}}</li>
    {{/each}}
  </ul>
</component>

<todo-list items='["code", "sleep", "repeat"]'></todo-list>
```

**slots:**
```html
<component>
  <meta name="card" title="default title" />
  <div class="card">
    <h3>{{title}}</h3>
    <div class="card-content">
      <slot></slot>
    </div>
  </div>
</component>

<card title="my card">
  <p>this content goes in the slot</p>
</card>
```

### how it works
arizona watches the dom for changes and automatically renders your custom components. when you define a component with `<component>` and a meta tag with a name, it becomes available as a custom element throughout your page.

the system is lightweight and doesn't require any build tools - just drop in the script and start defining components.
