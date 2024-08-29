# 0x03. Queuing System in JS

## Overview

In this project, you will learn how to create and manage a queuing system using Redis and Node.js. Redis is a powerful in-memory data structure store used as a database, cache, and message broker. You will also use `Kue`, a priority job queue backed by Redis, to manage job processing in Node.js. This project will guide you through the process of setting up a Redis server, performing basic operations, and integrating Redis with Node.js and Express to build a simple queue system.

## Learning Objectives

By the end of this project, you should be able to:

- Run a Redis server on your local machine.
- Perform simple operations using the Redis client.
- Integrate Redis with Node.js to perform basic operations.
- Store and retrieve hash values in Redis.
- Manage async operations with Redis in Node.js.
- Use `Kue` to set up and manage a queuing system.
- Build a basic Express app that interacts with Redis and a queue system.

## Requirements

- **Operating System:** Ubuntu 18.04 LTS
- **Node.js Version:** 12.x
- **Redis Version:** 5.0.7
- **File Extension:** `.js`
- **Code Style:** Your code should conform to standard JavaScript practices.
- **README:** A `README.md` file at the root of the project directory is mandatory.
- **Node.js Packages:** Don’t forget to run `$ npm install` after creating your `package.json` file.

## Project Setup

### Required Files

- **`package.json`**: Configuration file for Node.js projects, specifying dependencies and scripts.
- **`.babelrc`**: Configuration file for Babel, used for transpiling JavaScript.

### Example `package.json`

```json
{
  "name": "queuing_system_js",
  "version": "1.0.0",
  "description": "Queuing system using Redis and Node.js",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "express": "^4.17.1",
    "kue": "^0.11.6",
    "redis": "^3.0.2"
  }
}

