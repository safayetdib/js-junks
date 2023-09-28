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

## Wait for DOM elements

```
function waitForElem(waitFor, callback, minElements = 1, isVariable = false, timer = 10000, frequency = 25) {
  let elements = isVariable ? window[waitFor] : document.querySelectorAll(waitFor);
  if (timer <= 0) return;
  (!isVariable && elements.length >= minElements) || (isVariable && typeof window[waitFor] !== "undefined") ? callback(elements) : setTimeout(waitForElem.bind(null, waitFor, callback, minElements, isVariable, timer - frequency), frequency);
}
```
