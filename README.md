# A repo to show glob mistake

there is a folder in the src folder named `folderToCopyContentFrom` the structure of the folder is like this

```
---| folderToCopyContentFrom
               |
               |--------A
                        |----a.jpg
                        |----A1
                             |-----a1.jpg
               |--------B
                        |----b.jpg
                        |----B1
                             |-----b1.jpg

```

# 1-

run this command

```cmd
npm run build -- -c a1WithoutStarAtStart
```

with this config

```json
"a1WithoutStarAtStart": {
  "assets": [
    {
      "glob": "a/**/*.jpg",
      "input": "src/folderToCopyContentFrom",
      "output": "a1WithoutStarAtStart_Out"
    }
  ]
},
```

I expect to look into the folder a and go in any level of folders and copy anything inside. but look like the glob is exactly looking for `**/*.{ext}` and rest is magic

you will see that the output in dist folder is like this

```
---| folderToCopyContentFrom
               |
               a  <--- actually this is part of glob that spilling out to output path
               |--------A
                        |----a.jpg
                        |----A1
                             |-----a1.jpg
```

# 2-

run this command

```cmd
npm run build -- -c a1StarAtStart
```

with this config

```
"a1StarAtStart": {
  "assets": [
    {
      "glob": "*a/**/*.jpg",
      "input": "src/folderToCopyContentFrom",
      "output": "a1StarAtStart_Out"
    }
  ]
},
```

it copies **nothing**! clearly `*a` isn't a valid path

# 3-

run this command

```cmd
npm run build -- -c a1StarAtStart
```

with this config

```
"aDeepSearch": {
  "assets": [
    {
      "glob": "**/A1/**/*.jpg",
      "input": "src/folderToCopyContentFrom",
      "output": "aDeepSearch_Out"
    }
  ]
},
```

it copies **nothing**! clearly there is nothing to match with `**/*.{ext}` but it's a valid glob. I expect to see that `a.jpg` and `a1.jpg` both get copied to asset folder.
