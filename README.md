# ChatGPT Scroll Fix

## Overview

This JavaScript bookmarklet attempts to restore conversation scrolling in ChatGPT when browser focus has moved away from the scroll container. It manually returns focus to that container.

## How it works

The bookmarklet selects the first element matching `.thread-scroll-container`, the CSS class used to identify the conversation scroll container. If the element exists, it sets `tabindex="-1"` so the element can receive programmatic focus without being added to the normal Tab navigation order. It then calls `focus({preventScroll:true})` to focus the container without scrolling it into view.

If no matching element exists, it does nothing.

## Installation

1. In Chrome, create a bookmark and name it **ChatGPT Scroll Fix**.
2. Edit the bookmark and replace its entire **URL** field with the complete code below, including the `javascript:` prefix.
3. Save the bookmark. Keep it accessible in the bookmarks bar.

```javascript
javascript:(()=>{const s=document.querySelector('.thread-scroll-container');if(s){s.setAttribute('tabindex','-1');s.focus({preventScroll:true});}})();
```

The same code is stored in [`src/bookmarklet.js`](src/bookmarklet.js). No dependencies or build tools are required.

## Usage

When scrolling stops working in a ChatGPT conversation, click the **ChatGPT Scroll Fix** bookmark while that conversation tab is active, then try scrolling again. Run it manually again if focus moves away and the problem returns.

## Limitations

- It depends on ChatGPT's HTML structure and the `.thread-scroll-container` selector. It may stop working if that selector changes.
- It requires manual activation; it does not monitor focus or run automatically.
- It targets the focus-related scrolling problem described above. Other causes of scrolling failures have not been verified.
