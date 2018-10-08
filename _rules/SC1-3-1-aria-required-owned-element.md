---
name: ARIA required owned elements

description: |
	This rule checks that each role has at least one of its required owned elements.

success_criterion:
- 1.3.1 # Info and Relationships (A)

test_aspects:
- DOM Tree
- CSS Styling

authors:
- Audrey Maniez
- Jey Nandakumar
---

## Test procedure

### Applicability

This rule applies to any HTML or SVG element that is [exposed to assistive technologies](#exposed-to-assistive-technologies) and has an explicit [semantic role](#semantic-role) that has [WAI-ARIA required owned elements](https://www.w3.org/TR/wai-aria/#mustContain).

### Expectation

For each test target, at least one instance of one [WAI-ARIA required owned element](https://www.w3.org/TR/wai-aria-1.1/#mustContain) is present.

**Note:**
- When a widget is missing required owned elements due to script execution or loading, authors [MUST]((w3.org/TR/wai-aria-1.1/#mustContain)) mark a containing element with `aria-busy` equal to `true`.

## Assumptions

*There are currently no assumptions*

## Accessibility Support

This rule relies on assistive technologies to recognize owned elements, as defined by [WAI-ARIA 1.1](https://www.w3.org/TR/wai-aria). This includes when they are nested descendants that are not immediate children. However, some assistive technologies do not recognize owned elements that are not immediate children, unless workarounds are used.

## Background

- [Required Owned Element](https://www.w3.org/TR/wai-aria-1.1/#mustContain)
- [Owned Element](https://www.w3.org/TR/wai-aria-1.1/#dfn-owned-element)
- [HTML in ARIA](https://www.w3.org/TR/html-aria/)
- [Implicit WAI-ARIA Semantics](https://www.w3.org/TR/wai-aria-1.1/#implicit_semantics)

## Test Cases

### Passed

#### Passed example 1

Element `ul` with role `list` has at least one child node `span` with the required owned element `listitem` as an explicit semantic role.

```html
<ul role='list'>
	<span role='listitem'>
	</span>
	<span>
	</span>
</ul>
```

#### Passed example 2

Element `div` with role `tablist` has child node `span` with the required owned element `tab` as an explicit semantic role.

```html
<div role='tablist'>
	<span role='tab'>
	</span>
</div>
```

#### Passed example 3

Element with role `list` has `li` element which has an implicit semantic role of ´listitem´, which is a required owned element.

```html
<ul role='list'>
	<li></li> <!-- implicit role -->
</ul>
```

#### Passed example 4

Multiple roles that each have an instance of their required owned elements present as child nodes.

```html
<table role='grid'>
	<tr role='row'>
		<span role='cell'>
		</span>
	</tr>
</table>
```

#### Passed example 5

Multiple types of required owned elements are present.

```html
<ul role='menu'>
	<li></li> <!-- implicit role -->
	<li role='menuitem'></li>
	<li role='menuitemradio'></li>
</ul>
```

#### Passed example 6

Required owned element does not have to be an immediate child of the role, but could be any descendant. (See accessibility support notes for details).

```html
<div role="table">
	<div role="presentation">
		<div role="presentation">
			<div role="presentation">With presentation role</div>
		</div>
	</div>
	<div role="presentation">
		<div role="presentation">
			<div role="row">
				<div role="cell">my cell</div>
				<div role="cell">and another cell</div>
			</div>
			<div role="row">
				<div role="cell">my cell</div>
				<div role="cell">and another cell</div>
			</div>
		</div>
	</div>
</div>
```

#### Passed example 7

Nested required owned element(s) using the `containing` notation for respective role(s).

```html
<div role="grid">
	<div role="rowgroup">
		<div role="row">
			<div role="gridcell">1</div>
			<div role="gridcell">Item 1</div>
			<div role="gridcell">2 Nos.</div>
		</div>
	</div>
	<div role="rowgroup">
		<div role="row">
			<div role="gridcell">1</div>
			<div role="gridcell">Item 1</div>
			<div role="gridcell">2 Nos.</div>
		</div>
	</div>
</div>
```

#### Passed example 8

Element `div` with `list` role  contains a required owned element with implicit role of `listitem`.

```html
<div role='list'>
   <li>
   </li>
</div>
```

### Failed

#### Failed example 1

Missing required owned element ´listitem´.

```html
<ul role='list'>
	<span>
	</span>
</ul>
```

#### Failed example 2

Element with role `tablist` is missing required owned element `tab`.

```html
<ol role='tablist'>
	<li role='listitem'>
	</li>
</ol>
```

#### Failed example 3

Element with role grid is missing required owned element rowgroup, even though the containing required owned element is present.

```html
<div role="grid">
	<div>
		<div role="row">
			<span>Item 1</span>
		</div>
	<div>
	<div role="rowgroup">
		<div role="row">
			<span>Item 2</span>
		</div>
	</div>
</div>
```

### Inapplicable

#### Inapplicable example 1

Element is not exposed to assistive technologies.

```html
<ul role='list' aria-hidden='true'>
	<li></li>
</ul>
```

#### Inapplicable example 2

Element has empty role.

```html
<ul role=''>
	<li></li>
</ul>
```

#### Inapplicable example 3

Element has no role attribute.

```html
<ul>
	<li></li>
</ul>
```