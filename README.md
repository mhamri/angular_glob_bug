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

run this command

```cmd
npm run build -- -c a1WithoutStarAtStart
```

with this config

```
"a1WithoutStarAtStart": {
  "assets": [
    {
      "glob": "a/**/*.jpg",
      "input": "src/folderToCopyContentFrom",
      "output": "a1WithoutStarAtStart_OK"
    }
  ]
},
```

it copies `a` folder content as it is.

---

but run this command

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
      "output": "a1StarAtStart_NotOK"
    }
  ]
},
```

it copies **nothing**!

---

and run this command

```cmd
npm run build -- -c aDeepSearch
```

with this config

```
"aDeepSearch": {
  "assets": [
    {
      "glob": "**/a/a*/*.jpg",
      "input": "src/folderToCopyContentFrom",
      "output": "aDeepSearch_Out"
    }
  ]
},
```

it copies **nothing**!
