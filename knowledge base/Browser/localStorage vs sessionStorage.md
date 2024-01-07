
Web storage objects `localStorage` and `sessionStorage` allow to save key/value pairs in the browser.

What’s interesting about them is that the data survives a page refresh (for `sessionStorage`) and even a full browser restart (for `localStorage`).

The storage is bound to the origin (domain/protocol/port triplet). That is, different protocols or subdomains infer different storage objects, they can’t access data from each other.


### localStorage

The main features of `localStorage` are:
- **Shared between all tabs and windows** from the same origin.
- **The data does not expire**. It remains after the browser restart and even OS reboot.


### sessionStorage

The `sessionStorage` object is used much less often than `localStorage`.

Properties and methods are the same, but it’s much more limited:

- The `sessionStorage` exists **only within the current browser tab**.
    - Another tab with the same page will have a different storage.
    - But it is shared between iframes in the same tab (assuming they come from the same origin).
- **The data survives page refresh, but not closing/opening the tab.**