---
name: Links with identical accessible names have same purpose

description: |
  This rule checks that identical accessible names are only used for links that have the same purpose

success_criterion: 
- 2.4.9 # Link Purpose (Link Only)

test_aspects:
- DOM Tree
- CSS Styling

authors:
- Anne Thyme Nørregaard
---

## Test Procedure

### Applicability

The rule applies to any two or more HTML or SVG elements that have the [semantic role](#semantic-role) of link, are [exposed to assistive technologies](#exposed-to-assistive-technologies) and that have the same [accessible name](#accessible-name).

**Note:** Leading and trailing whitespace and difference in case sensitivity should be ignored when deciding whether the [accessible names](#accessible-name) are the same.

### Expectation

For each set of target elements, activating the links resolves, after any redirects, to resources that fulfil the same purpose in relation to the purpose indicated by the [accessible names](#accessible-name) of the link.

**Note:** Web pages and documents (e.g. PDFs, office formats etc.) may fulfil the same purpose in relation to the link, even if the resources:
* are located on different URLs, including different domains
* present different navigation options, e.g. through bread crumbs or local sub menus
* contain different amounts of information and/or differently worded information
* are using different layouts.

**Note:** If the same content is presented in different formats, the format itself is often part of the link purpose, e.g. an article as both HTML and PDF.

**Note:** If the [normalized](#url-normalization) value of the ´href´ is identical, the resources are identical, thus fulfilling the same purpose. [Relative URLs](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#relative-urls) first need to be resolved to full URLs before doing the comparison.

## Assumptions

* This rule assumes that the purpose of the links for links with identical link texts would not be ambiguous to users in general, which is the exception mentioned in the success criterion 2.4.9 Link Purpose (Link Only).

## Accessibility support

There are no major accessibility support issues known for this rule.

## Background

- [Understanding SC 2.4.9](https://www.w3.org/TR/UNDERSTANDING-WCAG20/navigation-mechanisms-link.html)
- [URL normalization](#url-normalization)

## Test Cases

### Passed

#### Passed example 1

Identical link text leads to identical URLs:

```html
<a href="/test-assets/link-purpose/index.html">Link text</a>
<a href="/test-assets/link-purpose/index.html">Link text</a>
```

#### Passed example 2

Links resolves to same page due to case-insensitivity on server:

```html
<a href="/Test-Assets/Link-Purpose/index.html">Link text</a>
<a href="/test-assets/link-purpose/index.html>Link text</a>
```

#### Passed example 3

Links resolves to same page after redirect:

```html
<a href="/test-assets/link-purpose/index.html">Link text</a>
<a href="/test-assets/link-purpose/redirect.html>Link text</a>
```

#### Passed example 4

Identical pages are located on different URLs:

```html
<a href="/test-assets/link-purpose/index.html">Link text</a>
<a href="/test-assets/link-purpose/index-copy.html>Link text</a>
```

#### Passed example 5

Same link text used for links going to pages where the content section is the same, but where the navigation options (bread crumbs and local sub menus) differ due to different placement in navigation hierarchy:

```html
<a href="/test-assets/link-purpose/about/contact.html">Link text</a>
<a href="/test-assets/link-purpose/careers/contact.html>Link text</a>
```

#### Passed example 6

URLs differ due to trailing slashes:

```html
<a href="/test-assets/link-purpose/link-purpose">Link text</a> 
<a href="/test-assets/link-purpose/link-purpose/">Link text</a>
```

#### Passed example 7

Pages contain different amounts of information and/or differently worded information, but fulfils same purpose in relation to the link:

```html
<a href="/test-assets/link-purpose/page1.html">Link text</a>
<a href="/test-assets/link-purpose/page2.html">Link text</a>
```

#### Passed example 8

Has the same content but are using different layouts:

```html
<a href="/test-assets/link-purpose/page1.html">Link text</a>
<a href="/test-assets/link-purpose/page3.html">Link text</a>
```

### Failed

#### Failed example 1

Same link text used for links going to different resources:

```html
<a href="http://facebook.com">Follow us</a> 
<a href="http://twitter.com">Follow us</a>
```

#### Failed example 2

Same link text used for links going to web pages with same name, but with different information:

```html
<a href="/test-assets/link-purpose/social-sciences/contact.html">Contact us</a> 
<a href="/test-assets/link-purpose/humanities/contact.html">Contact us</a>
```

#### Failed example 3

Case-sensitivity in file name:

```html
<a href="/test-assets/link-purpose/page1.html">Link text</a> 
<a href="/test-assets/link-purpose/Page1.html">Link text</a>
```

### Inapplicable 

#### Inapplicable example 1

´a´ and ´area´ elements without ´href´ attribute:

```html
<a>Link text</a>
<area aria-label="Link text"></area>
```

#### Inapplicable example 2

No identical link texts:

```html
<a href="/test-assets/link-purpose">Link text 1</a>
<a href="/test-assets/link-purpose">Link text 2</a>
```