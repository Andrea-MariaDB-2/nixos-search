---
name: Custom issue template
about: Describe this issue template's purpose here.
title: ''
labels: ''
assignees: ''

---

name: CI

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [ 14.x ]

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Setup Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}

      - name: Install dependencies
        run: npm i

      - name: Run linting
        run: npm run lint

      - name: Run tests
        run: npm run coverage

      - name: Upload coverage to Codecov
        uses: codecov/codecov-action@v1
     
 - .yml
