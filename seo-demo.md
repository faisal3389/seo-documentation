// Author: Faisal Ali
// Date: 5th Oct 2017

# What is SEO?

* The efforts revolving around trying to get a site/page to show up(rank) or increase rank within a Search Engine Results Page (SERP)

# Meta Tags:

* Meta Tags are an effective way for webmasters to provide information about their site to the search engine. 
A meta tag is not fully visible when the reader is surfing through the website. It appears on the SERP. They are a means of explaining everything in a site, in a summarized fashion to the search engines. They appear in the head section of the HTML code.

---- image => how we see website.png and how google-sees-website.png ---

* Meta tags played a crucial role in imporving the search results of a site before people started abusing them to get on top of SERPs. Today, high quality, informative and relevant content, plays a far superior role in site's SEO rankings than meta tags. But, It is still an important part of the website.

---- image => seo-ranking-factors.png ---

Elements of meta tags which are relevant today:-
1. Title tag <title></title>
2. Description <meta name="description" content="this is content">
3. url <meta name="description" content="this is content">
4. image <meta name="description" content="this is content">
5. keywords <meta name="description" content="this is content">
6. og:tags <meta name="description" content="this is content">


# social-media meta-tags:
1. used to show title and image, while sharing on social media.


# What is problem with angular app(or SPA) regarding Title & Meta tags?

* Since our app is Single Page Application and only the body part of the application gets updated every time as we move from one url to another so creating a proper title tag and meta tag description is really important.

* we need to have a solution that can dynamically generate a proper title tag as well as Meta tag description 

* By default, front end frameworks have virtual DOM so when a hard request is made to an app built with such frameworks (like Angular), the expected behavior is weird. The request is served with a response of just the HTML content found at the entry point of the app while the main app content is lost.

* This is not a problem to your users because your app virtually has content, styles, and state. Where the problem kicks in is with web crawlers that index your site for SEO sake. They get served with the incomplete HTML content which is very useless to them. This behavior even gets more painful when you expect people to share your app's link and you see an image like the one below when they do:

---- image => no-tags.png ---

# Solution:

* In 2009, Google made a proposal to make AJAX pages crawlable. Back then, their systems were not able to render and understand pages that use JavaScript to present content to users. Because "crawlers … [were] not able to see any content … created dynamically," they proposed a "set of practices" that webmasters can follow in order to ensure that their AJAX-based applications are indexed by search engines.

* Times have changed. Today, as long as we're not blocking Googlebot from crawling our JavaScript or CSS files, They are generally able to render and understand our web pages like modern browsers. To reflect this improvement, they recently updated their technical Webmaster Guidelines to recommend against disallowing Googlebot from crawling your site's CSS or JS files.

### Prerender

* Search engines and social networks are always trying to crawl your pages, but they only see the javascript tags...

It renders your javascript in a browser, save the static HTML, and you return that to the crawlers!

### Angular universal (Server-side Rendering for Angular 2 apps)

* The Universal idea is to build an app that does not just render to server but also runs on the server. Running in the sense that our state, content and styles are intact on the client and the server as well. In Angular 2, this is achieved with the help of Angular Universal which loads our app on the server first, and then drops it to the browser once ready.


* First time users of your application will instantly see a server rendered view which greatly improves perceived performance and the overall user experience. According to research at Google, the difference of just 200 milliseconds in page load performance has an impact on user behavior.

* Although Googlebot crawls and renders most dynamic sites, many search engines expect plain HTML. Server-side pre-rendering is a reliable, flexible and efficient way to ensure that all search engines can access your content.

##### At a high level, there are two major pieces to the Angular Universal:

* Rendering on the server which means generating all the HTML for a page at a given route
* Transitioning from the server view to the client view in the browser client

* There are two different approaches you can use for server rendering. The first option is to pre-render your application which means that you would use one of the Universal build tools (i.e. gulp, grunt, broccoli, webpack, etc.) to generate static HTML for all your routes at build time. Then you could deploy that static HTML to a CDN. The advantage of this approach is that it is highly scalable and performant. The disadvantage is that it is not quite as flexible as the second approach.

* The second approach is to dynamically re-render your application on a web server for each request. There are still several caching options available with this approach to improve scalability and performance, but you would be running your application code within the context of Angular Universal for each request.



# Server Rendering Flows
### Flow for server pre-rendering:

1. Generate static HTML with build tool
2. Deploy generated HTML to a CDN
3. Server view served up by CDN
4. Server view to client view transition (see below)

### Flow for server re-rendering:

1. HTTP GET request sent to the server
2. Server generates a page that contains rendered HTML and inline JavaScript for Preboot 
3. Server view to client view transition (see below)

### Flow for server view to client view transition:

1. Browser receives initial payload from server
2. User sees server view
3. Preboot creates hidden div that will be used for client bootstrap and starts recording events
4. Browser makes async requests for additional assets (i.e. images, JS, CSS, etc.)
5. Once external resources loaded, Angular client bootstrapping begins
6. Client view rendered to the hidden div created by Preboot
7. Bootstrap complete, so Angular client calls preboot.done()
8. Preboot events replayed in order to adjust the application state to reflect changes made by the user before Angular bootstrapped (i.e. typing in textbox, clicking button, etc.)
9. Preboot switches the hidden client view div for the visible server view div
10. Finally, Preboot performs some cleanup on the visible client view including setting focus


The user's activities are recorded (with Preboot.js) at this stage and after couple of seconds when Angular is ready with the real thing, the user is automatically switched and those events replayed. The user won't even catch a glimpse of what is happening under the hood.


* SEO Friendly

Angular Universal helps you to serve your app content to the server just as you did on the browser. When a web crawlers visit, they will be able to index you website's full content that can be used on search engines. This thereby solves one of the most popular front end challenges when working with JavaScript frameworks that create virtual DOM.

* Social Media Friendly

With Angular Universal serving your sever with browser content, social media platforms that display brief information about your website when a link is added can get access to the needed details.

* Pre-rendering

This is the most bind-blowing feature offered by Angular Universal. Angular Universal renders both your content and state as well as registering events on the server. The implication is that when your app boots, the server would serve the server-rendered content and a user can make use of the app at that stage.


* Angular Universal was originally built to work with a node.js back-end. There are adapters for most popular node.js server-side frameworks such as Express or Hapi.js. In addition to node.js, however, Angular Universal has ASP.NET Core support. In the near future we hope to add support for Java, PHP and Python.
