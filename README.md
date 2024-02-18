Search Library Genesis programmatically using an enhanced Python library. This fork extends the original `libgen-api` by [Harrison Broadbent](https://github.com/harrison-broadbent) with added features like direct download links and book cover links.

## Contents

- [Getting Started](#getting-started)
- [Basic Searching](#basic-searching)
- [Filtered Searching](#filtered-searching)
  - [Filtered Title Searching](#filtered-title-searching)
  - [Filtered Author Searching](#filtered-author-searching)
  - [Non-exact Filtered Searching](#non-exact-filtered-searching)
  - [Filter Fields](#filter-fields)
- [Resolving mirror links](#resolving-mirror-links)
- [More Examples](#more-examples)
- [Further Information](#further-information)
- [Testing](#testing)
- [Contributors](#contributors)

---

Please ⭐ if you find this useful!

---

## Getting Started

Install the package -

```
pip install libgen-api-enhanced
```

Perform a basic search -

```python
# search_title()

from libgen_api_enhanced import LibgenSearch
s = LibgenSearch()
results = s.search_title("Pride and Prejudice")
print(results)
```

Check out the [results layout](#results-layout) to see how the results data is formatted.

## Basic Searching:

**_NOTE_**: All queries must be at least 3 characters long. This is to avoid any errors on the LibGen end (different mirrors have different requirements, but a minimum of 3 characters is the official limit).

Search by title or author:

### Title:

```python
# search_title()

from libgen_api_enhanced import LibgenSearch
s = LibgenSearch()
results = s.search_title("Pride and Prejudice")
print(results)
```

### Author:

```python
# search_author()

from libgen_api_enhanced import LibgenSearch
s = LibgenSearch()
results = s.search_author("Jane Austen")
print(results)
```

## Filtered Searching

Skip to the [Examples](#filtered-title-searching)

- You can define a set of filters, and then use them to filter the search results that get returned.
- By default, filtering will remove results that do not match the filters exactly (case-sensitive) -
  - This can be adjusted by setting `exact_match=False` when calling one of the filter methods, which allows for case-insensitive and substring filtering.

### Filtered Title Searching

```python
# search_title_filtered()

from libgen_api_enhanced import LibgenSearch

tf = LibgenSearch()
title_filters = {"Year": "2007", "Extension": "epub"}
titles = tf.search_title_filtered("Pride and Prejudice", title_filters, exact_match=True)
print(titles)
```

### Filtered Author Searching

```python
# search_author_filtered()

from libgen_api_enhanced import LibgenSearch

af = LibgenSearch()
author_filters = {"Language": "German", "Year": "2009"}
titles = af.search_author_filtered("Agatha Christie", author_filters, exact_match=True)
print(titles)
```

### Non-exact Filtered Searching

```python
# search_author_filtered(exact_match = False)

from libgen_api_enhanced import LibgenSearch

ne_af = LibgenSearch()
partial_filters = {"Year": "200"}
titles = ne_af.search_author_filtered("Agatha Christie", partial_filters, exact_match=False)
print(titles)

```

### Filter Fields

You can filter against any of the Library Genesis column names, which are given as -

```python
col_names = [
        "ID",
        "Author",
        "Title",
        "Publisher",
        "Year",
        "Pages",
        "Language",
        "Size",
        "Extension",
        "Mirror_1",
        "Mirror_2",
        "Mirror_3",
        "Mirror_4",
        "Mirror_5",
        "Edit",
    ]
```

## More Examples

See the [testing file](test/manualtesting.py) for more examples.

## Results Layout

Results are returned as a list of dictionaries:

```json
[
  {
    "Author": "John Smith",
    "Edit": "http://example.com",
    "Extension": "epub",
    "ID": "00000",
    "Language": "German",
    "Mirror_1": "http://example.com",
    "Mirror_2": "http://example.com",
    "Mirror_3": "http://example.com",
    "Mirror_4": "http://example.com",
    "Mirror_5": "http://example.com",
    "Pages": "410",
    "Publisher": "Publisher",
    "Size": "1005 Kb",
    "Title": "Title",
    "Year": "2021"
  }
]
```

## Further information

- If there are no results, the library will return an empty array.
- All fields are strings.
- If a value is not present, the field will contain an empty string.
- Some listings will have page count listed in the form of "count[secondary-count]" as this is how they appear on Library Genesis.
- Only the first page of results (max. 25) will be returned.

## Testing

libgen-api-enhanced uses Pytest to run unit tests.

To run the tests -

- ## Clone this repo -
  ```
  git clone https://github.com/onurhanak/libgen-api-enhanced.git && cd libgen-api-enhanced
  ```
- ## Install dependencies with -
  ```
  pip install .
  ```
- ## Run tests with -
  ```
  pytest
  ```

## Contributors

A massive thank you to those that have contributed to this project!

Please don't hesitate to raise an issue, or fork this project and improve on it.

Thanks to the following contributors -

- [harrison-broadbent](https://github.com/harrison-broadbent)
- [calmoo](https://github.com/calmoo)
- [HENRYMARTIN5](https://github.com/HENRYMARTIN5)

## New Distribution

(for my own reference)

1. python3 -m pip install --user --upgrade setuptools wheel
2. python3 -m pip install --user --upgrade twine
3. python3 setup.py sdist bdist_wheel
4. python3 -m twine upload dist/\*
