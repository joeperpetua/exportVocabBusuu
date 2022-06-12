## Export / Extract Vocabulary from Busuu Website
### Steps:
- Go to Review page: https://www.busuu.com/dashboard#/review
- Mute the tab or the PC (when obtaining the audio links, they will be played out loud)
- Open browser console (Ctrl + Shift + J)
- Run following code in the broswer console:
```
const vocabList = document.querySelectorAll(".vocab-list-row.vocab-list-row--keyphrase");
let vocabToExport = [];

for(let i = 0; i < vocabList.length; i++){

    vocabList[i]?.childNodes[2]?.firstChild?.firstChild?.lastChild?.firstChild.click();
    vocabList[i]?.childNodes[6]?.firstChild?.lastChild?.click();

    const vocabText = vocabList[i]?.children[3]?.children[0]?.children[0]?.textContent;
    const vocabTranslation = vocabList[i]?.children[3]?.children[1]?.textContent;
    const vocabStrength = vocabList[i]?.children[4]?.children[1]?.textContent;
    const vocabExample = vocabList[i]?.children[6]?.children[1]?.children[1]?.textContent;
    const vocabAudioURL = vocabList[i]?.childNodes[2]?.firstChild?.firstChild?.lastChild?.firstChild?.getAttribute("src");
    const vocabExampleAudioURL = vocabList[i]?.childNodes[6]?.firstChild?.lastChild?.firstChild?.lastChild?.firstChild?.getAttribute("src");

    vocabToExport.push({
        "text": vocabText,
        "translation": vocabTranslation,
        "strength": vocabStrength,
        "example": vocabExample,
        "audio": vocabAudioURL,
        "example_audio": vocabExampleAudioURL
    });
}

console.log(vocabToExport);
```
- Wait for the result to be logged in the console
- This error message is expected, wait until all the errors are logged before unmuting the tab / PC:

![image](https://user-images.githubusercontent.com/43834198/173247810-0c9538f3-a20a-4535-8efa-496686c7d042.png)

- Copy the logged object:

![image](https://user-images.githubusercontent.com/43834198/173247838-0907f8bc-c41e-4690-9ce7-9b207a742f19.png)

- Go to [JSON to CSV Converter](https://www.convertcsv.com/json-to-csv.htm) and paste the copied object
- Generate your Busuu vocabulary in CSV format
