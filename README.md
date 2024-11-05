# How to Create a React + Flask Project with Vite 

***These setting are for Windows and VS Code and I suppose the React is already installed on your computer.***
***It is not necessary to clone, just follow the instructions and on the end all will be set.***

## 1. Create folder name "REACT_FLASK" and run following commnads:
inside of this folder:

- npx create-vite
    - select name: client, select framwerok: React, select language: JavaScript
    - above command will also create sub-folder "client"  
- cd client
- npm install

## 2. Create sub-folder "server" (in REACT_FLASK folder)
- cd server
- create virtual envirmonemt and activate it:
    - python -m venv venv
    - venv\Scripts\activate
- pip install Flask
- pip install Flask-CORS
  
## 3. Create file "main.py" in server (Flask) folder:
```
from flask import Flask, jsonify
from  flask_cors import CORS

app = Flask(__name__)
cors = CORS(app, origins='*')
 

@app.route("/api/users", methods=['GET'])
def users():
    return jsonify({"users": ["user1", "user2", "user3"]})

if __name__ == '__main__':
    app.run(debug=True, port=8080)
```

## 4. Open second terminal (one for server and second for client)
***in second (client) terminal:***
- cd client
- npm install axios
    - (Axio is to fetch API requests to our server)
- npn run dev
  
## 5. Start Python server: Run main.py directly in VS Code or command "python main.py" in first terminal (in server folder)

## 6. Modify App.jsx (client/src/App.jsx):
```
import { useState, useEffect } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'
import axios from 'axios';

function App() {
  const [count, setCount] = useState(0)
  const [array, setArray] = useState([]);

  const fetchAPI = async () => {
    const response = await axios.get("http://127.0.0.1:8080/api/users");
    console.log(response.data.users);
    setArray(response.data.users); 
  } ;

  useEffect(() => {
    fetchAPI();
  }, []);

  return (
    <>
      <div>
        <a href="https://vite.dev" target="_blank">
          <img src={viteLogo} className="logo" alt="Vite logo" />
        </a>
        <a href="https://react.dev" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1>Vite + React</h1>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        
          {array.map((user, index) => (
            <div key ={index}>
              <span key={index}>{user}</span>
              <br></br>
            </div>
          ))}
        
        <p>
          Edit <code>src/App.jsx</code> and save to test HMR
        </p>
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  )
}

export default App
```

## Now everything is set and you can see the data from Flask on React page :) 

### Printscreen:
![image](https://github.com/user-attachments/assets/695ece42-858f-4bbf-8010-708ffc544b70)


