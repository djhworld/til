+++
title = "Use strings.TrimFunc to trim suffixes/prefixes from strings"

date = 2021-06-11

[taxonomies]
tags = ["golang"]
+++

Found cool function in the [strings](https://golang.org/pkg/strings/) package today, [`TrimFunc`](https://golang.org/pkg/strings/#TrimFunc)! 


This allows you to remove any character (`rune`) you want from the suffix or prefix of a string by passing a function and returning true if something should be removed. 

Example

```
strings.TrimFunc("¡¡¡Hello, Gophers!!!", func(r rune) bool {
		return !unicode.IsLetter(r) && !unicode.IsNumber(r)
})
```
