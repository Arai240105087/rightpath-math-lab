# rightpath-math-lab
Differentiated learning website for the Pythagorean theorem
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>RightPath Math Lab</title>
  <style>
    :root {
      --blue: #2457d6;
      --dark: #172554;
      --light: #eff6ff;
      --green: #15803d;
      --border: #dbe4f0;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f5f8ff;
      color: #1e293b;
      line-height: 1.6;
    }

    header {
      background: linear-gradient(135deg, #173a8a, #3978ef);
      color: white;
      text-align: center;
      padding: 42px 18px;
    }

    header h1 {
      font-size: clamp(2rem, 5vw, 3rem);
      margin: 0 0 8px;
    }

    header p {
      margin: 0 auto;
      max-width: 650px;
    }

    main {
      width: min(900px, 92%);
      margin: 28px auto;
    }

    .card {
      background: white;
      padding: 24px;
      margin-bottom: 20px;
      border: 1px solid var(--border);
      border-radius: 18px;
      box-shadow: 0 5px 20px #1725540b;
    }

    h2 {
      color: var(--dark);
      margin-top: 0;
    }

    .formula {
      background: var(--light);
      color: var(--blue);
      text-align: center;
      font-size: 1.6rem;
      font-weight: bold;
      border-radius: 12px;
      padding: 16px;
      margin: 18px 0;
    }

    .levels {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin: 18px 0;
    }

    button {
      border: 0;
      border-radius: 10px;
      padding: 12px 15px;
      font-size: 1rem;
      font-weight: bold;
      cursor: pointer;
    }

    button:focus-visible,
    input:focus-visible {
      outline: 3px solid #93c5fd;
      outline-offset: 3px;
    }

    .level-btn {
      background: #e8efff;
      color: #2447a5;
      border: 2px solid transparent;
    }

    .level-btn.active {
      background: var(--blue);
      color: white;
    }

    .action {
      background: var(--blue);
      color: white;
      margin: 5px 5px 5px 0;
    }

    .secondary {
      background: #e8efff;
      color: #2447a5;
      margin: 5px 5px 5px 0;
    }

    .problem {
      background: #f8fafc;
      border-left: 4px solid var(--blue);
      padding: 16px;
      border-radius: 8px;
      margin: 18px 0;
    }

    input {
      width: 100%;
      max-width: 300px;
      padding: 12px;
      border: 1px solid #94a3b8;
      border-radius: 9px;
      font-size: 1rem;
      margin: 8px 0;
    }

    .feedback {
      padding: 12px;
      border-radius: 9px;
      margin-top: 12px;
    }

    .success {
      background: #dcfce7;
      color: #166534;
    }

    .error {
      background: #fee2e2;
      color: #991b1b;
    }

    .hint-box,
    .solution-box {
      background: #f0f7ff;
      border-radius: 10px;
      padding: 15px;
      margin-top: 14px;
    }

    .hidden {
      display: none;
    }

    .tag {
      display: inline-block;
      background: #dbeafe;
      color: #1d4ed8;
      padding: 4px 10px;
      border-radius: 20px;
      font-size: 0.85rem;
      font-weight: bold;
    }

    footer {
      text-align: center;
      padding: 24px;
      color: #64748b;
      font-size: 0.9rem;
    }

    @media (max-width: 520px) {
      .levels {
        grid-template-columns: 1fr;
      }

      .card {
        padding: 18px;
      }
    }
  </style>
</head>

<body>
  <header>
    <h1>RightPath Math Lab</h1>
    <p>Learn mathematics at your own pace with personalized practice,
      helpful hints, and step-by-step solutions.</p>
  </header>

  <main>
    <section class="card">
      <span class="tag">Differentiated Learning</span>
      <h2>Welcome, Math Explorer!</h2>
      <p>
        Every student learns differently. Choose a level that matches
        your current skills and practise the Pythagorean theorem.
      </p>
      <div class="formula">a² + b² = c²</div>
      <p>
        In a right triangle, <strong>a</strong> and <strong>b</strong>
        are the two shorter sides, and <strong>c</strong> is the
        hypotenuse, the longest side opposite the right angle.
      </p>
    </section>

    <section class="card">
      <h2>Choose Your Learning Level</h2>
      <div class="levels">
        <button class="level-btn active" data-level="0">
          Foundation
        </button>
        <button class="level-btn" data-level="1">
          Standard
        </button>
        <button class="level-btn" data-level="2">
          Advanced
        </button>
      </div>

      <p id="levelDescription"></p>
      <div class="problem">
        <h3 id="problemTitle"></h3>
        <p id="problemText"></p>
        <p><strong id="question"></strong></p>
      </div>

      <label for="answer"><strong>Your answer:</strong></label><br>
      <input id="answer" type="number" step="any"
        placeholder="Enter your answer">
      <p id="unit"></p>

      <div>
        <button class="action" id="checkBtn">Check Answer</button>
        <button class="secondary" id="hintBtn">Show Hint</button>
        <button class="secondary" id="solutionBtn">Show Solution</button>
        <button class="secondary" id="newBtn">New Practice</button>
      </div>

      <div id="feedback" class="feedback hidden"
        aria-live="polite"></div>
      <div id="hint" class="hint-box hidden" aria-live="polite"></div>
      <div id="solution" class="solution-box hidden"
        aria-live="polite"></div>
    </section>

    <section class="card">
      <h2>How Does Differentiated Learning Help?</h2>
      <ul>
        <li><strong>Foundation:</strong> Simple numbers and guided hints
          help beginners understand the formula.</li>
        <li><strong>Standard:</strong> Students practise applying the
          formula independently.</li>
        <li><strong>Advanced:</strong> A real-world problem encourages
          reasoning and problem-solving.</li>
      </ul>
      <p>
        Students can choose a suitable challenge, receive immediate
        feedback, and review worked solutions when needed.
      </p>
    </section>

    <section class="card">
      <h2>About This Project</h2>
      <p>
        RightPath Math Lab is an educational technology prototype
        demonstrating differentiated mathematics practice. Its
        predefined exercises, hints, and answer checking run in the
        browser. A live AI model is not connected in this version.
      </p>
    </section>
  </main>

  <footer>
    RightPath Math Lab · Educational Technology &amp; AI Project
  </footer>

  <script>
    const problems = [
      {
        name: "Foundation Level",
        description: "Start with small numbers and guided steps.",
        title: "Find the hypotenuse",
        text: "A right triangle has two shorter sides of 3 cm and 4 cm.",
        question: "What is the length of the hypotenuse?",
        a: 3, b: 4, answer: 5, unit: "cm",
        hint: "First, square both sides: 3² = 9 and 4² = 16. Then add the results.",
        solution: "Use a² + b² = c². Then 3² + 4² = c², so 9 + 16 = 25. Therefore c = √25 = 5 cm."
      },
      {
        name: "Standard Level",
        description: "Apply the formula with larger numbers.",
        title: "Calculate the hypotenuse",
        text: "A right triangle has legs measuring 6 cm and 8 cm.",
        question: "Find the hypotenuse in centimetres.",
        a: 6, b: 8, answer: 10, unit: "cm",
        hint: "Square 6 and 8, add the squares, and find the square root of the sum.",
        solution: "6² + 8² = c². Therefore 36 + 64 = 100, so c = √100 = 10 cm."
      },
      {
        name: "Advanced Level",
        description: "Use the theorem in a real-world situation.",
        title: "The ladder problem",
        text: "A 13 m ladder leans against a wall. Its base is 5 m from the wall.",
        question: "How high up the wall does the ladder reach? Enter the height in metres.",
        a: 5, b: 12, answer: 12, unit: "m",
        hint: "The ladder is the hypotenuse. Rearrange the formula: height² = 13² − 5².",
        solution: "Let h be the height. Since 13 m is the hypotenuse, h² + 5² = 13². Thus h² = 169 − 25 = 144, and h = √144 = 12 m."
      }
    ];

    let currentLevel = 0;
    let practiceIndex = 0;

    const levelButtons = document.querySelectorAll(".level-btn");
    const description = document.getElementById("levelDescription");
    const title = document.getElementById("problemTitle");
    const problemText = document.getElementById("problemText");
    const question = document.getElementById("question");
    const answerInput = document.getElementById("answer");
    const unit = document.getElementById("unit");
    const feedback = document.getElementById("feedback");
    const hintBox = document.getElementById("hint");
    const solutionBox = document.getElementById("solution");

    function currentProblem() {
      return problems[currentLevel];
    }

    function renderProblem() {
      const p = currentProblem();

      levelButtons.forEach((button, index) => {
        button.classList.toggle("active", index === currentLevel);
        button.setAttribute("aria-pressed", index === currentLevel);
      });

      description.textContent = p.description;
      title.textContent = p.title +
        (practiceIndex ? " — Practice " + (practiceIndex + 1) : "");
      problemText.textContent = p.text;
      question.textContent = p.question;
      unit.textContent = "Expected unit: " + p.unit;

      answerInput.value = "";
      feedback.className = "feedback hidden";
      hintBox.classList.add("hidden");
      solutionBox.classList.add("hidden");
    }

    levelButtons.forEach(button => {
      button.addEventListener("click", () => {
        currentLevel = Number(button.dataset.level);
        practiceIndex = 0;
        renderProblem();
      });
    });

    document.getElementById("checkBtn").addEventListener("click", () => {
      const p = currentProblem();
      const value = Number(answerInput.value);

      feedback.className = "feedback";
      feedback.classList.remove("hidden");

      if (answerInput.value.trim() === "" || !Number.isFinite(value)) {
        feedback.classList.add("error");
        feedback.textContent = "Please enter a numerical answer first.";
        return;
      }

      if (Math.abs(value - p.answer) < 0.01) {
        feedback.classList.add("success");
        feedback.textContent = "Correct! Great work. Your answer is " +
          p.answer + " " + p.unit + ".";
      } else {
        feedback.classList.add("error");
        feedback.textContent = "Not quite. Check your calculations or use a hint and try again.";
      }
    });

    document.getElementById("hintBtn").addEventListener("click", () => {
      hintBox.textContent = "Hint: " + currentProblem().hint;
      hintBox.classList.remove("hidden");
    });

    document.getElementById("solutionBtn").addEventListener("click", () => {
      solutionBox.textContent = "Solution: " + currentProblem().solution;
      solutionBox.classList.remove("hidden");
    });

    document.getElementById("newBtn").addEventListener("click", () => {
      practiceIndex++;
      renderProblem();
    });

    renderProblem();
  </script>
</body>
</html>
