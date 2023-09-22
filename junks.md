## set a maximum number of lines of text with CSS / line-clamp

```
.card__preview-text {
  --max-lines: 3;

  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: var(--max-lines);
  overflow: hidden;
}
```

## creating triangle / arrow-box with border for popup or dialogue box

```
.arrow {
  position: absolute;
  right: 10%;
  top: 95%;
  width: 0;
  height: 0;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
  border-top: 20px solid #000;
}

/* Add a black border around the arrow */
.arrow::before {
  content: "";
  position: absolute;
  border-left: 22px solid transparent;
  border-right: 22px solid transparent;
  border-top: 22px solid #FFF;
  top: -22px;
  right: -22px;
}

```

## Add Styles to an Element

### Inline styles

```
const note = document.querySelector('.note');
note.style.backgroundColor = 'yellow';
note.style.color = 'red';
```

### Using cssText property

Adding individual style is quite verbose. Fortunately, you can add set multiple styles at once by using the cssText property:

```
note.style.cssText += 'color:red;background-color:yellow';
```

In this example, we used the += operator to append new styles to the existing ones. If you use the = operator, the existing style will be removed, like this:

```
note.style.cssText = 'color:red;background-color:yellow';
```

### Using a helper function

The following helper function accepts an element and a style object. It add all styles from the style object to the style property of the element:

```
function css(element, style) {
    for (const property in style)
        element.style[property] = style[property];
}
```

you can use this css() helper function to set the styles for the <div> element as follows:

```
const note = document.querySelector('.note');
css(note, {
    'background-color': 'yellow',
    color: 'red'
});
```

### Global Styles

To add the global styles to an element, you create the style element, fill it with the CSS rules, and append the style element to the DOM tree, like this:

```
const style = document.createElement('style');
style.innerHTML = `
      .note {
        background-color: yellow;
        color:red;
      }
    `;
document.head.appendChild(style);
```

Reference: https://www.javascripttutorial.net/dom/css/add-styles-to-an-element/

## JS DOM Cheat Sheet

https://gist.github.com/thegitfather/9c9f1a927cd57df14a59c268f118ce86

https://webdesign.tutsplus.com/javascript-cheatsheet-event-listeners-and-dom-manipulation--cms-107006a
