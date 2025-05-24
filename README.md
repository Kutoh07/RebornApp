# HTML Code Documentation for Beginners

This documentation explains every block of code in the **Index** and **Guess** HTML files in simple terms.

---

## 📋 **INDEX.HTML - Form Page**

### 1. **HTML Structure Setup**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title id="page-title">Welcome to your new life</title>
```
**What it does:** 
- Sets up the basic HTML document structure
- `DOCTYPE html` tells the browser this is an HTML5 document
- `<head>` contains information about the page (not visible to users)
- `charset="UTF-8"` supports international characters (like French accents)
- `viewport` makes the page work well on mobile devices

### 2. **External Resources Loading**
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.0/font/bootstrap-icons.css" rel="stylesheet">
```
**What it does:**
- Links to **Bootstrap CSS** (makes the page look modern and responsive)
- Links to **Bootstrap Icons** (provides icons like 🌐, 👤, etc.)
- These are hosted online, so you need internet connection

### 3. **Custom Styling**
```html
<style>
  body {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    min-height: 100vh;
  }
  .card {
    background: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(10px);
    /* ... more styles ... */
  }
</style>
```
**What it does:**
- **Custom CSS** that overrides default styling
- `linear-gradient` creates a beautiful blue-purple background
- `rgba(255, 255, 255, 0.95)` creates semi-transparent white cards
- `backdrop-filter: blur(10px)` creates a frosted glass effect

### 4. **Form Structure**
```html
<form onsubmit="storeData(); return false;">
  <div class="row mb-4">
    <div class="col-md-6">
      <label id="label-language" class="form-label fw-semibold">🌐 Language</label>
      <select class="form-select" id="language" onchange="changeLanguage()">
        <option value="en">🇺🇸 English</option>
        <option value="fr">🇫🇷 Français</option>
      </select>
    </div>
  </div>
</form>
```
**What it does:**
- `<form>` wraps all input fields
- `onsubmit="storeData(); return false;"` runs JavaScript when form is submitted
- `return false` prevents the page from refreshing
- `onchange="changeLanguage()"` runs JavaScript when language is changed
- Bootstrap classes like `row`, `col-md-6` create responsive layout

### 5. **JavaScript - Language Translations**
```javascript
const translations = {
  en: {
    title: "Welcome to your new life",
    subtitle: "This app will help you...",
    // ... more translations
  },
  fr: {
    title: "Bienvenue dans votre nouvelle vie",
    subtitle: "Cette application vous aidera...",
    // ... more translations
  }
};
```
**What it does:**
- **Object** that stores text in different languages
- `en:` contains English text, `fr:` contains French text
- Makes it easy to switch the entire page language

### 6. **JavaScript - Language Switching**
```javascript
function changeLanguage() {
  const selectedLang = document.getElementById('language').value;
  const t = translations[selectedLang];
  
  document.getElementById('page-title').textContent = t.title;
  document.getElementById('main-title').textContent = t.title;
  // ... update more elements
}
```
**What it does:**
- **Function** that runs when user changes language
- `document.getElementById()` finds HTML elements by their ID
- `.textContent` changes the text inside elements
- Updates all text on the page to the selected language

### 7. **JavaScript - Loading Countries**
```javascript
async function loadCountries() {
  try {
    const response = await fetch('https://restcountries.com/v3.1/all?fields=name,flag,cca2');
    const countries = await response.json();
    // ... process countries
  } catch (error) {
    console.error('Error loading countries:', error);
    // ... fallback countries
  }
}
```
**What it does:**
- **Async function** that can wait for internet requests
- `fetch()` gets data from an online API (list of countries)
- `await` waits for the request to finish
- `try/catch` handles errors if the internet request fails
- Populates the country dropdown with real country data

### 8. **JavaScript - Data Storage**
```javascript
function storeData() {
  const data = {
    language: document.getElementById('language').value,
    country: document.getElementById('country').value,
    name: document.getElementById('name').value,
    // ... collect all form data
  };
  
  localStorage.setItem('userData', JSON.stringify(data));
  window.location.href = 'guess.html';
}
```
**What it does:**
- **Function** that runs when form is submitted
- Collects all form data into a JavaScript **object**
- `localStorage.setItem()` saves data in the browser's memory
- `JSON.stringify()` converts the object to text for storage
- `window.location.href` redirects to the guessing game page

---

## 🎮 **GUESS.HTML - Game Page**

