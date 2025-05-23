
# Interactive Word Flash Game

This web application helps users reflect on their personal struggles and explore the deeper meaning of the words they use. It consists of two HTML pages:

## 🔹 index.html (Form Page)
- Collects user details: Name, Age, Sex, Country, Language, Confidence Level, and a text describing their current struggle.
- Saves the data to localStorage.
- Redirects the user to the guessing game page (`guess.html`).

## 🔹 guess.html (Guessing Game)
- Extracts important words from the user's text.
- Shows each word briefly depending on confidence level:
  - Low: 3 seconds
  - Medium: 1.5 seconds
  - High: 0.5 seconds
- Prompts the user to type the word they saw.
- If the user is wrong, a dictionary definition of the word is fetched from [dictionaryapi.dev](https://dictionaryapi.dev).
- Provides speech synthesis for feedback and a final summary.

## 🛠 How to Use
1. Open `index.html` in your browser.
2. Fill out the form and click Submit.
3. You'll be redirected to `guess.html` to start the word recognition game.

## 🚀 Deployment
You can host these files on GitHub Pages, Netlify, or any static hosting provider.

## 📁 Files
- `index.html` — User form and data collection.
- `guess.html` — Flashing word game.
- `README.md` — This documentation.

Enjoy discovering the power of your own words.
