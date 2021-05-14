# Typoscript optionSplit

**optionSplit** uses `|*|` as a separator of parts. The separator for subparts is `||`. The order of parsing is as follows:

1. the last part is determined
  1. subparts are considered
1. the first part is determind
  1. subparts are considered
1. the middle part is determined and repeated until the elements are gone
  1. subparts are considered

The important thing here is that subparts are always filled first before moving on to the next (main) part.

E.g. with the pages A to E the following Typoscript
```
page = PAGE
page.10 = HMENU
page.10.1 = TMENU
page.10.1.NO.linkWrap = 1||2 |*||*| 3
page.10.1.NO.allWrap = |&nbsp;
```

gives `1A 2B 1C 2D 3E`
