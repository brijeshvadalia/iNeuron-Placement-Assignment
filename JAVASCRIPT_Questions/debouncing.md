# Debouncing

## HTML FILE
```
<!-- Html File  -->
<input type="text" id="search-input" placeholder="Search...">
<div id="search-results"></div>
```

## JAVASCRIPT FILE

```
// Debounce function
function debounce(func, delay) {
  let timeoutId;
  
  return function() {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(func, delay);
  }
}

// Function to simulate API call and display search results
function search() {
  const searchInput = document.getElementById('search-input');
  const searchResults = document.getElementById('search-results');
  const query = searchInput.value;

  // Simulating API call with search results
  const results = simulateAPICall(query);

  // Display search results
  searchResults.innerHTML = '';
  results.forEach(result => {
    const resultElement = document.createElement('p');
    resultElement.textContent = result;
    searchResults.appendChild(resultElement);
  });
}

// Simulated API call
function simulateAPICall(query) {
  // Simulating delay
  const delay = 500;

  // Simulating search results
  const results = [
    'Result 1',
    'Result 2',
    'Result 3',
    // ...
  ];

  // Simulating filtering based on the query
  const filteredResults = results.filter(result =>
    result.toLowerCase().includes(query.toLowerCase())
  );

  // Simulating delay in API response
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(filteredResults);
    }, delay);
  });
}

// Apply debouncing to the search function
const debouncedSearch = debounce(search, 300);

// Add event listener to the search input
const searchInput = document.getElementById('search-input');
searchInput.addEventListener('input', debouncedSearch);


```

> In this example, we have a search input field (< input>) and a search results container (< div>). We want to implement debouncing so that the search function is not triggered on every keystroke, but only after a brief pause when the user stops typing.

> The debounce function is a utility function that takes a function (func) and a delay in milliseconds (delay). It returns a new function that wraps the original function and uses a timer to delay its execution. If the wrapped function is called within the delay period, the timer is reset, effectively debouncing the function.

> The search function is the callback function that is debounced. It simulates an API call and displays the search results in the results container. In this example, we're using a simulated API call using the simulateAPICall function, which returns a promise with search results after a delay.

> We apply the debouncing by creating a debounced version of the search function using debounce(search, 300). This debounced version is assigned to the debouncedSearch variable.We then add an event listener to the search input field (searchInput) and attach the debouncedSearch function as the callback. The debounced function is triggered only after a 300ms pause between keystrokes, preventing excessive API calls and improving performance.

> By using debouncing, we optimize the search functionality by ensuring that the API call is made only after the user has finished typing or paused for a short period, reducing unnecessary API requests and improving the user experience.