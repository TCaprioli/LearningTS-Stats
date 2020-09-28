# LearningTS-Stats

## Setting up the Environment

Create the package.json and tsconfig.json with: `npm init -y` & `tsc --init`

Create a src and build folder in the rootdir

Install nodemon & concurrently: `npm install nodemon concurrently`

Link src and build folders to the rootDir and outDir in tsconfig.json

Update the scripts in the package.json to include:
```
"start:build": "tsc -w",
"start:run": "nodemon build/index.js",
"start": "concurrently npm:start:*"
```
## Goals
*  Load the csv file
*  Parse it
*  Analyze it
*  Report it

## Loading the file
To load the file, import the node fs API: `import fs from 'fs'`
fs.readFileSync() will load the file and return a string

## Parsing the file
To parse, split the loaded file by \n. Iterate through the array by mapping it and splitting each element again by a comma:
```
.split("\n").map((row: string): string[] =>{
    return row.split(",")
})
```
