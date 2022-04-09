## Introducing Next.js, React.js's Newest Sibling.


In October 2016, Vercel and the open-source community released an "icing on the cake" framework.

The main goal of its first release was to improve one of the most popular JavaScript libraries on the market, React.

While React is very popular, there were a lot of problems that developers had to deal with when they started using it. These problems included performance issues, routing, server-side rendering, and SEO.

Now, let's examine all of Next.js's implications for these difficulties.


### 1. Server-Side Rendering

React employs the time-honored technique of client-side rendering.

When developing a React application, the initial load time is lengthy owing to the loading and rendering of all DOM elements.

However, not all components are loaded when changes are made. Because just the updated components are loaded, future loads following the initial ones are quick.

Next.js adds server-side rendering, which renders pages in HTML format without waiting for all the JavaScript code to load (like React does). This means that you can view pages in your browser while the JavaScript code is being downloaded behind the scenes.

Next.js was designed to be as intelligent as possible, loading only the Javascript and CSS required for any given page.

With React, you'd have to wait for all of these to complete before viewing the pages.

When using `npm run dev` to start your next app, you'll notice that the initial load time is significantly faster than when using `npm start` in React.

Next.js applications are extremely quick due to the use of static sites and server-side rendering.




### 2. Search Engine Optimization (SEO) 

Essentially, HTML is displayed on the server when Next is used.
It is rendered on the client-side, i.e. in the browser, with React.
SEO makes use of an algorithm tool that scans the server's HTML content.

Additionally, Next.js includes a <Head> component that allows you to incorporate all meta tags to aid in crawling web page titles and descriptions.

```
import Head from 'next/head'

function Home() {
  return (
    <div>
      <Head>
        <title>Michael Asiedu/title>
        <meta name="viewport" content="initial-scale=1.0, width=device-width" />
      </Head>
      <p>Hello world!</p>
    </div>
  )
}

export default Home
``` 

Additionally, SEO has improved significantly in recent years, and as a result, it now favors quicker websites over slower ones.


### 3. Easy Routing

Routing in React takes some getting used to, as you must install an npm package, [React Router](https://blog.michaelasiedu.com/a-complete-beginners-guide-to-understanding-react-router), import it, and define routes and their paths.

Implementing dynamic and chained routes might be challenging.

Next.js includes a built-in file-system-based router that is based on the concept of pages.

Following Next's installation, a default folder called "pages" is created.

When a file is added to the "pages" directory, it becomes available as a route automatically.

In addition, like a single-page app, the Next.js router lets you move between pages on the client-side.

A component named `Link` assists in the conceptualization of this idea.

```
import Link from 'next/link'

function Navbar() {
  return (
    <ul>
      <li>
        <Link href="/">
          <a>Home</a>
        </Link>
      </li>
      <li>
        <Link href="/about">
          <a>About Us</a>
        </Link>
      </li>
      <li>
        <Link href="/blog/hello-world">
          <a>Contact</a>
        </Link>
      </li>
    </ul>
  )
}

export default Navbar
``` 

### Conclusion

Adoption of Next. js became prevalent quickly because it solved a problem that many web developers used to have with web applications rendered on the client-side (in the browser).


- Server-side rendering

- Improved Search Engine Optimization

- Improved web page performance

- Better development process










