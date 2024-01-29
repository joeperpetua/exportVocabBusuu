## Export / Extract Vocabulary from Busuu Website in JSON
### Steps:
- Go to Review page: https://www.busuu.com/dashboard#/review
- Open browser console (Ctrl + Shift + J)
- Copy/Paste and Run one of the following code in the browser console:

``` javascript
// Function to extract and export vocabulary data (supposed to be more performent)
function extractVocabularyDataMethodOne() {
    const vocabularyData = [];

    // Select all vocabulary list rows
    const vocabularyRows = document.querySelectorAll('.vocab-list-row');

    // Loop through each vocabulary row
    vocabularyRows.forEach(row => {
        const wordData = {};

        // Extract word text and translation
        const wordText = row.querySelector('.vocab-list-row__course-language .font-face-lt').textContent.trim();
        const translation = row.querySelector('.vocab-list-row__interface-language').textContent.trim();

        // Extract strength indicator
        const strengthIcon = row.querySelector('.vocab-strength-indicator__icon svg');
        const strength = strengthIcon.getAttribute('fill');
		
        // Add extracted data to wordData object
        wordData.wordText = wordText;
        wordData.translation = translation;
        wordData.strength = strength;

        // Check if the row has an example sentence element
        const hasExampleSentence = row.classList.contains('vocab-list-row--keyphrase');

        if (hasExampleSentence) {
            // Extract example sentence and translation
            const exampleSentence = row.querySelector('.vocab-list-row__keyphrase-course .font-face-lt').textContent.trim();
            const exampleTranslation = row.querySelector('.vocab-list-row__keyphrase-interface').textContent.trim();

            // Add example sentence and translation to wordData object
            wordData.exampleSentence = exampleSentence;
            wordData.exampleTranslation = exampleTranslation;
        } else {
            // If no example sentence, set to empty string
            wordData.exampleSentence = '';
            wordData.exampleTranslation = '';
        }

        // Push wordData object to vocabularyData array
        vocabularyData.push(wordData);
    });

    // Convert vocabularyData to JSON
    const jsonData = JSON.stringify(vocabularyData);

    // Export JSON data
    const blob = new Blob([jsonData], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'vocabulary_data.json';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
}

// Call the function to extract and export vocabulary data
extractVocabularyDataMethodOne();
```
``` javascript
// Function to extract and export vocabulary data
function extractVocabularyDataMethodTwo() {
    const vocabularyData = [];

    // Select all vocabulary list rows
    const vocabularyRows = document.querySelectorAll('.vocab-list-row');

    // Loop through each vocabulary row
    vocabularyRows.forEach(row => {
        const wordData = {};

        // Extract word text and translation
        const wordText = row.querySelector('.vocab-list-row__course-language .font-face-lt').textContent.trim();
        const translation = row.querySelector('.vocab-list-row__interface-language').textContent.trim();

        // Extract strength indicator
        const strengthIcon = row.querySelector('.vocab-strength-indicator__icon svg');
        const strength = strengthIcon.getAttribute('fill');

        // Add extracted data to wordData object so far
        wordData.wordText = wordText;
        wordData.translation = translation;
        wordData.strength = strength;

        // Extract example sentence if it exists
        const exampleSentenceElement = row.querySelector('.vocab-list-row__keyphrase-course .font-face-lt');
        const exampleTranslationElement = row.querySelector('.vocab-list-row__keyphrase-interface');
		
        if (exampleSentenceElement && exampleTranslationElement) {
            const exampleSentence = exampleSentenceElement.textContent.trim();
            const exampleTranslation = exampleTranslationElement.textContent.trim();

            // Add example sentence and translation to wordData object
            wordData.exampleSentence = exampleSentence;
            wordData.exampleTranslation = exampleTranslation;
        } else {
            // If example sentence doesn't exist, set to empty string
            wordData.exampleSentence = '';
            wordData.exampleTranslation = '';
        }

        // Push wordData object to vocabularyData array
        vocabularyData.push(wordData);
    });

    // Convert vocabularyData to JSON
    const jsonData = JSON.stringify(vocabularyData);

    // Export JSON data
    const blob = new Blob([jsonData], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = 'vocabulary_data.json';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
}

// Call the function to extract and export vocabulary data
extractVocabularyDataMethodTwo();
```
- Wait for the download
