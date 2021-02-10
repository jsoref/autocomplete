---
id: introduction
title: What is Autocomplete?
---
import { AutocompleteExample } from '@site/src/components/AutocompleteExample';
import { AutocompleteDocSearchItem } from '@site/src/components/AutocompleteDocSearchItem';
import { getAlgoliaHits } from '@algolia/autocomplete-js';
import algoliasearch from 'algoliasearch/lite';
const searchClient = algoliasearch(
  'BH4D9OD16A',
  'a5c3ccfd361b8bcb9708e679c43ae0e5'
);

Autocomplete is an open-source, production-ready JavaScript library for building autocomplete experiences.

A user types into an input, and the autocomplete "completes" their thought by providing full terms or results: this is the very base of an autocomplete experience.

For example, try typing the letter "s" in the search box below.

<AutocompleteExample
  getSources={({ query }) => {
    return [
      {
        sourceId: 'docsearch',
        getItems() {
          return getAlgoliaHits({
            searchClient,
            queries: [
              {
                indexName: 'autocomplete',
                query,
                params: {
                  hitsPerPage: 5,
                  attributesToSnippet: [
                    'content:10',
                    'hierarchy.lvl0:10',
                    'hierarchy.lvl1:10',
                    'hierarchy.lvl2:10',
                    'hierarchy.lvl3:10',
                    'hierarchy.lvl4:10',
                    'hierarchy.lvl5:10',
                    'hierarchy.lvl6:10',
                  ],
                  snippetEllipsisText: '…',
                },
              },
            ],
          });
        },
        getItemUrl({ item }) {
          return item.url;
        },
        templates: {
          item({ item }) {
            return (
              <AutocompleteDocSearchItem
                hit={item}
                breadcrumb={Object.values(item.hierarchy)
                  .filter(Boolean)
                  .slice(0, -1)}
              />
            );
          },
        },
      },
    ];
  }}
/>

You can directly navigate to documentation on concepts like "<strong><u>s</u></strong>ources" and "<strong><u>s</u></strong>tate". If you continue typing, say "st", the results update. You see pages having to do with "<strong><u>st</u></strong>ate," "getting <strong><u>st</u></strong>arted," and "<strong><u>st</u></strong>atic sources."

**Autocomplete is now a ubiquitous part of most search experiences.** Search providers like Google, e-commerce sites like Amazon, and messaging apps like Slack all offer autocomplete experiences on mobile and desktop.

While the search experience on this site displays links to pages, autocomplete experiences frequently show completed search terms. If you start a search by typing the letter "j" into Google, it suggests search terms like "javascript", "jest", "jsonlines", etc. Selecting one of these lands you on the search results page for the term.

This experience minimizes typing, which is particularly impactful on mobile. It enables users to find what they're looking for quicker. It also exposes them to searches, products, or pages they may not have thought of but are interested in anyway.

You may have already used Autocomplete-powered UIs. The [Algolia](https://www.algolia.com/doc/), [React Native](https://reactnative.dev/), [Tailwind CSS](https://tailwindcss.com/docs), and other documentation websites use Autocomplete via the [Algolia DocSearch](https://docsearch.algolia.com/) project. This library is flexible enough to power more than just documentation search though. **It's designed to help you build interactive and accessible autocomplete experiences, regardless of your use case.**

## What this library provides

Autocomplete is a JavaScript library that lets you quickly build autocomplete experiences. All you need to get started is:
- A container to inject the experience into
- Data to fill the autocomplete with

The data that populates the autocomplete results are called [sources](sources). You can use whatever you want in your sources: a static set of searches terms, search results from an external source like an [Algolia](https://www.algolia.com/doc/guides/getting-started/what-is-algolia/) index, recent searches, and more.

By configuring just those two required parameters ([`container`](autocomplete-js/#container) and [`getSources`](autocomplete-js/#getsources)) you can have an interactive autocomplete experience. **The library creates an input and provides the interactivity and accessibility attributes, but you're in full control of the DOM elements to output.**

You don't have to display just suggested search terms, you can display links for actual results themselves (rather than links to results pages) or even display "actions" that a user can take from within an autocomplete. For example, you could let your users turn dark mode on, directly from an autocomplete, if they begin to type "darkmode".

You can also display different data types (such as suggested search terms, product results, and actions) differently. The format of each data type and layout is customizable.

## What this library doesn't provide

Unlike [Algolia InstantSearch](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/), Autocomplete doesn't provide a library of ready-made UI widgets. You're in control of the full rendering of your autocomplete experience, and the library provides everything you need to make it functional and accessible.

You're also in charge of providing the collection of items to display. You can easily plug Algolia results using [`getAlgoliaHits`](getAlgoliaHits-js) if you want, but you're free to use Autocomplete with any data sources you want.

Ready to learn more? Move on to [Getting Started](getting-started) to see a basic example in action.