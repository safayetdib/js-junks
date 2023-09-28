# Reusable functions

Get element / all elements:

- container -> parent element
- selector -> class / id

if only one argument is passed then container will be the selector

```
function getElement(container, selector) {
  return selector ? container.querySelector(selector) : document.querySelector(container);
}
```

```
function getAllElements(container, selector) {
  return selector ? container.querySelectorAll(selector) : document.querySelectorAll(container);
}
```

Insert a new element:

- target element -> container element -> to which the new element will be inserted
- position -> in which position the new element will be
- element -> new element
- exists -> to check if the element or other dependent element exists or not -> if exissts then the element will not be inserted

```
function insertElement(target, position, element, exists) {
  if (!exists) {
    typeof element === "string" ? target.insertAdjacentHTML(position, element) : target.insertAdjacentElement(position, element);
  }
}
```

## Wait for DOM elements

```
function waitForElem(waitFor, callback, minElements = 1, isVariable = false, timer = 10000, frequency = 25) {
  let elements = isVariable ? window[waitFor] : document.querySelectorAll(waitFor);
  if (timer <= 0) return;
  (!isVariable && elements.length >= minElements) || (isVariable && typeof window[waitFor] !== "undefined") ? callback(elements) : setTimeout(waitForElem.bind(null, waitFor, callback, minElements, isVariable, timer - frequency), frequency);
}
```

## Mutation Observer

```
function mainfunction() {
	console.log('New Page : ', location.href);
}
var currentUrl = '';

var observer = new MutationObserver(() => {
	if (currentUrl !== location.pathname) {
		mainfunction();
		currentUrl = location.pathname;
	}
});

observer.observe(document.body, {
	attributes: false,
	childList: true,
	subtree: true,
});

```

## SPA site - history tracking - reload

```
mainFuncBIS005();

(function(history) {
    var pushState = history.pushState;
    history.pushState = function(state) {
        pushState.apply(history, arguments);
        if (typeof history.onpushstate == "function") {
            history.onpushstate({
                state: state,
            });
        }
        mainFuncBIS005();
    };
})(window.history);

window.addEventListener("popstate", (event) => {
    mainFuncBIS005();
});
```