### 1. **Game Interface Structure**
```html
<div class="game-card p-4">
  <div id="progress-container" class="mb-4">
    <div class="d-flex justify-content-between align-items-center mb-2">
      <h5 id="progress-title" class="mb-0">Progress</h5>
      <span id="progress-text" class="fw-bold">0 / 0</span>
    </div>
    <div class="progress progress-custom">
      <div id="progress-bar" class="progress-bar progress-bar-custom"></div>
    </div>
  </div>
</div>
```
**What it does:**
- Creates the visual structure for the game
- **Progress bar** shows how many words completed
- Bootstrap classes handle spacing and alignment
- `id` attributes allow JavaScript to find and update these elements

### 2. **JavaScript - Global Variables**
```javascript
let words = [];
let currentIndex = 0;
let userData = null;
let displayTime = 1500;
let wordResults = [];
let isShowingWord = false;
```
**What it does:**
- **Variables** that store game state
- `words[]` - array of words to guess
- `currentIndex` - which word we're currently on
- `userData` - information from the form
- `displayTime` - how long to show each word
- `wordResults[]` - stores results of each guess

### 3. **JavaScript - Loading User Data**
```javascript
function loadUserData() {
  try {
    const storedData = localStorage.getItem('userData');
    
    if (!storedData) {
      alert('No user data found. Please fill out the form first.');
      window.location.href = 'index.html';
      return false;
    }
    
    userData = JSON.parse(storedData);
    return true;
  } catch (error) {
    console.error('Error loading user data:', error);
    return false;
  }
}
```
**What it does:**
- **Function** that retrieves data saved from the form
- `localStorage.getItem()` gets data from browser memory
- `JSON.parse()` converts text back to JavaScript object
- **Error handling** redirects back to form if data is missing
- `console.error()` logs errors for debugging

### 4. **JavaScript - Word Filtering**
```javascript
function filterMeaningfulWords(text) {
  const rawWords = text.match(/\b\w+\b/g) || [];
  
  const stopWords = new Set([
    'a', 'an', 'and', 'are', 'as', 'at', 'be', 'by', 'for', 'from'
    // ... many more common words
  ]);

  const meaningfulWords = rawWords
    .map(word => word.toLowerCase())
    .filter(word => 
      word.length > 3 && 
      !stopWords.has(word) &&
      /^[a-zA-ZÀ-ÿ]+$/.test(word)
    );

  return [...new Set(meaningfulWords)];
}
```
**What it does:**
- **Function** that finds important words in user's text
- `text.match(/\b\w+\b/g)` uses **regular expression** to find all words
- **Stop words** are common words like "the", "and" that we ignore
- `.filter()` removes short words, stop words, and non-letters
- `new Set()` removes duplicate words
- **Smart filtering** keeps only meaningful words for the game

