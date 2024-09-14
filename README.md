# Fast-Finder-Search-Bar
npx create-react-app country-search
cd country-search
npm start
src/
  components/
    SearchBar.js
  data/
    countriesData.js
  App.js
  App.css
const countriesData = [
  {
    "country": "United States",
    "capital": "Washington, D.C.",
    "population": 331002651,
    "official_language": "English",
    "currency": "United States Dollar"
  },
  {
    "country": "Canada",
    "capital": "Ottawa",
    "population": 37742154,
    "official_language": ["English", "French"],
    "currency": "Canadian Dollar"
  },
  // (Continue with the rest of the provided JSON data)
];

export default countriesData;
import React, { useState } from 'react';
import countriesData from '../data/countriesData';
import './SearchBar.css'; // Custom styles for the component

const SearchBar = () => {
  const [inputValue, setInputValue] = useState('');
  const [suggestions, setSuggestions] = useState([]);

  // Function to handle input change and filter suggestions
  const handleInputChange = (event) => {
    const value = event.target.value.toLowerCase();
    setInputValue(value);

    if (value) {
      const filteredSuggestions = countriesData.filter(
        (item) =>
          item.country.toLowerCase().includes(value) ||
          item.capital.toLowerCase().includes(value)
      );
      setSuggestions(filteredSuggestions);
    } else {
      setSuggestions([]);
    }
  };

  // Handle suggestion selection
  const handleSuggestionClick = (suggestion) => {
    setInputValue(`${suggestion.country} - ${suggestion.capital}`);
    setSuggestions([]);
  };

  return (
    <div className="search-bar-container">
      <input
        type="text"
        placeholder="Search by country or capital"
        value={inputValue}
        onChange={handleInputChange}
        className="search-input"
      />

      {suggestions.length > 0 && (
        <ul className="suggestions-list">
          {suggestions.map((item, index) => (
            <li
              key={index}
              className="suggestion-item"
              onClick={() => handleSuggestionClick(item)}
            >
              {item.country} - {item.capital}
              <div className="suggestion-details">
                <p>Population: {item.population.toLocaleString()}</p>
                <p>
                  Language: {Array.isArray(item.official_language)
                    ? item.official_language.join(', ')
                    : item.official_language}
                </p>
                <p>Currency: {item.currency}</p>
              </div>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default SearchBar;
/* Container for the search bar */
.search-bar-container {
  width: 400px;
  margin: 20px auto;
  position: relative;
}

/* Search input styling */
.search-input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #ccc;
  border-radius: 25px;
  outline: none;
}

.search-input:focus {
  border-color: #007bff;
}

/* Suggestions list styling */
.suggestions-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
  position: absolute;
  width: 100%;
  max-height: 300px;
  overflow-y: auto;
  background-color: white;
  border: 1px solid #ccc;
  border-top: none;
  border-radius: 0 0 25px 25px;
}

.suggestion-item {
  padding: 10px;
  cursor: pointer;
  background-color: white;
}

.suggestion-item:hover {
  background-color: #f1f1f1;
}

.suggestion-details {
  font-size: 14px;
  color: #555;
  padding-left: 10px;
}

.suggestion-details p {
  margin: 5px 0;
}
import React from 'react';
import SearchBar from './components/SearchBar';
import './App.css'; // Import the main styles

const App = () => {
  return (
    <div className="app-container">
      <h1>Country Search</h1>
      <SearchBar />
    </div>
  );
};

export default App;
.app-container {
  text-align: center;
  font-family: Arial, sans-serif;
  padding: 50px;
  background-color: #f9f9f9;
}

h1 {
  color: #333;
  margin-bottom: 20px;
}
npm start
