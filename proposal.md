# Creating a drgants.js library

This is a document to store the initial research and thoughts to create a js library. It will eventually be combined
into public repo.

**Table of Contents**

* [What is a Library](#what-is-a-library)
* [Library vs. Framework](#library-vs-framework)
* [Architecture](#architecture)
* [Features](#features)
* [Terms](#library-terms)
* [Browser Support](#browser-support)
* [NPM](#npm)
* [Scaffolding](#lib-scafolding)

## What is a Library?

> Generally speaking, JavaScript libraries are collections of pre-written code snippets that can be used and reused to perform common functions surrounding the purpose of library.
> A particular library can be plugged into the rest of your project’s code on an as-needed basis.
---

### What does it achieve?

> faster development and fewer vulnerabilities to have errors.

## Library vs. Framework?

> Libraries are a specialized tool for on-demand use, JavaScript frameworks are a full toolset that helps shape and organize your website or application. In other words,
> libraries are about using what is needed for the task, while frameworks provide you with all the tools you could need even if you don’t particularly need all of them.
> ---
>  Think of it like cooking some pasta. When using a JavaScript library, you simply grab the pot, pan, ingredients to make the pasta, and plates to serve.
> You only require the things you need to make pasta. When thinking about a JavaScript framework, imagine an entire fully loaded kitchen. Another way to think about it can be that JavaScript libraries are like pieces of furniture that add style and function to an already constructed house. At the same time, frameworks are templates you can use to build the house itself.

[reference] (https://generalassemb.ly/blog/what-is-a-javascript-library/)

---

## Architecture

---

### Directory Structure

```bash
.
├── build                   # Compiled files (alternatively `dist`)
├── docs                    # Documentation files (alternatively `doc`)
├── src                     # Source files (alternatively `lib` or `app`)
│   ├── adapters            # Operations which deal with 3rd party (ipfs, node, graph) 
│   │   ├── README.md 
│   ├── core                # Domain logic specific to drgants - business 
│   │   ├── README.md 
│   ├── utilities 
│   │   ├── README.md 
│   ├── examples            # intended use of library
│   │   ├── README.md 
│   ├── dgrants.js          # (alternatively index) is responsible for creating an instance of dgrantsjs
│   ├── defaults.js         # responsible for setting default functionality not related to the domain of drants
│   ├── helpers.js          # generic functions that are NOT related to the domain of dgrants 
├── test                    # Automated tests (alternatively `spec` or `tests`)
├── tools                   # Tools and utilities
├── LICENSE
└── README.md
```

### Data

> **Conversation**: We probably want to use websockets, not HTTP + polling. Using HTTP + polling caused us to go through a ton of
> Alchemy usage during the last dgrants round. Using websockets to have data pushed instead of pulled would
> reduce that, and is what Alchemy recommended to us. ethers has a websocket provider (https://docs.ethers.io/v5/single-page/#/v5/api/providers/other/-%23-WebSocketProvider)
> which should make this pretty simple. However, HTTP might be better for node-based use cases (convenience layers, data analysis, etc) so we should consider that too
>
> **Proposition**: What could potentially be a solution is to allow the end user to setup which transport type they
> would be interested in using. Something to the effect of:

```typescript
  const dataPolling = dgrants.setDataTransport('websocket');
```

### Migration Plan

1. To reuse as much as we can from the current implementation of dgrants.
    1. extract the following files:
   ```bash
         ├── utils                    
             ├── data                     
            │   ├── contributions.ts           
            │   ├── grantRounds.ts            
            │   ├── grants.ts            
            │   ├── ipfs.ts            
            │   ├── utils.ts           
             ├── alerts.ts                     
             ├── chains.ts                     
             ├── constants.ts                     
             ├── ethers.ts                     
             ├── utils.ts                     
   ```
   and apply SOLID principles around them making them easily testable, extensible, composable, and pluggable.
2. Take inventory of the functionality we have vs what we want/need. Extract those out to workable user stories.
3. Document everything

## Features

---

## Browser Support

![Chrome](https://raw.github.com/alrra/browser-logos/master/src/chrome/chrome_48x48.png)
| ![Firefox](https://raw.github.com/alrra/browser-logos/master/src/firefox/firefox_48x48.png)
| ![Safari](https://raw.github.com/alrra/browser-logos/master/src/safari/safari_48x48.png)
| ![Opera](https://raw.github.com/alrra/browser-logos/master/src/opera/opera_48x48.png)
| ![Edge](https://raw.github.com/alrra/browser-logos/master/src/edge/edge_48x48.png)

---

## Library Terms

---

* `Library` a set of pre-written code that can be leveraged as a tool (over and over) for other engineers to use on
  demand.
* `Framework` a collection of libraries that provide a developer with pre-written code that suggests a particular
  context to develop the application in.
* `Protocol` 
 
