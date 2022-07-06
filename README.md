#The_Real_Project

name: Running Code Coverage

on: [push, pull_request]

jobs:
  build:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: 8.11.0

    steps:
    - name: Checkout repository
      uses: actions/checkout@v2
      with:
        fetch-depth: 2

    - name: Set up Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ matrix.node-version }}

    - name: Install dependencies
      run: npm install

    - name: Run tests
      run: npm run test

    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v1
