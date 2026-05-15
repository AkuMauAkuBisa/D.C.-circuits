<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>A-Level Physics: D.C. Circuits Quiz</title>
  <style>
    /* Theme & Base Layout */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: system-ui, -apple-system, sans-serif;
      background: #0d1117; color: #c9d1d9; line-height: 1.6;
      max-width: 800px; margin: 0 auto; padding: 20px;
    }
    header {
      text-align: center; margin-bottom: 30px; border-bottom: 2px solid #30363d; padding-bottom: 20px;
    }
    h1 { color: #f0f6fc; margin-bottom: 10px; }
    .subtitle { color: #58a6ff; font-weight: bold; }

    /* Quiz Container */
    .quiz-container { background: #161b22; border: 1px solid #21262d; border-radius: 8px; padding: 25px; }
    .question-card { display: none; }
    .question-card.active { display: block; }
    .question-text { font-size: 1.2rem; color: #f0f6fc; margin-bottom: 15px; font-weight: 600; }
    
    /* Options */
    .options-list { list-style: none; margin-bottom: 20px; }
    .option-item {
      background: #21262d; border: 1px solid #30363d; border-radius: 6px;
      padding: 12px 15px; margin-bottom: 10px; cursor: pointer; transition: background 0.2s;
    }
    .option-item:hover { background: #30363d; }
    .option-item.selected { border-color: #58a6ff; background: #1f2d3d; }
    
    /* Feedback Box */
    .feedback-box {
      display: none; padding: 15px; border-radius: 6px; margin-bottom: 20px; font-size: 0.95rem;
    }
    .feedback-box.correct { display: block; background: #1b4322; border: 1px solid #2ea043; color: #85ea93; }
    .feedback-box.incorrect { display: block; background: #4c1a1a; border: 1px solid #f85149; color: #ff9185; }
    .explanation-title { font-weight: bold; margin-top: 5px; color: #fff; }

    /* Buttons & Progress */
    .btn {
      background: #238636; color: white; border: 1px solid #2ea043; border-radius: 6px;
      padding: 10px 20px; font-size: 1rem; cursor: pointer; font-weight: bold;
    }
    .btn:hover { background: #2ea043; }
    .btn:disabled { background: #21262d; border-color: #30363d; color: #8b949e; cursor: not-allowed; }
    .controls { display: flex; justify-content: space-between; align-items: center; margin-top: 20px; }
    .progress-bar { height: 6px; background: #21262d; border-radius: 3px; margin-bottom: 20px; overflow: hidden; }
    .progress-fill { height: 100%; background: #58a6ff; width: 0%; transition: width 0.3s; }

    /* Results Screen */
    .results-screen { display: none; text-align: center; padding: 30px 0; }
    .score-text { font-size: 2rem; color: #58a6ff; font-weight: bold; margin: 15px 0; }
  </style>
</head>
<body>

  <header>
    <h1>⚡ D.C. Circuits Interactive Quiz</h1>
    <p class="subtitle">A-Level Physics Assessment</p>
  </header>

  <main class="quiz-container">
    <!-- Progress Bar -->
    <div class="progress-bar">
      <div id="progress-fill" class="progress-fill"></div>
    </div>

    <!-- Question Container -->
    <div id="quiz-questions">
      <!-- Question 1 -->
      <div class="question-card active" data-index="0">
        <p class="question-text">1. A battery of e.m.f. 12 V and internal resistance 2.0 Ω is connected to a 4.0 Ω resistor. What is the terminal potential difference (V) across the battery?</p>
        <ul class="options-list">
          <li class="option-item" data-value="A">A. 4.0 V</li>
          <li class="option-item" data-value="B">B. 6.0 V</li>
          <li class="option-item" data-value="C">C. 8.0 V</li>
          <li class="option-item" data-value="D">D. 12.0 V</li>
        </ul>
        <div class="feedback-box"></div>
      </div>

      <!-- Question 2 -->
      <div class="question-card" data-index="1">
        <p class="question-text">2. Two identical resistors are connected in parallel. This combination is then connected in series with a third identical resistor. If the total resistance of the circuit is 15 Ω, what is the resistance of each individual resistor?</p>
        <ul class="options-list">
          <li class="option-item" data-value="A">A. 5 Ω</li>
          <li class="option-item" data-value="B">B. 10 Ω</li>
          <li class="option-item" data-value="C">C. 15 Ω</li>
          <li class="option-item" data-value="D">D. 20 Ω</li>
        </ul>
        <div class="feedback-box"></div>
      </div>

      <!-- Question 3 -->
      <div class="question-card" data-index="2">
        <p class="question-text">3. Kirchhoff's First Law is a statement of the conservation of which physical quantity?</p>
        <ul class="options-list">
          <li class="option-item" data-value="A">A. Energy</li>
          <li class="option-item" data-value="B">B. Momentum</li>
          <li class="option-item" data-value="C">C. Charge</li>
          <li class="option-item" data-value="D">D. Voltage</li>
        </ul>
        <div class="feedback-box"></div>
      </div>
    </div>

    <!-- Controls -->
    <div class="controls" id="quiz-controls">
      <span id="question-number">Question 1 of 3</span>
      <button id="action-btn" class="btn" disabled>Check Answer</button>
    </div>

    <!-- Score Screen -->
    <div id="results-screen" class="results-screen">
      <h2>🎉 Quiz Completed!</h2>
      <p class="score-text" id="final-score">Your Score: 0 / 3</p>
      <button class="btn" onclick="location.reload()">Restart Quiz</button>
    </div>
  </main>

  <script>
    // Data Kuis (Kunci jawaban & Penjelasan Indonesia)
    const quizData = [
      {
        correct: "C",
        explanation: "Gunakan rumus kuat arus total: I = E / (R + r). Maka I = 12 / (4 + 2) = 2 A. Tegangan jepit (terminal p.d.) dihitung dengan V = I * R atau V = E - (I * r). Jadi, V = 2 A * 4 Ω = 8.0 V."
      },
      {
        correct: "B",
        explanation: "Dua resistor paralel nilainya menjadi R/2. Ditambah satu resistor seri (+ R), maka hambatan total R_total = 1.5R. Diketahui R_total = 15 Ω, sehingga 1.5R = 15, didapat R = 10 Ω."
      },
      {
        correct: "C",
        explanation: "Hukum Pertama Kirchhoff (Kirchhoff's First Law / Current Law) menyatakan bahwa jumlah arus yang masuk percabangan sama dengan yang keluar. Ini didasarkan pada prinsip Kekekalan Muatan (Conservation of Charge)."
      }
    ];

    let currentStep = 0; // 0 = melihat soal, 1 = setelah cek jawaban
    let currentIndex = 0;
    let selectedOption = null;
    let score = 0;

    const cards = document.querySelectorAll('.question-card');
    const actionBtn = document.getElementById('action-btn');
    const qNumberSpan = document.getElementById('question-number');
    const progressFill = document.getElementById('progress-fill');

    // Update Progress Bar
    function updateProgress() {
      const percentage = ((currentIndex) / cards.length) * 100;
      progressFill.style.width = `${percentage}%`;
      qNumberSpan.textContent = `Question ${currentIndex + 1} of ${cards.length}`;
    }

    // Handle Option Selection
    document.querySelectorAll('.option-item').forEach(item => {
      item.addEventListener('click', function() {
        if (currentStep === 1) return; // Kunci pilihan jika sudah cek jawaban

        const parent = this.closest('.question-card');
        parent.querySelectorAll('.option-item').forEach(el => el.classList.remove('selected'));
        
        this.classList.add('selected');
        selectedOption = this.getAttribute('data-value');
        actionBtn.disabled = false;
      });
    });

    // Handle Button Click (Check Answer / Next Question)
    actionBtn.addEventListener('click', function() {
      const currentCard = cards[currentIndex];
      const feedback = currentCard.querySelector('.feedback-box');
      const data = quizData[currentIndex];

      if (currentStep === 0) {
        // --- TAHAP CEK JAWABAN ---
        if (selectedOption === data.correct) {
          feedback.className = "feedback-box correct";
          feedback.innerHTML = `<strong>Correct!</strong>`;
          score++;
        } else {
          feedback.className = "feedback-box incorrect";
          feedback.innerHTML = `<strong>Incorrect.</strong> The correct answer is ${data.correct}.`;
        }
        // Tambahkan penjelasan bahasa Indonesia
        feedback.innerHTML += `<div class="explanation-title">Penjelasan:</div><div>${data.explanation}</div>`;
        
        // Ubah status tombol
        currentStep = 1;
        if (currentIndex === cards.length - 1) {
          actionBtn.textContent = "See Results";
        } else {
          actionBtn.textContent = "Next Question";
        }
      } else {
        // --- TAHAP LANJUT SOAL / SELESAI ---
        currentCard.classList.remove('active');
        currentIndex++;

        if (currentIndex < cards.length) {
          // Masuk ke soal berikutnya
          cards[currentIndex].classList.add('active');
          selectedOption = null;
          currentStep = 0;
          actionBtn.textContent = "Check Answer";
          actionBtn.disabled = true;
          updateProgress();
        } else {
          // Selesai kuis, tampilkan hasil
          document.getElementById('quiz-questions').style.display = 'none';
          document.getElementById('quiz-controls').style.display = 'none';
          progressFill.style.width = '100%';
          
          const resultsScreen = document.getElementById('results-screen');
          resultsScreen.style.display = 'block';
          document.getElementById('final-score').textContent = `Your Score: ${score} / ${cards.length}`;
        }
      }
    });

    // Inisialisasi awal
    updateProgress();
  </script>
</body>
</html>
