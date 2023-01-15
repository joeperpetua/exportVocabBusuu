## Export / Extract Vocabulary from Busuu Website
### Steps:
- Go to Review page: https://www.busuu.com/dashboard#/review
- Mute the tab or the PC (when obtaining the audio links, they will be played out loud)
- Open browser console (Ctrl + Shift + J)
- Copy/Paste and Run the following code in the browser console:
```
const vocabList = document.querySelectorAll(".vocab-list-row");
let vocabToExport = [];

console.log("==========\nThis can take some time, depending on the amount of vocabulary there is to export, around 2 minutes for 700 entries for example.\n==========");

for(let i = 0; i < vocabList.length; i++){

    vocabList[i]?.childNodes[2]?.firstChild?.firstChild?.lastChild?.firstChild.click();
    vocabList[i]?.childNodes[6]?.firstChild?.lastChild?.click();

    const vocabText = vocabList[i]?.children[3]?.children[0]?.children[0]?.textContent;
    const vocabTranslation = vocabList[i]?.children[3]?.children[1]?.textContent;
    const vocabStrength = vocabList[i]?.children[4]?.children[1]?.textContent;
    const vocabExampleTranslated = vocabList[i]?.children[6]?.children[1]?.children[1]?.textContent;
    const vocabOriginalExample = vocabList[i]?.children[6]?.children[1]?.children[0]?.textContent;
    const vocabAudioURL = vocabList[i]?.childNodes[2]?.firstChild?.firstChild?.lastChild?.firstChild?.getAttribute("src");
    const vocabExampleAudioURL = vocabList[i]?.childNodes[6]?.firstChild?.lastChild?.firstChild?.lastChild?.firstChild?.getAttribute("src");

    vocabToExport.push({
        "text": vocabText,
        "translation": vocabTranslation,
        "strength": vocabStrength,
        "example_translated": vocabExampleTranslated,
        "example": vocabOriginalExample,
        "audio": vocabAudioURL,
        "example_audio": vocabExampleAudioURL
    });
    
    console.log("<--- Entries processed");
}
console.log("==========\nProcess finished, you can copy the following object:");
console.log(vocabToExport);
console.log("==========");
```
- Wait for the result to be logged in the console
- This error message is expected, wait until all the errors are logged before unmuting the tab / PC:

![image](https://user-images.githubusercontent.com/43834198/173247810-0c9538f3-a20a-4535-8efa-496686c7d042.png)

- Copy the logged object:

![image](https://user-images.githubusercontent.com/43834198/173247838-0907f8bc-c41e-4690-9ce7-9b207a742f19.png)

- Go to [JSON to CSV Converter](https://www.convertcsv.com/json-to-csv.htm) and paste the copied object
- Generate your Busuu vocabulary in CSV/xlsx format

That is pretty much all, you can do whatever you want with the CSV file (making an Anki deck for example).
If you have any issues with the script, please create an issue in the repository.
