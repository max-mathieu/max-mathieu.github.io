---
layout: post
title: A simple recursive object viewer for VueJS
tags:
  - vuejs
---

I needed a quick way to turn some metadata into a nested `<ul>` list.
Turns out, VueJS supports recursive components, so I just put together a simple recursive `ObjectViewer.vue` component.

The very simple version looks like this:

{% raw %}
```html
<template>
  <ul>
    <li v-for="(value, key) in object">
      {{{ key }}:
      <object-viewer v-if="typeof value == 'object'" :object="value"></object-viewer>
      <span v-else>{{ value }}</span>
    </li>
  </ul>
</template>

<script>
  export default {
    props: [ 'object' ]
  };
</script>
```
{% endraw %}

To use it:

```html
<template>
  <object-viewer :object="metadata"></object-viewer>
</template>

<script>
  export default {
    data() {
      return {
        metadata: {
          date: '2017-01-01',
          tags: [ 'tag1', 'tag2' ],
          file: {
            extension: 'vue',
            size: 789
          }
        }
      };
    }
  };
</script>
```

And you get something like this:

- date: 2017-01-01
- tags:
  - 0: tag1
  - 1: tag1
- file:
  - extension: vue
  - size: 789
      
And here you have it: a simple example of a VueJS recursive component. It just works™
