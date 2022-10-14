# firebase-utils-func

Hey guys,
I build a firebase-utils-func to manage people's time. When you create any firebase function you need to write much code. So I decided to build some helper functions to manage our time. It's a fun purpose I build this small library. Hope you guys enjoy it. 

## Installation

Use the package manager [firebase-utils-func](https://github.com/jsdevrazu/firebase-utils-func) to install firebase-utils-func

```bash
npm install firebase
npm install firebase-utils-func
#or
yarn add firebase
yarn add firebase-utils-func
```

## Config your firebase file
```javascript
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getStorage } from 'firebase/storage'
import { FacebookAuthProvider, getAuth, GoogleAuthProvider } from "firebase/auth";
import { getFirestore } from "firebase/firestore";


// Your web app's Firebase configuration
const firebaseConfig = {
  apiKey: "your api key",
  authDomain: "your auth domain",
  projectId: "your project id",
  storageBucket: "your storage storageBucket",
  messagingSenderId: "your messagingSenderId",
  appId: "your appId"
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);
export const storage = getStorage(app);
export const providerGoogle = new GoogleAuthProvider();
export const providerFacebook = new FacebookAuthProvider();
export const db = getFirestore(app)
export const auth = getAuth(app);
```
## All module import
```javascript
import {
  uploadFiles,
  registerApi,
  loginApi,
  googleApi,
  facebookApi,
  forgotPassApi,
  signOutApi,
  createCollection,
  updateCollection,
  deleteCollection,
  getCollections,
  getCollection,
} from "firebase-utils-func";
```

## Usage Upload File
```javascript
import { ChangeEvent,, useState } from "react";
import { storage } from "../firebase"; //your firebase config file auth variable
import { uploadFiles } from "firebase-utils-func"; //import uploadFiles function from firebase-utils-func


const Home = () => {
  const [files, setFiles] = useState([])

  const uploadFile = (e) =>{
    if(!e.target.files) return;
    setFiles([...e.target.files])
  }

  const handleSubmit = async (e) =>{
    e.preventDefault();
    try {
        const res = await uploadFiles(storage, "demo", files);
        console.log(res)
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <input type="file" onChange={uploadFile} />
      <button type="button" onClick={handleSubmit}>Upload File</button>
    </>
  );
};

export default Home;
```

## Usage Register Firebase Function
```javascript
import { useState } from "react";
import { auth } from "../firebase"; //your firebase config file auth variable
import { registerApi } from "firebase-utils-func"; //import registerApi function from firebase-utils-func

const Home = () => {
const [email, setEmail] = useState("")
const [password, setPassword] = useState("");

  const handleSubmit = async (e) =>{
    e.preventDefault();
    try {
        const data = { email, password }
        const res = await registerApi(auth, "your collection name", data);
        console.log(res)
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <input type="text" value={email} onChange={e => setEmail(e.target.value)} />
      <input type="text" value={password} onChange={e => setPassword(e.target.value)} />
      <button type="button" onClick={handleSubmit}>Register Now</button>
    </>
  );
};

export default Home;
```

## Usage Login Firebase Function
```javascript
import {useState } from "react";
import { auth } from "../firebase"; //your firebase config file auth variable
import { loginApi } from "firebase-utils-func"; //import loginApi function from firebase-utils-func

const Home = () => {
const [email, setEmail] = useState("")
const [password, setPassword] = useState("");

  const handleSubmit = async (e) =>{
    e.preventDefault();
    try {
        const data = { email, password }
        const res = await loginApi(auth, data);
        console.log(res)
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <input type="text" value={email} onChange={e => setEmail(e.target.value)} />
      <input type="text" value={password} onChange={e => setPassword(e.target.value)} />
      <button type="button" onClick={handleSubmit}>Login Now</button>
    </>
  );
};

export default Home;
```

## Usage Google Login Firebase Function
```javascript
import { auth, provierGoogle } from "../firebase"; //your firebase config file auth and provierGoogle variable
import { googleApi } from "firebase-utils-func"; //import googleApi function from firebase-utils-func

const Home = () => {
  const handleSubmit = async (e) =>{
    e.preventDefault();
    try {
        const data = { email, password }
        const res = await googleApi(auth, provierGoogle);
        console.log(res)
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <button type="button" onClick={handleSubmit}>Login With Google</button>
    </>
  );
};

export default Home;
```

## Usage Facebook Login Firebase Function
```javascript
import { auth, provierFacebok} from "../firebase"; //your firebase config file auth and provierGoogle variable
import { facebookApi } from "firebase-utils-func"; //import facebookApi function from firebase-utils-func

const Home = () => {
  const handleSubmit = async (e) =>{
    e.preventDefault();
    try {
        const data = { email, password }
        const res = await facebookApi(auth, provierFacebok);
        console.log(res)
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <button type="button" onClick={handleSubmit}>Login With Facebook</button>
    </>
  );
};

export default Home;
```

## Usage Forgot Password Firebase Function
```javascript
import { auth } from "../firebase"; //your firebase config file auth variable
import { forgotPassApi } from "firebase-utils-func"; //import forgotPassApi function from firebase-utils-func

const Home = () => {
const [email, setEmail] = useState("")
  const handleSubmit = async (e) =>{
    e.preventDefault();
    try {
        const res = await forgotPassApi(auth, email);
        console.log(res)
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <input type="text" value={email} onChange={e => setEmail(e.target.value)} />
      <button type="button" onClick={handleSubmit}>Forgot Password</button>
    </>
  );
};

export default Home;
```

## Usage Logout Firebase Function
```javascript
import { auth } from "../firebase"; //your firebase config file auth variable
import { signOutApi } from "firebase-utils-func"; //import signOutApi function from firebase-utils-func

const Home = () => {
  const handleLogout = async () =>{
    e.preventDefault();
    try {
        await signOutApi(auth);
       //next js push to login page before router import router from  next/router
       router.push("/login")
       //react js push to login page before navigate import navigate from useNavigate()
       navigate("/login")
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <button type="button" onClick={handleLogout}>Logout/button>
    </>
  );
};

export default Home;
```

## Usage Create Database Collection Firebase Function
```javascript
import { db } from "../firebase"; //your firebase config file auth variable
import { createCollection } from "firebase-utils-func"; //import createCollection function from firebase-utils-func

const Home = () => {
  const handleSubmit = async (e) =>{
    e.preventDefault();
    try {
       const data = {email:"example@email.com", fullname:"demo user"}
        const res = await createCollection(db, "your collection name", data);
        console.log(res)
    } catch (error) {
      console.log(error.message)
    }
  }

  return (
    <>
      <button type="button" onClick={handleSubmit}>Create User/button>
    </>
  );
};

export default Home;
```

## Usage Get All Data From Database Collection Firebase Function
```javascript
import { useEffect } from "react";
import { db } from "../firebase"; //your firebase config file auth variable
import { getCollections } from "firebase-utils-func"; //import getCollections function from firebase-utils-func

const Home = () => {

  useEffect(() => {
    const getData = async () => {
      try {
        const res = await getCollections(db, "your collection name");
        console.log(res);
      } catch (error) {
        console.log(error.message);
      }
    };
    getData();
  }, []);
};

export default Home;
```

## Usage Get Single Data From Database Collection Firebase Function
```javascript
import {useEffect } from "react";
import { db } from "../firebase"; //your firebase config file auth variable
import { getCollection } from "firebase-utils-func"; //import getCollections function from firebase-utils-func

const Home = () => {
//in next js before you need import useRouter hooks
const { id } = router.query;
//in react.js you need import useParams hooks
const { id } = useParams();

  useEffect(() => {
    const getSingleData = async () => {
      try {
        const res = await getCollection("your collection name", db, id);
        console.log(res);
      } catch (error) {
        console.log(error.message);
      }
    };
    getSingleData ();
  }, []);
};

export default Home;
```

## Usage Get Single Data From Database Collection Firebase Function
```javascript
import {useEffect } from "react";
import { db } from "../firebase"; //your firebase config file auth variable
import { updateCollection } from "firebase-utils-func"; //import updateCollection function from firebase-utils-func

const Home = () => {
  const updateData = async () => {
  const data = {email:"example@email.com", fullname:"demo user"}
    try {
     await updateCollection(db, "your collection name", data);
    } catch (error) {
      console.log(error.message);
    }
  };

  return (
    <>
      <button type="button" onClick={updateData}>
        Update User
      </button>
    </>
  );
};

export default Home;

```

## Usage Get Single Data From Database Collection Firebase Function
```javascript
import { useEffect } from "react";
import { db } from "../firebase"; //your firebase config file auth variable
import { deleteCollection } from "firebase-utils-func"; //import deleteCollection function from firebase-utils-func

const Home = () => {
  const updateData = async () => {
  const data = {id:1, email:"example@email.com", fullname:"demo user"}
    try {
     await deleteCollection(db, "your collection name", data);
    } catch (error) {
      console.log(error.message);
    }
  };

  return (
    <>
      <button type="button" onClick={updateData}>
        Delete User
      </button>
    </>
  );
};

export default Home;

```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
Copyright (c) 2022 jsdevrazu

About Me:
[portfolio](http://devcoded.com)
[buy me a coffee](https://www.buymeacoffee.com/jsdevrazu)