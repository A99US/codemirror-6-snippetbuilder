
# Snippet Builder For CodeMirror 6

This is a function for CodeMirror 6 to convert a standard array of snippet (like [this one](https://github.com/capaj/vscode-standardjs-snippets/blob/master/snippets/javascript.json)) and turn it into snippet array that is ready to use in CodeMirror 6 extension.

## How To Use

First you need to add the extension :

```console
npm i codemirror-6-snippetbuilder
```

And then import the function :

```javascript
import snippetbuilder from 'codemirror-6-snippetbuilder'
```

You also need a *'normal'* snippet array to be converted by the function. For example, this one will come from a file : 

```javascript
import jssnippetarray from './snippetarray.js'
```

And then you feed CodeMirror 6 extension with an array built by this function. For example :

```javascript
javascriptLanguage.data.of({
  autocomplete: snippetbuilder({
    source: jssnippetarray 
  })
})
```
	
**Important Note :** The source snippet array **MUST HAVE AT LEAST**  index ***'body'*** in the following design :

```JSON
{
  /*
  "Snippet Keyword / Prefix": {
    "scope": "lang1,lang2,lang3,lang4",
    "body": ["body","of","snippet"],
    "description": "Snippet Description"
  }
  */
  "attr set": {
    "scope": "js,ts",
    "body": ["$('${selector}').attr('${attr}','${value}');${}"],
    "description": "Setting value for certain attribute."
  }
}
```

 - Index Key : Will be the keyword / prefix for the snippet (Mandatory)
 - Body : Snippet body (Mandatory)
 - Description : Description of the snippet (Optional)
 - Scope : Language scope (Optional)

## Setting


```javascript
snippetbuilder({
  source: snippetsource, // Mandatory
  description: true, // Optional, default true
  scope: 'javascript', // Optional, default ''
  prefix: 'jqr ' // Optional, default ''
})
```

**Source :** 
Snippet array to be converted. 

**Description :** 
Whether description should be added to the snippet popup or not. Default true, if description is present in the source array.

 **Scope :** 
 If set, function will filter to only include snippet that is in the scope. Only usable if source array has *scope* index. Filter by *scopes.includes(scope)*.
 For example, if you only want to use snippet of react :
 
```javascript
snippetbuilder({
  source: jssnippetarray,
  scope: 'javascriptreact'
})
```

With the following array source, will only add *javascriptreact* to snippet.

```javascript
{
  "Prefix1": {
    "scope": "javascript,javascriptreact",
    "body": "//Body here",
    "description": "Snippet for javascript and javascriptreact"
  },
  "Prefix2": {
    "scope": "javascriptreact",
    "body": "//Body here",
    "description": "Snippet for javascriptreact only"
  }
}
```

 **Prefix :** 
Add prefix to snippet popup. Will be part of snippet keyword. Default *null*.

## To-Do List

 - Multiple scopes filter.
 - Dynamic index name for possible non-common array source.
 - Interchangeability of keyword / prefix for possible non-common array source. Snippet keyword could be taken from item index or prefix, or both. For now it's fixed from item index instead of *prefix* for readability reason.

## License

MIT
