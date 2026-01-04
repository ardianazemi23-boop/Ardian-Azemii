let questions = {
  easy: [
    {
      q: "Who is the national hero of Albania?",
      a: ["Napoleon", "Skanderbeg", "Julius Caesar", "Alexander the Great"],
      correct: 1,
      info: "Skanderbeg led Albanian resistance in the 15th century."
    }
  ],
  medium: [
    {
      q: "In which century did Skanderbeg live?",
      a: ["13th", "14th", "15th", "16th"],
      correct: 2,
      info: "Skanderbeg lived during the 15th century."
    }
  ],
  hard: [
    {
      q: "Which battle started Skanderbeg’s rebellion?",
      a: ["Battle of Kosovo", "Battle of Torvioll", "Battle of Varna", "Battle of Lepanto"],
      correct: 1,
      info: "The Battle of Torvioll in 1444."
    }
  ]
};

let currentLevel = "";
let currentQuestion = 0;

function startGame(level) {
  currentLevel = level;
  currentQuestion = 0;
  document.getElementById("level-select").classList.add("hidden");
  document.getElementById("game").classList.remove("hidden");
  loadQuestion();
}

function loadQuestion() {
  let q = questions[currentLevel][currentQuestion];
  document.getElementById("question").innerText = q.q;

  q.a.forEach((answer, i) => {
    document.getElementById("a" + i).innerText = answer;
  });

  document.getElementById("result").innerText = "";
  document.getElementById("nextBtn").classList.add("hidden");
}

function checkAnswer(index) {
  let q = questions[currentLevel][currentQuestion];
  let result = document.getElementById("result");

  if (index === q.correct) {
    result.innerText = "✅ Correct! " + q.info;
  } else {
    result.innerText = "❌ Wrong. Correct answer: " + q.a[q.correct] + ". " + q.info;
  }

  document.getElementById("nextBtn").classList.remove("hidden");
}

function nextQuestion() {
  currentQuestion++;

  if (currentQuestion >= questions[currentLevel].length) {
    document.getElementById("game").innerHTML =
      "<h2>🎉 Level Finished!</h2><button onclick='location.reload()'>Home</button>";
  } else {
    loadQuestion();
  }
}
