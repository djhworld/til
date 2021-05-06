+++
title = "Golang JSON marshaller will replace some characters in strings with unicode runes"
date = 2021-05-05

[taxonomies]
tags = ["golang"]
+++

By [default the Golang JSON encoder](https://golang.org/pkg/encoding/json/) will replace certain characters in strings with their unicode equivalent 

> String values encode as JSON strings coerced to valid UTF-8, replacing invalid bytes with the Unicode replacement rune. So that the JSON will be safe to embed inside HTML \<script\> tags, the string is encoded using HTMLEscape, which replaces "<", ">", "&", U+2028, and U+2029 are escaped to "\u003c","\u003e", "\u0026", "\u2028", and "\u2029". This replacement can be disabled when using an Encoder, by calling `SetEscapeHTML(false)`


You can disable the behaviour if required but it might catch you out if the JSON parser at the other end is crap and doesn't support unicode.
