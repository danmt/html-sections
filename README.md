# Make it Accessible: Better layouts with HTML

In this article I'm going to teach you how to use the HTML tags `<div>`, `<section>` and `<article>`, and why they can improve your web applications accessibility.

Here you can access all the [resources used in the article](https://github.com/danmt/html-sections).

## The Problem

Web applications are built with HTML, even though it isn't a programming language, it has some complexity to deal with. One of the first issues you may encounter is knowing which element to use, what makes this issue even harder is the huge amount of elements available.

When it comes to your page's layout some of the options are; `<div>`, `<section>` and `<article>`. Today you're going to learn when you should use each of them.

## The Solution

First of all is to conceptualize each of the elements I just mentioned. You can learn more about this in the [w3c wai aria practices guide](https://www.w3.org/TR/wai-aria-practices) but let's bring those concepts here:

> The `<div>` element is often used as a container for other HTML elements to style them with CSS or to perform certain tasks with JavaScript.
> w3schools.com

Is common to be tempted to use `<div>` with some styles instead of learning about the available elements in HTML5. I have to tell you, if you do that, you're hurting your users. The truth is each element has a specific purpose, you should be using the right element, `<div>` is useful when you want to group some elements and give them some styling, that doesn't mean you should make everything with `<div>`.

> The `<section>` tag defines sections in a document, such as chapters, headers, footers, or any other sections of the document.
> w3school.com

This is a very important tag as you start your accessibility journey. It gives context to your users, specially those with Screen Readers. If you're thinking what do you mean by context? Well, if you wrap a group of elements with a section and give it an accessible name, once users focus one of the elements it reads the parent container too.

> The `<article>` tag specifies independent, self-contained content.
> w3school.com

Almost every application has some kind of catalogue showing several items having the same styles, and if you think it through, these items could be placed anywhere without any context. Articles are cool for those cases, even though these aren't landmarks is common for Screen Readers to have a mechanism to allow users to navigate through articles easily.

## The Implementation

Next we're going to do a small sample using each of the mentioned elements, let's start with the `<div>`.

### Using divs right

Now that you are fully aware of the purpose of a `<div>` is time to use it. For this one I decided to take the easy road and make a very simple example, let's say you have multiple "things" you want to group and apply some additional styling. That can be easily done like this:

```html
<html>
  <head>
    <style>
      .square {
        display: inline-block;
        width: 150px;
        height: 150px;
        border: 1px solid black;
        margin: 10px;
        background-color: white;
      }

      .group {
        display: inline-block;
        margin: 0;
        background-color: #bbb;
      }
    </style>
  </head>

  <body>
    <header>
      <h1>Using divs right</h1>
    </header>

    <main>
      <div class="group">
        <div class="square"></div>
        <div class="square"></div>
      </div>
      <div class="square"></div>
      <div class="square"></div>
      <div class="square"></div>
    </main>
  </body>
</html>
```

All you got to do for testing it yourself is create a file with the `.html` extension containing what I just gave you and open it with your preferred browser. You'll noticed that the first two have a light gray background. Once again, very simple and easy to follow. Let's jump to the next example.

### Sections are the way to go

For this one I was looking for a more exciting example. Let's say you are building an application for a movie theater that allows customers to order tickets online. If you buy a ticket, you want to have a page where you can see all the details about the movie and your ticket.

Let's start by thinking it through. We want to see all the information about the movie, title, synopsis, a banner image and a genre. When it comes to the ticket, I want to see its worth, my sit number and the time left for the show to start.

The HTML for something like this would look like this:

```html
<html>
  <head>
    <style>
      body {
        margin: 0;
        padding: 0;
      }

      main {
        display: flex;
        align-items: flex-start;
        justify-content: center;
        flex-wrap: wrap;
        background-color: #333;
        min-height: calc(100vh - 80px);
        margin-top: 80px;
      }

      header {
        position: absolute;
        height: 80px;
        color: white;
        background-color: #444;
        padding: 2px 0;
        text-align: center;
        box-shadow: 0px 6px 3px 3px rgba(0, 0, 0, 0.1);
        width: 100%;
        top: 0px;
      }

      .card {
        box-shadow: 0px 6px 3px 3px rgba(0, 0, 0, 0.1);
        display: inline-block;
        margin: 20px;
      }

      .movie-details {
        width: 400px;
      }

      .movie-details figure {
        width: 100%;
        margin: 0;
      }

      .movie-details figure img {
        width: 100%;
        object-fit: cover;
      }

      .container {
        padding: 10px;
        border: 1px solid #333;
        background-color: #444;
        color: white;
      }

      .ticket-summary {
        width: 250px;
      }

      .ticket-summary dt {
        color: #ccc;
        font-size: 1.1rem;
        font-weight: bold;
        margin-top: 8px;
      }
    </style>
  </head>

  <body>
    <header>
      <h1>Your Ticket Details</h1>
    </header>

    <main>
      <section class="card movie-details" aria-label="movie details">
        <figure>
          <img src="./img.jpg" alt="" />
        </figure>

        <div class="container">
          <h2 style="margin: 6px 0;">Parasite</h2>
          <p style="text-align: justify;">
            Greed and class discrimination threaten the newly formed symbiotic
            relationship between the wealthy Park family and the destitute Kim
            clan.
          </p>
          <p><b>Comedy, Drama</b></p>
        </div>
      </section>

      <section
        class="card ticket-summary"
        aria-labelledby="ticket-summary-title"
        aria-describedby="ticket-summary-description"
      >
        <div class="container">
          <h2
            id="ticket-summary-title"
            style="margin: 6px 0; text-align: center;"
          >
            Ticket Summary
          </h2>
          <p id="ticket-summary-description" style="text-align: justify;">
            Remember to exchange your ticket identifier for the actual ticket as
            soon as you get to the movie theater.
          </p>
          <dl>
            <dt>Identifier</dt>
            <dd>123</dd>
            <dt>Seat</dt>
            <dd>B-12</dd>
            <dt>Price</dt>
            <dd>$ 2,00 USD</dd>
            <dt>Starts in</dt>
            <dd>2h 30m</dd>
          </dl>
        </div>
      </section>
    </main>
  </body>
</html>
```

For now you can ignore the styles, it's just to make it look less ugly, what I want you to pay attention to is the HTML part. Look how I created two sections; one for the movie details and one for the ticket summary. Another important takeaway is how I used aria-label and aria-labelledby, both have the same results but in the movie details I wanted to read "Movie Details" instead of the movie title, in the case of the Ticket Summary it's different because we want to read the same title.

By structuring your HTML document this way, using sections with the proper accessible names, you're not only giving context to the user but you're creating a hierachical view of the landmarks of your application. This makes it easier for Screen Readers to understand your page and as a consequence you get better usability for your disabled users.

### Articles are useful too

I know that example may have set the bar a little high, for this example I'm doing something simpler. Let's say that this movie theater we are "working for" wants to show all the available movies to possible customers. This is where articles shine the most, because let's face it, no matter how many movies they are, all of them will have the same styles.

Let's roll up our sleeves then, create a new html file with this content:

```html
<html>
  <head>
    <style>
      body {
        margin: 0;
        padding: 0;
      }

      main {
        display: flex;
        align-items: flex-start;
        justify-content: center;
        flex-wrap: wrap;
        background-color: #333;
        min-height: calc(100vh - 80px);
        margin-top: 80px;
      }

      header {
        position: absolute;
        height: 80px;
        color: white;
        background-color: #444;
        padding: 2px 0;
        text-align: center;
        box-shadow: 0px 6px 3px 3px rgba(0, 0, 0, 0.1);
        top: 0px;
        width: 100%;
      }

      .card {
        box-shadow: 0px 6px 3px 3px rgba(0, 0, 0, 0.1);
        display: inline-block;
        margin: 20px;
      }

      .movies {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
        width: 800px;
      }

      .feed {
        display: flex;
        margin-top: 10px;
      }

      .movie {
        width: 200px;
        height: 420px;
      }

      .movie figure {
        width: 100%;
        height: 300px;
        margin: 0;
        overflow: hidden;
      }

      .movie figure img {
        width: 100%;
        object-fit: cover;
        height: 100%;
      }

      .container {
        padding: 10px;
        height: 100px;
        border: 1px solid #333;
        background-color: #444;
        color: white;
      }

      .movie h2 {
        margin: 8px 0;
        font-size: 1.2rem;
        font-weight: bold;
      }

      .movie p {
        margin: 8px 0;
        font-style: italic;
      }
    </style>
  </head>

  <body>
    <header>
      <h1>Movies List</h1>
    </header>

    <main>
      <section class="movies" aria-label="available movies">
        <div role="feed" class="feed">
          <article
            class="movie card"
            aria-labelledby="movie-name-1"
            aria-describedby="movie-genre-1"
            tabindex="0"
            aria-posinset="1"
            aria-setsize="3"
          >
            <figure>
              <img src="./movie-1.jpg" alt="" />
            </figure>
            <div class="container">
              <h2 id="movie-name-1">The Shawshank Redemption</h2>
              <p id="movie-genre-1">Drama</p>
            </div>
          </article>
          <article
            class="movie card"
            aria-labelledby="movie-name-2"
            aria-describedby="movie-genre-2"
            tabindex="0"
            aria-posinset="2"
            aria-setsize="3"
          >
            <figure>
              <img src="./movie-2.jpg" alt="" />
            </figure>
            <div class="container">
              <h2 id="movie-name-2">The Godfather</h2>
              <p id="movie-genre-2">Crime, Drama</p>
            </div>
          </article>
          <article
            class="movie card"
            aria-labelledby="movie-name-3"
            aria-describedby="movie-genre-3"
            tabindex="0"
            aria-posinset="3"
            aria-setsize="3"
          >
            <figure>
              <img src="./movie-3.jpg" alt="" />
            </figure>
            <div class="container">
              <h2 id="movie-name-3">The Dark Knight</h2>
              <p id="movie-genre-3">Crime, Drama</p>
            </div>
          </article>
        </div>
      </section>
    </main>
  </body>
</html>
```

Remember to focus on the HTML structure, not the styles. The first time I saw this kind of code I was like, wow, what's all that aria stuff doing? Today I'm going to make this easier for you.

> First of all I have to remind you all these ideas come from the [WAI ARIA Authoring Practice Guide](https://www.w3.org/TR/wai-aria-practices-1.1).

One thing to notice before heading to the code is that a list of movies is a feed. Also, don't reinvent the wheel. The WAI ARIA guide has a very detailed description of how a feed should be implemented having accessibility as a first class citizen. You have to start with `<div>` with `role="feed"`, next you have to work on the articles.

Setting up the feed container is very simple, what's not so straightforward is the articles themselves. Each of the aria properties has a specific purpose:

- aria-labelledby: Title of the movie.
- aria-describedby: Additional information about the movie.
- aria-posinset: Position of the movie in the list.
- aria-setsize: Size of the list of movies.

There's also a `tabindex="0"` because once in a feed screen readers provide users with additional navigation mechanisms that require us to make the articles "focusable".

NOTE: All the `<img>` in the samples have an empty alt like this `alt=""`. It's because using an empty alt tells screen readers to ignore the images entirely, in a real life project for images that provide information you always give a proper alt value.

## Conclusion

Every time I write one of these series I come up with the same conclusion, just us HTML! I'm even thinking on changing the name to "It's Already Accessible". Is common to hear developers saying HTML is easy and simple, it might be for some, but you still have to learn. My advice is, whenever you write an application, try to build it following patterns like the ones in WAI-ARIA, make sure you follow their specification and you'll make applications all your users will love.
