<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Geography Quiz</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f8ff;
      padding: 20px;
    }
    .quiz-container {
      max-width: 700px;
      margin: auto;
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 0 10px #aaa;
    }
    .question {
      font-size: 18px;
      font-weight: bold;
    }
    .options {
      margin-top: 15px;
    }
    .option {
      display: block;
      margin: 10px 0;
      padding: 10px;
      background: #eee;
      border-radius: 5px;
      cursor: pointer;
    }
    .option.correct {
      background-color: #c8e6c9;
    }
    .option.wrong {
      background-color: #ffcdd2;
    }
    .navigation {
      margin-top: 20px;
      text-align: center;
    }
    button {
      padding: 10px 20px;
      margin: 5px;
      font-size: 16px;
      cursor: pointer;
    }
    #score {
      font-size: 20px;
      font-weight: bold;
      text-align: center;
      margin-top: 30px;
    }
  </style>
</head>
<body>
<div class="quiz-container">
  <div id="quiz">
    <div class="question" id="question"></div>
    <div class="options" id="options"></div>
    <div class="navigation">
      <button onclick="prevQuestion()">Previous</button>
      <button onclick="nextQuestion()">Next</button>
    </div>
    <div id="score"></div>
  </div>
</div>

<script>
const quizData = [
  { q: "What percentage of the Earth’s surface is covered by land?", a: "29%", options: ["29%", "31%", "50%", "22%"] },
  { q: "What percentage of the Earth’s surface is covered by water?", a: "71%", options: ["51%", "62%", "71%", "80%"] },
  { q: "Which is the third largest country in the world by area?", a: "United States of America", options: ["India", "China", "Russia", "United States of America"] },
  { q: "What percentage of the world’s population resides in India?", a: "17.5%", options: ["10%", "15%", "17.5%", "20%"] },
  { q: "Which is the most populous country in the world?", a: "China", options: ["India", "USA", "China", "Indonesia"] },
  { q: "Which country is the largest in the world by area?", a: "Russia", options: ["USA", "Russia", "China", "Brazil"] },
  { q: "What is the total area of India?", a: "32.87 lakh sq km", options: ["31 lakh sq km", "32.87 lakh sq km", "33 lakh sq km", "34.5 lakh sq km"] },
  { q: "What is the position of India in the world by population?", a: "Second", options: ["First", "Third", "Second", "Fourth"] },
  { q: "What is the latitudinal and longitudinal extent of India?", a: "8°4′ N to 37°6′ N latitude and 68°7′ E to 97°25′ E longitude", options: [
      "7° N to 37° N and 66° E to 98° E", 
      "8°4′ N to 37°6′ N latitude and 68°7′ E to 97°25′ E longitude", 
      "10° N to 40° N and 60° E to 100° E", 
      "9° N to 36° N and 65° E to 95° E"
    ] },
  { q: "What is the standard meridian of India?", a: "82°30′ E", options: ["80° E", "81°30′ E", "82°30′ E", "83° E"] },
  // ...continue same format till Q40

  // Example last question
  { q: "Which river flows between the Vindhya and Satpura ranges?", a: "Narmada", options: ["Godavari", "Krishna", "Mahanadi", "Narmada"] }
];

let current = 0;
let score = 0;

function loadQuestion() {
  const qBox = document.getElementById("question");
  const optBox = document.getElementById("options");
  const qData = quizData[current];
  qBox.innerText = `${current + 1}. ${qData.q}`;
  optBox.innerHTML = "";
  qData.options.forEach(option => {
    const btn = document.createElement("div");
    btn.className = "option";
    btn.innerText = option;
    btn.onclick = function () {
      if (btn.classList.contains("correct") || btn.classList.contains("wrong")) return;

      if (option === qData.a) {
        btn.classList.add("correct");
        score++;
      } else {
        btn.classList.add("wrong");
        // highlight correct one
        [...optBox.children].forEach(o => {
          if (o.innerText === qData.a) o.classList.add("correct");
        });
      }
    };
    optBox.appendChild(btn);
  });
}

function nextQuestion() {
  if (current < quizData.length - 1) {
    current++;
    loadQuestion();
  } else {
    document.getElementById("score").innerText = `Quiz Complete! Your Score: ${score}/${quizData.length}`;
  }
}

function prevQuestion() {
  if (current > 0) {
    current--;
    loadQuestion();
  }
}

window.onload = loadQuestion;
</script>
</body>
</html>
