# Use Express para Backend sem um Frontend

![img](imageReadme/imageREADME.png)

## Netlify

A Netlify é uma plataforma de hospedagem e automação projetada para simplificar o desenvolvimento, implantação e gerenciamento de aplicativos web modernos. Funcionando como uma solução de PaaS (Platform as a Service), a Netlify oferece aos desenvolvedores uma abordagem fácil e eficiente para hospedar sites, aplicativos e funções serverless.

## 1. Crie um novo projeto Express:

1.1 crie a pasta

```bash
mkdir my-express-backend
```

1.2 Acesse a pasta

```bash
cd my-express-backend
```

1.3 Inicie a estrutura inicial

```Bash
npm init -y
```

## 2. Instale as dependências necessárias:

```Bash
npm i express serverless-http @netlify/functions @types/express
```

## 3. Crie um arquivo de função Netlify para TypeScript ou JavaScript:

**Detalhe:** neste arquivo contera as declarações de rotas a serem dimensionadas de acordo com sua necessidade e de acordo com tal ira ser acessivel em : **_https://url_projeto/api/SuaFunção_**

Crie em o arquivo _api.ts_ ==> **"/netlify/functions/api.ts"** com os dados abaixo:

```Javascript

import express, { Router } from "express";
import serverless from "serverless-http";

const api = express();

const router = Router();
//===============================================================
//  Rotas a serem planejadas

router.get("/hello", (req, res) => res.send("Hello World!"));

api.use("/api/", router);

// n_rotas . . .
//===============================================================

export const handler = serverless(api);

```

## 4. Adicione a configuração no netlify.toml:

Crie o arquivo denominado _netlify.toml_ no diretorio _raiz_ do projeto e coloque os dados abaixo:

```
  <!-- ========================================================= -->
[functions]
  <!-- declara o pacote externo necessario para usar no servidor -->
  external_node_modules = ["express"]
  <!-- empacotador de funções netlify -->
  node_bundler = "esbuild"
  <!-- ========================================================= -->
[[redirects]]
  <!-- Redireciona as rotas para /api/ * -->
  force = true
  from = "/api/*"
  status = 200
  to = "/.netlify/functions/api/:splat"
  <!-- ========================================================= -->
[build]
    <!-- Builda a função para registro de logs no netlify -->
  command = "echo Building Functions"
```

## 5. Implante o aplicativo Express no Netlify:

- Faça commit do código no Git.
- Use o .gitignore para evitar subir arquivos node_modules
- Crie um repositório no GitHub ou em outro serviço de hospedagem.
- Conecte seu repositório ao Netlify para acionar implantações automáticas.

## 6. Acesse suas rotas do backend:

- As rotas do backend agora estão disponíveis no Netlify, por exemplo:

  ```Bash
  /api/rota_definida
  ```

- Você pode acessar essas rotas a partir de outros serviços ou ferramentas para testar ou integrar com o seu backend.
- As rotas são definidas apatir do arquivo **_api.ts_** localizado em **/netlify/functions/api.ts**

Documentação oficial acesse [netlify docs](https://docs.netlify.com/integrations/frameworks/express/)
