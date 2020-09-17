---
id: reverseSnippetItem
---

Returns a string with highlighted and escaped non-matching parts of an Algolia hit snippet.

# Example

```js
import { reverseSnippetItem } from '@algolia/autocomplete-js';

const item = {}; // fetch an Algolia hit
const reverseSnippetedValue = reverseSnippetItem({
  item,
  attribute: 'query',
});
```

# Reference

## Params

### `item`

> `AlgoliaHit` | required

The Algolia hit to retrieve the attribute value from.

### `attribute`

> `string` | required

The attribute to retrieve the snippet value from.

### `highlightPreTag`

> `string` | defaults to `<mark>`

The HTML tag to prefix the value with.

### `highlightPostTag`

> `string` | defaults to `</mark>`

The HTML tag to suffix the value with.

### `ignoreEscape`

> `string[]` | defaults to `[]`

The characters to skip from escaping.