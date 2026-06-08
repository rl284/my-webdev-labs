## Code Review Exercise

### Issue #1: Overwriting Loading Contianer

After a successful fetchCatFacts();, which happens upon the first page `GET`, the line here:

```
    loading.setAttribute('class', 'display-none');
```

overwrites the whole class list, so the element isn't a .loading-container.
This means upon clicking "Load New Cat Facts", the previous facts disappear
and new ones are unable to load because the .loading-container element can't
be retrieved again.

<img src="../images/10-debugging/issue1.png" height=200 alt="screenshot showing an aaccessibility issue on the close button of the modal">

To fix this, we can just set add and remove a speicifc class.

Initial code:

```js
const createLoadingContainer = function () {
  const loadingContainer = document.querySelector('.loading-container');
  ...
  loadingContainer.append(loader);
};

const fetchCatFacts = async function () {
  ...

  createLoadingContainer();

  try {
    ...
    };
  } catch (error) {
    ...
  } finally {
    const loading = document.querySelector('.loading-container');
    loading.setAttribute('class', 'display-none');
  }
};
```

Updated code:

```js
const createLoadingContainer = function () {
  const loadingContainer = document.querySelector(".loading-container");
  ...
  loadingContainer.classList.remove("display-none");
  loadingContainer.append(loader);
};

const fetchCatFacts = async function () {
  ...

  createLoadingContainer();

  try {
    ...
    };
  } catch (error) {
    ...
  } finally {
    const loading = document.querySelector(".loading-container");
    loading.classList.add("display-none");
  }
};

```
