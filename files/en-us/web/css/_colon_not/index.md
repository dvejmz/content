---
title: ':not()'
slug: Web/CSS/:not
tags:
  - ':not()'
  - CSS
  - Layout
  - Negation
  - Pseudo-class
  - Reference
  - Selector
  - Web
browser-compat: css.selectors.not
---
{{CSSRef}}

The **`:not()`** [CSS](/en-US/docs/Web/CSS) [pseudo-class](/en-US/docs/Web/CSS/Pseudo-classes) represents elements that do not match a list of selectors. Since it prevents specific items from being selected, it is known as the _negation pseudo-class_.

```css
/* Selects any element that is NOT a paragraph */
:not(p) {
  color: blue;
}
```

The `:not()` pseudo-class has a number of [quirks, tricks, and unexpected results](#description) that you should be aware of before using it.

## Syntax

The `:not()` pseudo-class requires a comma-separated list of one or more selectors as its argument. The list must not contain another negation selector or a [pseudo-element](/en-US/docs/Web/CSS/Pseudo-elements).

```
:not( <complex-selector-list> )
```

## Description

There are several unusual effects and outcomes when using `:not()` that you should keep in mind when using it:

- The `:not` pseudo-class may not be nested, which means that `:not(:not( ))` is invalid.
- Useless selectors can be written using this pseudo-class. For example, `:not(*)` matches any element which is not an element, which is obviously nonsense, so the accompanying rule will never be applied.
- This pseudo-class can increase the [specificity](/en-US/docs/Web/CSS/Specificity) of a rule. For example, `#foo:not(#bar)` will match the same element as the simpler `#foo`, but has the higher specificity of two `id` selectors.
- The specificity of the `:not()` pseudo-class is replaced by the specificity of the most specific selector in its comma-separated argument of selectors; providing the same specificity as if it had been written [`:not(:is(argument))`](/en-US/docs/Web/CSS/:is).
- `:not(.foo)` will match anything that isn't `.foo`, _including {{HTMLElement("html")}} and {{HTMLElement("body")}}._
- The `:not()` pseudo-class may not work as expected when used with [descendant combinators](/en-US/docs/Web/CSS/Descendant_combinator). For instance, if you do `body :not(table) a`, instead of excluding all the links that are the direct or indirect children of {{HTMLElement("table")}} like you would expect, it excludes only the links that are direct children of {{HTMLElement("table")}}. That means any links you may have inside a {{HTMLElement("tr")}} or {{HTMLElement("td")}} will still be selected.
- You can negate several selectors at the same time. Example: `:not(.foo, .bar)` is equivalent to `:not(.foo):not(.bar)`.

## Examples

### Basic set of :not() examples

#### HTML

```html
<p>I am a paragraph.</p>
<p class="fancy">I am so very fancy!</p>
<div>I am NOT a paragraph.</div>
<h2>
  <span class="foo">foo inside h2</span>
  <span class="bar">bar inside h2</span>
</h2>
```

#### CSS

```css
.fancy {
  text-shadow: 2px 2px 3px gold;
}

/* <p> elements that don't have a class `.fancy` */
p:not(.fancy) {
  color: green;
}

/* Elements that are not <p> elements */
body :not(p) {
  text-decoration: underline;
}

/* Elements that are not <div> and not <span> elements */
body :not(div):not(span) {
  font-weight: bold;
}

/* Elements that are not <div>s or `.fancy` */
body :not(div, .fancy) {
  text-decoration: overline underline;
}

/* Elements inside an <h2> that aren't a <span> with a class of `.foo` */
h2 :not(span.foo) {
  color: red;
}
```

#### Result

{{EmbedLiveSample('Basic_set_of_not_examples', '100%', 320)}}

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Pseudo-classes](/en-US/docs/Web/CSS/Pseudo-classes)
- [Pseudo-classes and pseudo-elements](/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
- Related CSS pseudo-classes:

  - {{cssxref(":has", ":has()")}}
  - {{cssxref(":is", ":is()")}}
  - {{cssxref(":where", ":where()")}}
