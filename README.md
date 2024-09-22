<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Interactivo</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .quiz-container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 300px;
        }
        h1 {
            text-align: center;
        }
        .question {
            margin-bottom: 15px;
        }
        .options button {
            display: block;
            margin: 5px 0;
            padding: 10px;
            width: 100%;
            border: none;
            border-radius: 4px;
            background-color: #007BFF;
            color: white;
            cursor: pointer;
            font-size: 16px;
        }
        .options button:hover {
            background-color: #0056b3;
        }
        .result {
            display: none;
            text-align: center;
            font-weight: bold;
        }
    </style>
</head>
<body>

<div class="quiz-container">
    <h1>Quiz Interactivo</h1>
    <div id="quiz">
        <div class="question" id="question">Pregunta aquí...</div>
        <div class="options">
            <button id="btnA">Opción A</button>
            <button id="btnB">Opción B</button>
            <button id="btnC">Opción C</button>
        </div>
    </div>
    <div class="result" id="result"></div>
</div>

<script>
    const questions = [
        {
            question: "¿Cuál es tu actividad favorita para relajarte?",
            options: { a: "Leer un libro", b: "Ver una película", c: "Salir a caminar" }
        },
        {
            question: "¿Cómo te describirías en una palabra?",
            options: { a: "Creativo", b: "Lógico", c: "Sociable" }
        },
        {
            question: "Si pudieras viajar a cualquier lugar, ¿a dónde irías?",
            options: { a: "Una ciudad histórica", b: "La naturaleza", c: "Una playa tropical" }
        },
        {
            question: "¿Cuál es tu bebida preferida?",
            options: { a: "Café", b: "Té", c: "Jugo natural" }
        },
        {
            question: "¿Qué tipo de arte disfrutas más?",
            options: { a: "Pintura", b: "Música", c: "Cine" }
        },
        {
            question: "¿Cómo manejas el estrés?",
            options: { a: "Reflexionando en silencio", b: "Haciendo ejercicio", c: "Hablando con amigos" }
        }
    ];

    // Resultados asociados a rangos de puntaje
    const results = [
        { range: [6, 6], result: "Eres una persona reflexiva y creativa." },
        { range: [7, 7], result: "Tienes una mente lógica aunque con toques creativos." },
        { range: [8, 8], result: "Piensas mucho en esos pequeños momentos que hacen magia." },
        { range: [9, 9], result: "Te caracteriza tu unica energia y una profunda conexión con la naturaleza." },
        { range: [10, 10], result: "Eres curioso y te encanta aprender cosas nuevas." },
        { range: [11, 11], result: "Eres muy intuitivo y sensible." },
        { range: [12, 12], result: "Tienes una actitud aventurera ." },
        { range: [13, 13], result: "Eres pragmático y resuelto." },
        { range: [14, 14], result: "Eres muy sociable y carismático." },
        { range: [15, 15], result: "Tienes una gran paz interior." },
        { range: [16, 16], result: "Eres introspectivo y filosófico." },
        { range: [17, 17], result: "Eres una persona muy extrovertida ." }
    ];

    let currentQuestionIndex = 0;
    let score = 0;

    // Mostrar la primera pregunta
    function showQuestion() {
        const questionElement = document.getElementById('question');
        const btnA = document.getElementById('btnA');
        const btnB = document.getElementById('btnB');
        const btnC = document.getElementById('btnC');

        const currentQuestion = questions[currentQuestionIndex];
        questionElement.textContent = currentQuestion.question;
        btnA.textContent = currentQuestion.options.a;
        btnB.textContent = currentQuestion.options.b;
        btnC.textContent = currentQuestion.options.c;
    }

    async function handleAnswer(option) {
        if (option === 'a') {
            score += 1;
        } else if (option === 'b') {
            score += 2;
        } else if (option === 'c') {
            score += 3;
        }

        currentQuestionIndex++;
        if (currentQuestionIndex < questions.length) {
            showQuestion();
        } else {
            showResult();
        }
    }

    function showResult() {
        const quizElement = document.getElementById('quiz');
        const resultElement = document.getElementById('result');

        quizElement.style.display = 'none';
        resultElement.style.display = 'block';

        // Encontrar el resultado basado en el puntaje
        const finalResult = results.find(r => score >= r.range[0] && score <= r.range[1]);
        if (finalResult) {
            resultElement.textContent = finalResult.result;
        } else {
            resultElement.textContent = "No se encontró un resultado para tu puntaje.";
        }
    }

    document.getElementById('btnA').addEventListener('click', () => handleAnswer('a'));
    document.getElementById('btnB').addEventListener('click', () => handleAnswer('b'));
    document.getElementById('btnC').addEventListener('click', () => handleAnswer('c'));

    // Mostrar la primera pregunta al cargar la página
    showQuestion();
</script>

</body>
</html>
