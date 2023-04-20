# React App to Search Songs using Apple's iTunes API

In this project, I will be creating a React app that allows users to search for songs using Apple's iTunes API. I will start by setting up our starter files, then style our app using CSS. Next, I will create a search input and learn about the iTunes API. Finally, I will create variables and a search function, display search results in a table, and see the final result.

![Image](https://res.cloudinary.com/ratracegrad/image/upload/v1673900547/Screenshot_2023-01-16_at_3.21.50_PM_tyvecg.png)


## Table of Contents

- [Create Our Starter Files](#create-our-starter-files)
- [Styling our App](#styling-our-app)
- [Creating Our Search Input](#creating-our-search-input)
- [Intro to the Apple iTunes API](#intro-to-the-apple-itunes-api)
- [Create our Variables and Search Function](#create-our-variables-and-search-function)
- [Displaying Search Results in a Table](#displaying-search-results-in-a-table)
- [Final Result](#final-result)


## Create Our Starter Files

I will assume you already have Node installed on your computer. At your terminal enter this command:

```js
npx create-react-app react-song-finder
```

When it is finished change into the directory that it created with the command:

```js
cd react-song-finder
```

If you run `npm start` in the terminal, you will see this:

![Image](https://res.cloudinary.com/ratracegrad/image/upload/v1673823502/Screenshot_2023-01-15_at_5.58.13_PM_mx8ejv.png)


## Styling our App

This project is not to teach you how to style elements in CSS. I want to focus on teaching you the functionality of creating a React App and having it search the iTunes API. 

So I am going to give you the barebones of CSS used in this app.

Open up the `App.css` file and replace everything in it with this code:

```css
#root {
  max-width: 1280px;
  margin: 0 auto;
}

input {
  height: 41px;
  padding: 0;
  width: 200px;
}

.btn {
  border-radius: 8px;
  padding: 10px 20px;
  font-weight: 700;
  background-color: #646cff;
  border: none;
  color: white;
  cursor: pointer;
  margin-left: 1em;
  height: 45px;
}
```

## Creating Our Search Input

Open up the App.jsx file. Delete the following:

* the import of the React Logo

* the const for count

* everything inside the div with className of App

Your file should look like this:

```js
import { useState } from 'react'
import './App.css'

function App() {

  return (
    <div className="App">

    </div>
  )
}

export default App
```
We want to add a title, an input field, and a button. The input field. For the input field, we will use the `onChange` method to capture the text the user inputs and store it in a variable called `searchTerm`.

When a user clicks the button we want to call a function `findMusic` that will search the iTunes API.

Add the following code inside the `div` with a className of `App`:

```js
      <h1>Song Finder</h1>
      <input 
        type="text"
        placeholder="Enter search term"
        onChange={e => setSearchTerm(e.target.value)}
      ></input>
      <button className="btn" onClick={(() => findMusic() )}>Search</button>
      <hr></hr>
```

## Intro to the Apple iTunes API

If you want to read about the API you can find more details here.

To search the API, you call a URL that has this format:

https://itunes.apple.com/search?parameterkeyvalue

Where `parameterkeyvalue` can be one or more parameter keys and value pairs indicating the details of your query.

The one parameter we will be using is called `term`. Its value will be set to the `searchTerm` user entered in the input field.

## Create our Variables and Search Function

We need to create a state variable called searchTerm. On the line below the function App add the following code:

```js
const [searchTerm, setSearchTerm] = useState('');
```

Now we will create our `findMusic` function. The first thing we want to check is that the user has actually entered a search term into the input field. If they haven't, show them an alert asking them to enter a search phrase.

If we have a search term, we will use `fetch` to call the iTunes API. For now, add the following code:

```js
  const findMusic = () => {
    if (!searchTerm || searchTerm === '') {
      alert('Please enter a search term');
    } else {
      const url = `https://itunes.apple.com/search?term=${searchTerm}`;
      fetch(url)
        .then((response) => response.json())
        .then((data) => {
          console.log(data.results);
        })
    }
  }
```

If you input a search term, you should see results in your console like this:

![Image](https://res.cloudinary.com/ratracegrad/image/upload/v1673902630/Screenshot_2023-01-16_at_3.56.48_PM_mkyfhd.png)

We want to store these results in a state variable called `artists` which is an array.

Add this line below the other `useState` line:

```js
const [artists, setArtists] = useState([]);
```

In our `findMusic` function, replace the console.log with this code:

```js
setArtists(data.results);
```


## Displaying Search Results in a Table

We only want to display the table with the search results, when we actually have something. We can do this by only showing the table if our `artists` array has a length greater than zero.

If we have results then we want to create a table. The table will have four columns. The columns will display the following:

* Artwork

* Artist Name

* Track Name

* Price

We want one row in the table for each entry returned from the iTunes API. We will iterate over the entries using the Array `map` method.

Add the following code:

```js
     {artists.length && (
        <table>
          <thead>
            <tr>
              <th>Artwork</th>
              <th>Artist Name</th>
              <th>Track Name</th>
              <th>Price</th>
            </tr>
          </thead>
            <tbody>
              {artists.map((artist) => {
                const list = (
                  <>
                    <tr>
                    <td><img src={artist.artworkUrl60} alt={artist.artistName} /></td>
                      <td key={artist.artistId}>{artist.artistName}</td>
                      <td>{artist.trackCensoredName}</td>
                      <td>{artist.collectionPrice}</td>
                    </tr>
                  </>
                );
                return list;
              })}
            </tbody>
        </table>
      )}
```


## Final Result

If you view the app in your browser, you should see the completed results:

![Image](https://res.cloudinary.com/ratracegrad/image/upload/v1673900547/Screenshot_2023-01-16_at_3.21.50_PM_tyvecg.png)

