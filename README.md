# Autenticação via Firebase com React - exemplo básico

## 1. Como criar app React, ambiente Windows:

#### Se necessário instale o Node.js:

- Baixe o instalador do Node.js em nodejs.org.
- Siga as instruções do instalador para configurar o Node.js em seu sistema.

**Crie um novo projeto React** 

Abra o terminal (pode ser o PowerShell ou o Prompt de Comando).
Execute o seguinte comando para instalar o create-react-app globalmente:

```
npm install -g create-react-app
```

Em seguida, crie um novo projeto React com o comando:

```
npx create-react-app meu-projeto-react
```

Navegue até o diretório do projeto:

```
cd meu-projeto-react
```

Inicie o servidor de desenvolvimento:

```
npm start
```

Isso abrirá automaticamente uma página no seu navegador com o aplicativo React em execução.
em geral será localhost:3000 

## 2. Como criar app React ambiente Windows com autenticação via Firebase:

- Criar um novo projeto React em uma pasta Windows
  
```
npx create-react-app firebase-auth-app
cd firebase-auth-app
```

- Instalar as dependências do Firebase
```
npm install firebase
```

- Configurar o Firebase no seu aplicativo

    Vá para o Console do Firebase (https://console.firebase.google.com/)
    Crie um novo projeto ou selecione um projeto existente
    Vá para a seção "Authentication" e ative o método de autenticação que deseja usar (por exemplo, E-mail/senha)
    Clique em "Configuração do SDK" e copie as configurações do Firebase (apiKey, authDomain, etc.)

- Implementar a lógica de autenticação no seu aplicativo React

No arquivo src/App.js: adicionar o código para fazer login usando o Firebase Authentication. 
Exemplo básico:

### Lembre-se de preencher suas credenciais do Firebase.

```
import React, { useState } from 'react';
import firebase from 'firebase/compat/app'; // alterado aqui
import 'firebase/compat/auth'; // alterado aqui

// Configure Firebase
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_AUTH_DOMAIN",
  // adicione outras configurações do Firebase aqui
};

if (!firebase.apps.length) {
  firebase.initializeApp(firebaseConfig);
}

function App() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState(null);

  const handleLogin = async () => {
    try {
      await firebase.auth().signInWithEmailAndPassword(email, password);
      setError(null);
      // Login bem-sucedido, você pode redirecionar ou fazer outras ações aqui
    } catch (err) {
      setError(err.message);
    }
  };

  return (
    <div>
      <h1>Firebase Authentication</h1>
      <input
        type="email"
        placeholder="Email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
      />
      <input
        type="password"
        placeholder="Password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button onClick={handleLogin}>Login</button>
      {error && <p>{error}</p>}
    </div>
  );
}

export default App;

```


