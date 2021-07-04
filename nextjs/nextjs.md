# What is NextJs

Next is a React frontend development web framework created by Vercel that enables functionality such as server-side rendering nad static site generation.

# Server-Side Rendering

Unlike a traditional React app where the entire application is loaded and rendered on the client , Next.js allows the first page load to be rendered by the server, which is great for SEO & performance.


Traditionally, if you built an application using create React App such as we did in react crash course your entire application is rendered on the client side via javascript . So the request gets redirected through a single HTML file then your javascript gets loaded and  it displays your application in the browser. So this allows you to have really fast and interactive user interface when you compare it to an older php p type website where the server compiles the data and uses template engine and delivers a formatted html page with all your content.
If it's done that way every time you want to navigate to a new route or you want to update your user interface you have to make a new request and reload the page.

Now event though a client- side framework is fast and dynamic there can be some shortcomings and one of the biggest is SEO .

If you use create-react-app and you open up your source code in your browser you're not going to see any of your content you're not going to see the h1s or the h2s the paragraphs anything like that you'll see the main div that is later on replaced with your content via javascript. 

Now this is horrible for SEO because search engine crawlers can't pick up your content and there's multiple ways of handling this,

 but next.js does this right out of the box because the first page load is rendered server-side rather than client-side.

NOT ONLY does this increase PERFORMANCE in some situations but your content is also delivered directly so if you view the page source in the next.js app you're going to see all that content and so are the search engine crawlers. 

So you get the SEO of a server-side-application, and you still get quick dynamic client-side routing and everything else that comes with a react app

- EASY PAGE ROUTING
- API ROUTES
- OUT OF THE BOX Typescript & Sass
- Static site generation ( next export )
- Easy Deployment 