# Song Finder

This is a React-based web application that allows you to search for songs and their corresponding artist information using the iTunes API. 

[Launch Live Preview](https://celadon-queijadas-c8cba0.netlify.app/)


## Table of Contents

- [Code Breakdown](#code-breakdown)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)
- [Contact](#contact)


## Code Breakdown

1. **Search by song:** Users can enter a song title or artist name to search for a specific song or artist. The search function uses the iTunes API to retrieve data.

2. **Display results:** The app displays the search results in a table, including artwork, artist name, track name, and price.

This is a React component called **`App`** which is the main component for the Song Finder project.

The code starts by importing **`useState`** hook from the **`react`** library and the CSS file for styling the app.

```jsx
import { useState } from 'react'
import './App.css'
```

The **`useState`** hook allows us to use state in a functional component.

The **`App`** component contains two state variables, **`searchTerm`** and **`artists`**, both of which are created using the **`useState`** hook. **`searchTerm`** is used to store the value of the search term entered by the user, while **`artists`** is used to store the array of artists that are returned from the iTunes API.

```jsx
  const [searchTerm, setSearchTerm] = useState('');
  const [artists, setArtists] = useState([]);
```

The **`findMusic`** function is called when the user clicks the search button. It checks if a search term has been entered and if so, it uses **`fetch`** to call the iTunes API with the search term. When the API call returns, it updates the **`artists`** state variable with the results.

```jsx
  const findMusic = () => {
    if (!searchTerm || searchTerm === '') {
      alert('Please enter a search term');
    } else {
      const url = `https://itunes.apple.com/search?term=${searchTerm}`;
      fetch(url)
        .then((response) => response.json())
        .then((data) => {
          setArtists(data.results);
        })
    }
  }
```

The **`return`** statement contains the JSX code that defines the UI of the app. It contains a header with the title "Song Finder", an input field for entering the search term, and a button to initiate the search. When the user clicks the search button, the **`findMusic`** function is called. If **`artists`** state variable has any items, a table is displayed with the details of the artists.

```jsx
  return (
    <div className="App">
      <h1>Song Finder</h1>
      <input
        type="text"
        placeholder="Enter search term"
        onChange={e => setSearchTerm(e.target.value)}
      ></input>
      <button className="btn" onClick={(() => findMusic() )}>Search</button>
      <hr></hr>
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
    </div>
  )

```

Overall, this code is responsible for rendering the UI of the Song Finder app and fetching and displaying the data from the iTunes API in a table.


## Technologies Used

- ReactJS
- JavaScript (ES6+)
- HTML
- CSS
- iTunes API (for fetching music data)

## Installation

1. Clone the repository:

```js
git clone https://github.com/mmartins23/react-song-finder
```

2. Change into the project directory:

```js
cd react-song-finder
```

3. Install dependencies:

```js
npm install
```

4. Start the development server:

```js
npm start
```

This will start the app on http://localhost:3000 in your browser.

## Usage

1. Start the application: `npm start`
2. Enter a search term in the input field and click the "Search" button
3. View the search results in the table below the search bar


## License

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://opensource.org/licenses/MIT)

This project is licensed under the terms of the MIT license. See [LICENSE](LICENSE) for more information.


## Contact

You can reach me on [Twitter](https://twitter.com/23mmartins)


Feel free to send me a message if you have any questions or feedback about this project. I'll do my best to respond as soon as possible.