### 5. **JavaScript - Dictionary Lookup**
```javascript
async function getDefinition(word, language) {
  try {
    const response = await fetch(`https://api.dictionaryapi.dev/api/v2/entries/${language}/${word}`);
    if (response.ok) {
      const data = await response.json();
      if (data[0]?.meanings?.[0]?.definitions?.[0]?.definition) {
        return {
          definition: data[0].meanings[0].definitions[0].definition,
          partOfSpeech: data[0].meanings[0].partOfSpeech || '',
          source: 'Dictionary API'
        };
      }
    }
  } catch (error) {
    console.log('Dictionary API failed:', error);
  }
  
  return {
    definition: language === 'fr' ? 'Définition non disponible' : 'Definition not available',
    partOfSpeech: '',
    source: 'Fallback'
  };
}
```
**What it does:**
- **Async function** that looks up word definitions online
- Uses **Dictionary API** to get real definitions
- **Language-aware** - gets French definitions for French words
- **Error handling** provides fallback if API fails
- Returns **object** with definition, part of speech, and source

### 6. **JavaScript - Game Logic**
```javascript
function showWord() {
  if (currentIndex >= words.length) {
    showResults();
    return;
  }
  
  const flashDiv = document.getElementById('flash');
  flashDiv.textContent = words[currentIndex];
  
  setTimeout(() => {
    flashDiv.innerHTML = '<i class="bi bi-question-circle question-mark"></i>';
  }, displayTime);
}
```
**What it does:**
- **Function** that displays each word
- Checks if game is finished (all words shown)
- Updates the flash area with current word
- `setTimeout()` waits, then shows question mark animation
- **Timing** depends on user's confidence level

### 7. **JavaScript - Checking Guesses**
```javascript
async function checkGuess() {
  const userInput = document.getElementById('guess').value.trim().toLowerCase();
  const correctWord = words[currentIndex].toLowerCase();
  
  if (userInput === correctWord) {
    // CORRECT GUESS
    wordResults.push({ 
      word: correctWord, 
      status: 'OK', 
      userGuess: userInput,
      definition: '' 
    });
    
    feedbackDiv.innerHTML = `<div class="alert alert-success">Correct!</div>`;
    
    // Auto-advance after 2 seconds
    setTimeout(() => {
      clearFeedbackAndShowNextWord();
    }, 2000);
    
  } else {
    // WRONG GUESS
    const definitionData = await getDefinition(correctWord, userData.language);
    
    wordResults.push({ 
      word: correctWord, 
      status: 'NOT OK', 
      userGuess: userInput,
      definition: definitionData.definition 
    });
    
    // Show definition and Next button
    feedbackDiv.innerHTML = `Wrong! The word was: ${correctWord}. Definition: ${definitionData.definition}`;
    nextBtn.style.display = 'inline-block';
  }
}
```
**What it does:**
- **Function** that processes user's guess
- Compares user input with correct word (case-insensitive)
- **If correct:** Shows success message, auto-advances to next word
- **If wrong:** Gets definition from dictionary, shows Next button
- **Different behavior** for right vs wrong answers
- Stores results for final summary

### 8. **JavaScript - Results Display**
```javascript
function showResults() {
  document.getElementById('results-container').style.display = 'block';
  
  const tableBody = document.getElementById('results-table-body');
  
  wordResults.forEach((result, index) => {
    const row = document.createElement('tr');
    row.className = result.status === 'OK' ? 'table-row-correct' : 'table-row-wrong';
    
    row.innerHTML = `
      <th scope="row">${index + 1}</th>
      <td><strong>${result.word}</strong></td>
      <td>${result.status}</td>
      <td><em>${result.definition}</em></td>
    `;
    
    tableBody.appendChild(row);
  });
  
  // Calculate statistics
  const correctCount = wordResults.filter(r => r.status === 'OK').length;
  const percentage = Math.round((correctCount / wordResults.length) * 100);
}
```
**What it does:**
- **Function** that shows final results table
- `forEach()` loops through all word results
- `createElement()` creates new HTML table rows
- **Dynamic styling** - correct answers green, wrong ones red
- **Statistics calculation** shows percentage of correct answers
- **DOM manipulation** adds content to the page

### 9. **JavaScript - Event Listeners**
```javascript
document.getElementById('guess').addEventListener('keypress', function(e) {
  if (e.key === 'Enter' && !this.disabled) {
    checkGuess();
  }
});
```
**What it does:**
- **Event listener** responds to user actions
- Listens for **Enter key** press in the input field
- Only works if input is not disabled
- Calls `checkGuess()` function
- **User experience** - can submit guess by pressing Enter

### 10. **JavaScript - Game Initialization**
```javascript
if (loadUserData()) {
  console.log('User data loaded successfully');
  updateLanguage();
  initializeWords();
  updateProgress();
  showWord();
} else {
  console.error('Failed to load user data');
}
```
**What it does:**
- **Main execution** that starts the game
- Loads user data from previous page
- Sets up the language
- Processes user's text to extract words
- Shows the first word
- **Error handling** for missing data

---

## 🔑 **Key Programming Concepts Explained**

### **Variables**
```javascript
let words = [];           // Array (list) of words
let currentIndex = 0;     // Number
let userData = null;      // Object or null
```

### **Functions**
```javascript
function doSomething() {  // Regular function
  // code here
}

async function getData() { // Async function (can wait)
  // code here
}
```

### **Objects**
```javascript
const person = {
  name: "John",
  age: 25,
  speak: function() { console.log("Hello"); }
};
```

### **Arrays**
```javascript
const fruits = ["apple", "banana", "orange"];
fruits.push("grape");      // Add item
fruits.filter(f => f.length > 5); // Filter items
```

### **DOM Manipulation**
```javascript
document.getElementById('myId');           // Find element
element.textContent = "New text";         // Change text
element.style.display = 'none';           // Hide element
element.addEventListener('click', func);   // Listen for clicks
```

### **Async/Await**
```javascript
async function getData() {
  const response = await fetch('https://api.com/data');
  const data = await response.json();
  return data;
}
```

### **Error Handling**
```javascript
try {
  // Code that might fail
  const result = riskyOperation();
} catch (error) {
  // Handle the error
  console.error('Something went wrong:', error);
}
```

---

## 💡 **Tips for Understanding the Code**

1. **Read top to bottom** - HTML loads in order
2. **Follow the data flow** - Form → localStorage → Game
3. **Trace user actions** - Click button → Run function → Update display
4. **Use browser dev tools** - F12 to see console logs and errors
5. **Experiment** - Change values and see what happens
6. **Break it down** - Understand one function at a time

The code combines **HTML structure**, **CSS styling**, and **JavaScript logic** to create an interactive web application that processes user input, calls external APIs, and provides a dynamic gaming experience!
