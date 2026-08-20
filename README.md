# codealpha_tasks
code alpha's tasks
Features:
Enter text to translate.
Select source language.
Select target language.
Translate text using an API.
Project Structure:
language-translator/
│── index.html
│── style.css
│── script.js<!DOCTYPE html>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Language Translation Tool</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div class="container">

    <h2>🌐 Language Translation Tool</h2>

    <textarea id="inputText" placeholder="Enter text here..."></textarea>

    <div class="languages">

        <select id="sourceLang">
            <option value="en">English</option>
            <option value="hi">Hindi</option>
            <option value="fr">French</option>
            <option value="es">Spanish</option>
            <option value="de">German</option>
        </select>

        <span>➡</span>

        <select id="targetLang">
            <option value="hi">Hindi</option>
            <option value="en">English</option>
            <option value="fr">French</option>
            <option value="es">Spanish</option>
            <option value="de">German</option>
        </select>

    </div>

    <button onclick="translateText()">Translate</button>

    <h3>Translated Text</h3>

    <textarea id="outputText" readonly></textarea>

    <div class="buttons">
        <button onclick="copyText()">Copy</button>
        <button onclick="speakText()">🔊 Speak</button>
    </div>

</div>

<script src="script.js"></script>

</body>
</html>
body{
    font-family: Arial;
    background:#f4f4f4;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}

.container{
    width:500px;
    background:white;
    padding:20px;
    border-radius:10px;
    box-shadow:0 0 10px gray;
}

textarea{
    width:100%;
    height:120px;
    margin:10px 0;
    padding:10px;
    resize:none;
}

.languages{
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin:10px 0;
}

select{
    width:180px;
    padding:8px;
}

button{
    padding:10px 20px;
    background:#007bff;
    color:white;
    border:none;
    cursor:pointer;
    margin:5px;
}

button:hover{
    background:#0056b3;
}

.buttons{
    display:flex;
    justify-content:space-between;
}
Replace "YOUR_API_KEY" with your Google Cloud Translation API key.
async function translateText() {

    const text = document.getElementById("inputText").value;
    const source = document.getElementById("sourceLang").value;
    const target = document.getElementById("targetLang").value;

    const url =
    `https://translation.googleapis.com/language/translate/v2?key=YOUR_API_KEY`;

    const response = await fetch(url,{
        method:"POST",
        headers:{
            "Content-Type":"application/json"
        },
        body:JSON.stringify({
            q:text,
            source:source,
            target:target,
            format:"text"
        })
    });

    const data = await response.json();

    document.getElementById("outputText").value =
    data.data.translations[0].translatedText;

}
function copyText(){

    const output=document.getElementById("outputText");

    output.select();

    document.execCommand("copy");

    alert("Copied!");
}
function speakText(){

    const text=document.getElementById("outputText").value;

    const speech=new SpeechSynthesisUtterance(text);

    speech.lang=document.getElementById("targetLang").value;

    window.speechSynthesis.speak(speech);

}
Sample Output

Input

Hello, how are you?

Source Language

English

Target Language

Hindi

Output

नमस्ते, आप कैसे हैं?
