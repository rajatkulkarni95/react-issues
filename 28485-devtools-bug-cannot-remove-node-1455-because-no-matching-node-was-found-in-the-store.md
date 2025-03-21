# [DevTools Bug] Cannot remove node "1455" because no matching node was found in the Store.

> Issue #28485 - Created on 3/4/2024

> Original URL: https://github.com/facebook/react/issues/28485

## Description

### Website or app

Found it on my localhost website

### Repro steps

I added strictmode on my react app on the top level component.

   <StrictMode>
      <BrowserRouter>
        <QueryClientProvider client={queryClient}>
          <header>
            <Link to="/">Adopt Me!</Link>
          </header>
          <Routes>
            <Route path="/details/:id" element={<Details />} />
            <Route path="/" element={<SearchParams />} />
          </Routes>
        </QueryClientProvider>
      </BrowserRouter>
    </StrictMode>

folder structure looks like that.

### How often does this bug happen?

Every time

### DevTools package (automated)

react-devtools-extensions

### DevTools version (automated)

5.0.0-993c4d003

### Error message (automated)

Cannot remove node "1455" because no matching node was found in the Store.

### Error call stack (automated)

```text
at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1130512
    at C.emit (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1099142)
    at chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1100830
    at bridgeListener (chrome-extension://fmkadmapgofadopljbjfkapdkoienihi/build/main.js:1:1501127)
```


### Error component stack (automated)

_No response_

### GitHub query string (automated)

```text
https://api.github.com/search/issues?q=Cannot remove node  because no matching node was found in the Store. in:title is:issue is:open is:public label:"Component: Developer Tools" repo:facebook/react
```

