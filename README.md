<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Online Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        .quiz-container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
            box-shadow: 2px 2px 12px rgba(0, 0, 0, 0.1);
        }
        .question {
            font-size: 20px;
        }
        .options {
            list-style: none;
            padding: 0;
        }
        .options li {
            margin: 10px 0;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h2>Online Quiz</h2>
        <div id="quiz"></div>
        <button onclick="submitQuiz()">Submit</button>
        <p id="result"></p>
    </div>

    <script>
        const quizData = [
            {
                question: "What is the capital of France?",
                options: ["Berlin", "Madrid", "Paris", "Lisbon"],
                answer: "Paris"
            },
            {
                question: "Which planet is known as the Red Planet?",
                options: ["Earth", "Mars", "Jupiter", "Saturn"],
                answer: "Mars"
            },
            {
                question: "What is 5 + 3?",
                options: ["5", "8", "10", "15"],
                answer: "8"
            }
        ];

        const quizContainer = document.getElementById("quiz");

        function loadQuiz() {
            quizData.forEach((q, index) => {
                const questionElement = document.createElement("div");
                questionElement.classList.add("question");
                questionElement.innerHTML = `<p>${index + 1}. ${q.question}</p>`;

                const optionsList = document.createElement("ul");
                optionsList.classList.add("options");

                q.options.forEach(option => {
                    const li = document.createElement("li");
                    li.innerHTML = `<label><input type="radio" name="question${index}" value="${option}"> ${option}</label>`;
                    optionsList.appendChild(li);
                });
                
                quizContainer.appendChild(questionElement);
                quizContainer.appendChild(optionsList);
            });
        }

        function submitQuiz() {
            let score = 0;
            quizData.forEach((q, index) => {
                const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
                if (selectedOption && selectedOption.value === q.answer) {
                    score++;
                }
            });
            document.getElementById("result").innerText = `You scored ${score} out of ${quizData.length}`;
        }

        loadQuiz();
    </script>
</body>
</html>
