## Demo

- [Plain text joiner](https://godicheol.github.io/javascript-string/)

## Usage

```js
import jsStr from "js-str";
```

```js
var str = `Lorem ipsum dolor sit amet, consectetur adipiscing elit.`;

jsStr.get(str, [0, 5]); // "Lorem"

jsStr.search(str, "l", {case: true}); // [[0, 1], [14, 15], [52, 53]]
jsStr.search(str, ["l", "L"]); // [[0, 1], [14, 15], [52, 53]]
jsStr.search(str, ["l"], {case: true}); // [[0, 1], [14, 15], [52, 53]]
jsStr.search(str, /l/i); // [[0, 1], [14, 15], [52, 53]]
jsStr.search(str, /l/i, {case: true}); // [[0, 1], [14, 15], [52, 53]]
jsStr.search("Ｌｏｒｅｍ", "lorem", {case: true, width: true}); // [[0, 5]]

jsStr.replace(str, [[6, 11]], "IPSUM"); // "Lorem IPSUM ..."

jsStr.split(str, [[6, 11]]); // ["Lorem ", " dolor..."]

jsStr.compare("a", "b"); // -1
jsStr.compare("b", "a"); // 1
jsStr.compare("a", "a"); // 0

jsStr.parse(before, after);
jsStr.parse(before, after, {case: true});
// [{
//     isMatched: Boolean,
//     from: [0, 0], // before
//     to: [0, 3] // after
// }, ...]

```

- Sort array

```js
var arr = ["B","1A","1B","a-2","한국어","1","#","日本語","عربي","2","A","a-12"]

arr.sort(jsStr.compare);
// ['#', '1', '1A', '1B', '2', 'A', 'B', 'a-2', 'a-12', 'عربي', '日本語', '한국어']
```

- Parse

```js
var a = "a...";
var b = "b...";
jsStr.parse(a, b).map(function(item) {
    return {
        isMatched: item.isMatched,
        from: jsStr.get(a, item.from),
        to: jsStr.get(b, item.to),
    };
});
// [{
//     isMatched: false,
//     from: "a", // before
//     to: "b" // after
// }, {
//     isMatched: true,
//     from: "...", // before
//     to: "..." // after
// }]
```

- Match

```js
var a = `Lorem ipsum dolor sit amet, consectetur adipiscing elit.`;
var b = "ipsum consectetur";

jsStr.match(a, b); // 0.30357142857142855
jsStr.match(b, a); // 1
```