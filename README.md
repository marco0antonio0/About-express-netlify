# Use Express para Backend sem um Frontend

![img](imageReadme/imageREADME.png)

## Netlify

A Netlify é uma plataforma de hospedagem e automação projetada para simplificar o desenvolvimento, implantação e gerenciamento de aplicativos web modernos. Funcionando como uma solução de PaaS (Platform as a Service), a Netlify oferece aos desenvolvedores uma abordagem fácil e eficiente para hospedar sites, aplicativos e funções serverless.

# About-express-netlify

This project demonstrates how to set up a basic Express.js server and deploy it on Netlify using serverless functions. Follow the steps below to implement this model.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Additional Resources](#additional-resources)

## Prerequisites

Before you begin, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or later)
- [npm](https://www.npmjs.com/) (v6 or later)
- [Netlify CLI](https://docs.netlify.com/cli/get-started/)

## Installation

1. **Clone the repository:**

    ```sh
    git clone https://github.com/marco0antonio0/About-express-netlify
    cd About-express-netlify
    ```

2. **Install dependencies:**

    ```sh
    npm install
    ```

## Configuration

1. **Create netlify.toml file:**

    ```sh
    [functions]
        external_node_modules = ["express"]
        node_bundler = "esbuild"

    [[redirects]]
        force = true
        from = "/api/*"
        status = 200
        to = "/.netlify/functions/api/:splat"

    [build]
        command = "echo Building Functions"
    ```

2. **Create netlify/functions/api.js file:**

    ```sh
        import express, { Router } from "express";
        import serverless from "serverless-http";

        const api = express();

        const router = Router();
        router.get("/hello", (req, res) => res.send("Hello World!"));

        api.use("/api/", router);

        export const handler = serverless(api);

    ```

3. **Ensure your package.json includes the necessary dependencies:**

    ```sh
        {
        "name": "example_project",
        "version": "1.0.0",
        "main": "index.js",
        "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
        },
        "keywords": [],
        "author": "",
        "license": "ISC",
        "description": "",
        "dependencies": {
            "@netlify/functions": "^2.7.0",
            "@types/express": "^4.17.21",
            "express": "^4.19.2",
            "serverless-http": "^3.2.0"
                }
        }
    ```

## Usage

Once deployed, you can access your Express.js API through the Netlify URL. For example, if your Netlify site is <https://yoursite.netlify.app>, you can access the API endpoint at:

  ```sh
  https://yoursite.netlify.app/api/hello
  ```

This should return Hello World!.

## Additional Resources

For more detailed information on deploying Express.js applications with Netlify, visit the Netlify [documentation](https://docs.netlify.com/frameworks/express/).

This README provides a comprehensive guide on how to set up, configure, and deploy an Express.js server on Netlify. It includes step-by-step instructions, making it easy for users to follow and implement the project.
