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

## Analyze the file
The known match results are home win, away win, and draw. Create an enum MatchResults with those three values.
Iterate through the parsed file.
Using a conditional and the values of the enum MatchResults, increment a counter to determine the number of wins for the desired team.

## Report the file
Console log a template string explaining the desired team and their corrosponding wins

# First Refactor!
In the first iteration, the data is hard coded. 
By creating a class, CsvFileReader, it allows the program to read files that may come from different sources, such as an API.
```
CsvFileReader.ts

import fs from 'fs'

export class CsvFileReader {
    data: string[][] = [];
    
    constructor(public filename: string){}

    read(): void{
        this.data = fs.readFileSync(this.filename,{
            encoding: 'utf-8'  
        })
        .split("\n")
        .map((row: string): string[] =>{
            return row.split(",")
        })
    }
}
```
Import the new class into index.ts and initialize it with the desired file name. 
Call the read method on the new class instance to parse it. 
