# PokeChallenge

import { useState, useEffect } from 'react';

const useApiData = (url) => {
  const [data, setData] = useState([]);


  // API -> Son funcionalidades de acceso a información sin tener que pasar por una base de datos

  // REST -> La que nos devuelve información en formato JSON

  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch(url);
      const resultTotal = await response.json();
      setData(resultTotal.results);
    };

    fetchData();
  }, [url]);

  const renderCards = () => {
    return data.map((item) => {
      return (
        <div key={item.name}>
          <h2>{item.name}</h2>
          <p>{item.url}</p>
        </div>
      );
    });
  };

  return { data, renderCards };
};

export default useApiData;



// ------->

import logo from './logo.svg';
import './App.css';
import useApiData from './Custom';

function App() {
  const { renderCards } = useApiData('https://pokeapi.co/api/v2/pokemon');

  return (
    <div>
      {renderCards()}
      <button>NEXT</button>
    </div>
  );
}

export default App;
