# Exercise 2 - Writing a whole function with Copilot

Now we're going to stretch GitHub Copilot a little further and use it to write a few functions that will help us!

1. Create a new file called `syllable-counter.js`
2. Add a comment at the top of the file and press Enter:

```javascript
// import syllables counting library
```

Copilot should suggest something similar to:
```javascript
var syllable = require('syllable');
```

3. Press Enter a few more times and add this comment then press Enter:
```javascript
// function to test the number of syllables in a sentence
```

Copilot should help you write a function to count syllables.

_Important: GitHub Copilot is non-deterministic! That means you may not get the same result as the person next to you, or even if you try it multiple times. It's important to remember that Copilot is just an AI assistant. It can't write perfect code!_

Below, find an example of one implementation provided by GitHub Copilot. Yours may look very different! If you get stuck, expand the below for an implementation you can use.

<details>

```javascript
// import syllables counting library
var syllable = require('syllable');

// function to test the number of syllables in a sentence
export function countSyllables(sentence) {
    var words = sentence.split(' ');
    var totalSyllables = 0;
    words.forEach(function(word) {
        totalSyllables += syllable(word);
    });
    return totalSyllables;
    }
}
```
</details>

Now let's use this function in a new route. You'll get fewer hints for the next few steps! Try to get GitHub Copilot to help you along the way, and correct if necessary.

4. Open the `index.js` file again
5. On a new line after line 4, add a reference to your syllable counter: 
```javascript
const syllablecounter = require('./syllable-counter.js');
```
6. On a new line below the `app.get` function (approximately line 16), add a new comment, then press Enter.
```javascript
// write a status route to test each haiku's syllable count and return the results in json
```

GitHub Copilot should start to help you write a new status route.

**Some tips:**
- GitHub Copilot will do better if you have the `syllable-counter.js` file open in another tab.
- You may need to explicitly ask GitHub Copilot to split each haiku into lines!
- If you're getting an unhelpful response, try providing more context - either a more detailed comment, or starting to type what you think you'll need next.

If you get stuck, expand the below for an implementation you can use:

<details>

```javascript
// write a status route to test each haiku's syllable count and return the results in json
app.get('/status', (req, res) => {
  let status = [];
  haikus.forEach(function(haiku) {
    // split by line
    let lines = haiku.text.split('\n');
    // count syllables in each line
    let syllables = lines.map(function(line) {
      return syllablecounter.countSyllables(line);
    });
    // check if syllables are correct
    let correct = syllables[0] === 5 && syllables[1] === 7 && syllables[2] === 5;
    // add to status array
    status.push({
      haiku: haiku.text,
      correct: correct,
      syllables: syllables
    });
  });
  res.json(status);
});
```

</details>

7. Open the `package.json` file
8. Add a new entry to the list of dependencies (line 15): 
```json
"syllable": "^5.0.0"
```
8. Once you're finished, debug and navigate to the `/status` page (or whatever equivalent you've produced).

You should see a JSON output with an indication of which Haikus have the correct syllables (which might be wrong, but that wasn't the point!)

## Resources:
- [GitHub Copilot](https://gh.io/copilot)
- [GitHub Copilot Prompt Engineering](https://dev.to/github/a-beginners-guide-to-prompt-engineering-with-github-copilot-3ibp)