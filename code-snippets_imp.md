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

## Get data from DOM

```
async function getDOM(url, callback) {
  const response = await fetch(url);
  const html = await response.text();
  const parser = new DOMParser();
  const doc = parser.parseFromString(html, "text/html");
  return callback ? callback(doc) : doc;
}

```

##

```
function networkCallObserver(callback) {
  const observer = new PerformanceObserver((list) => {
    list.getEntries().forEach((entry) => {
      callback(entry.name);
    });
  });
  observer.observe({entryTypes: ["resource"]});
}
```

## Scroll down to specific section

```
element.addEventListener("click", () => {
        const offsetY = -120;
        const targetElement = getElement("#complete-the-look-section");
        const positionY = targetElement.getBoundingClientRect().top + window.pageYOffset + offsetY;

        window.scrollTo({top: positionY, behavior: "smooth"});
      });
```

## find matching words from a list of words in an array

```
function hasMatchingWord(products, search) {
  const seenWords = new Set(); // To keep track of already seen words
  const matches = [];
  for (let i = search.length - 1; i >= 0; i--) {
    const searchWord = search[i].toLowerCase();
    for (const product of products) {
      const productWord = product.split(" ").map((word) => word.toLowerCase());
      if (productWord.includes(searchWord) && !seenWords.has(searchWord)) {
        const capitalizedWord = searchWord.charAt(0).toUpperCase() + searchWord.slice(1);
        matches.push(capitalizedWord);
        seenWords.add(searchWord);
      }
    }
    if (matches.length >= 5) break;
  }
  return matches;
}
```

## Split url testing

target page URL through regex in convert : hotelcollection\.com\/products\/(scent-diffuser|penthouse-scent-diffuser|tower-scent-diffuser|villa-scent-diffuser|presidential-scent-diffuser|double-presidential-scent-diffuser)

Set a cookie so that the test is not bucketed every time

```
console.log("test-29-bucketed");
if (!document.cookie.includes("newTheme=bucketed")){
   document.cookie = "newTheme=bucketed";
   window.location.href = `${window.location.href}?_ab=0&_fd=0&_sc=1&preview_theme_id=133396168870`;
}
```
