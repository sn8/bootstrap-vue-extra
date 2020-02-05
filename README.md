# bootstrap-vue-extra

Useful components for [bootstrap-vue](https://bootstrap-vue.js.org):

* Breadcrumbs
* DeclarativeForm
* Loading
* LoadingButton
* Pagination
* Toastr

## Install
With yarn:
```
yarn add bootstrap-vue-extra
```
With npm:
```
npm i bootstrap-vue-extra
```

## Usage

```vue
<template>
  <loading :is-loading="true" />
</template>

<script>
import { Loading } from 'bootstrap-vue-extra'

export default {
  name: 'Foo',
  components: { Loading }
}
</script>
```
