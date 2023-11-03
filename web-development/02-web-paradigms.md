# WEB PARADIGMS

There are 3 paradigms for web content delivery:

- **Static (SSG)** - HTML is prebuilt ahead of any request and the web server responds to a request with an existing finished HTML document.
- **Server Side Rendering (SSR)** - A program runs on the server and this generates HTML & CSS code on a per requesst basis
- **Client Side Rendering/ Single Page Applications (SPA/ PWA)** - Minimal HTML is sent and a large complex JavaScript program executes on the client (browser) to create and manage the user's DOM.

## Static Websites

- A static website is rendered on a server at build time, before the site is requested
- Static sites generally change content very infrequently, have a lot of HTML and very little JavaScript (interaactivity)
- The page is then served as a static file in response to a client request, eliminating the time associated with generating the page on demand
- Some commonly used SSGs include Jekyll, Hugo, Gatsby & Next.js - these can take a markdown file and transform it into html
- Pros of SSGs:
  - Easy to serve
  - Browser firendly - since pages are built ahead of time, they are easier for search engine web crawlers to parse in contrast to websites that require client-side rendering. Also, browsers don't understand JavaScript so the fact that statc websites have little JavaScript makes it easier for web crawlers to understand and thus you get good search engine optimisation with static websites
  - Pre-built pages can be served from a content delivery network (CDN) close to the end user since there’s no need to execute server logic or obtain data from a database, making the page quickly accessible
  - Since server-side logic is performed ahead of time, an increase in the number of concurrent users has less impact on the server load compared to SSR performed at request time. This makes it easier to scale to a large number of users, especially if using a CDN
  - Cheaper to host a static website than a server side rendered website
  - You can cache static websites - a static website will change very infrequently, so client can cache the website to save the time cost of requesting it from the server everytime the site is used
- Cons of SSGs:
  - Static websites are limited/ stale
  - A lot of boilerplate if creating a site without any frameworks / tools

## Server Rendered Websites

- Web server creates HTML dynamically
- Content can thus be adjusted based on the context of the request
- Pros of SSR:
  - When content is rendered on a server, the time required for downloading, parsing, and executing JavaScript code is reduced. This will ensure faster load times for web pages.
  - SSR helps in improving SEO (search engine optimization) by pre-rendering the page. Thus, search engine crawlers can easily read the generated HTML file. In client-side rendering, crawlers read an empty HTML file with links to JavaScript that reduce the search ranking of the web page. Fast loading of the server-side rendered web page also helps the site rank higher in search results.
  - Can serve secure pages easily
- Cons of SSR:
  - When the user clicks on a link for some content, the whole website is rendered again on the server. And if the number of concurrent users increases, the load on the servers increases. At scale, this can be troubling and expensive for SSR.
  - SSR applications can be more complex to set up, may require extra computation

## Client Rendered Websites

- A very simple HTML file is given in reponse to a website request.
- HTML is basically just to link JavaScript file, which builds the webpage from the URL
- Pros of client rendered websites/ single page applications:
  - Give an excellent user experience - can change content dynamically very, very quickly without the need to request back to the server because ou have the means to create all the pages you need
- Cons of SPAs:
  - Can be very slow to load if the JavaScript file is very large
  - Site is totally useless without a client that executes JavaScript
  - Not search engine friendly as browsers can't understand JavaScript

## Hydration

- You can use varying amounts of JavaScript with each of the paradigms
- Sometimes you might want to bring interaction to a static or SSR website using JavaScript
- The process of doing this is called **hydration**
