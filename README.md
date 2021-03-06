# Madu

> Note: this is not production ready.

Write `jsx` as if is `html` string.

## What is Madu?

With Madu, you can think of `jsx` as `html` string.

```jsx
const Madu = require('@lihautan/madu');
const html = (
  <html>
    <body>
      <h1>Hello World!</h1>
    </body>
  </html>
);
// html = "<html><body><h1>Hello World!</h1></body></html>"
```

All you need to do is to add `"@lihautan/babel-transform-madu"` into your `.babelrc`;

```json
{
  "plugins": ["@lihautan/babel-transform-madu"]
}
```

The benefit of writing `jsx` is that, you can write `JavaScript` within it.

```jsx
const formula = (
  <div>
    <span className="question">1 + 2 =</span>
    <span className="answer">{1 + 2}</span>
  </div>
);
// formula = "<div>
//              <span class="question">1 + 2 =</span>
//              <span class="answer">3</span>
//            </div>";
const list = (
  <>
    <h3>Flower</h3>
    <ul>
      {['rose', 'tulips', 'lily'].map(flower => (
        <li>{flower}</li>
      ))}
    </ul>
  </>
);
// list = "<h3>Flower</h3>
//         <ul>
//           <li>rose</li>
//           <li>tulips</li>
//           <li>lily</li>
//         </ul>"
```

Besides, with `jsx`, you can compose components, just like you would when writing React flavor applications

```jsx
function App() {
  return (
    <body>
      <Header />
      <Body />
    </body>
  );
}
function Header() {
  return <navbar />;
}
function Body() {
  return <div />;
}
const app = <App />;
// app = "<body>
//   <navbar></<navbar>
//   <div></div>
// </body>";
```

### Async mode

In async mode, `jsx` can be think of `Promise<string>`
This allows you to fetch data in the component function.

```jsx
const { MaduAsync: Madu } = require('@lihautan/madu');

function MovieList({ movies }) {
  return (
    <ul>
      {movies.map(movie => (
        <li>
          {movie.title}
          <span className="director">{movie.director}</span>
        </li>
      ))}
    </ul>
  );
}
async function App({ searchParam }) {
  // fetch list of movies
  const movies = await fetchMovies(searchParam);
  return <MovieList movies={movies} />;
}

const app = require('express')();
app.get('/movies/search', async function(req, res) {
  res.send(await <App searchParam={req.query.search} />);
  // sends out
  // "<ul>
  //   <li>
  //     Avengers<span class="director">Anthony Russo</span>
  //   </li>
  //   <li>
  //     A star is born<span class="director">Bradley Cooper</span>
  //   </li>
  //   ...
  // </ul>"
});
```

## The Damu-Madu Project

The Damu-Madu sister project aims to bring the developer experience of writing JSX (XML in JavaScript) without having to use React.

JSX is independent of React, you don't have to use React just to use JSX in your development process.

The Damu-Madu sister project contains solution for both client render and server render:

- [madu](https://github.com/tanhauhau/madu) - Writing jsx as if html string
- [damu](https://github.com/tanhauhau/damu) - Converts jsx to vanilla javascript