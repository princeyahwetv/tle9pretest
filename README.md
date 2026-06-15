<!doctype html>
<html lang="en" class="h-full">
 <head><script src="/_sdk/telemetry_sdk.js"></script>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TLE CSS 9 Pre-Test Quiz</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="https://cdn.jsdelivr.net/npm/lucide@0.263.0/dist/umd/lucide.min.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&amp;display=swap" rel="stylesheet">
  <style>
    * { font-family: 'DM Sans', sans-serif; }
    .option-btn { transition: all 0.2s; }
    .option-btn:hover:not(.selected):not(.correct):not(.wrong) { transform: translateX(4px); background: #e0f2fe; }
    .option-btn.selected { background: #bfdbfe; border-color: #3b82f6; }
    .option-btn.correct { background: #bbf7d0; border-color: #22c55e; }
    .option-btn.wrong { background: #fecaca; border-color: #ef4444; }
    .progress-fill { transition: width 0.4s ease; }
  </style>
  <style>body { box-sizing: border-box; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full">
  <div id="app" class="h-full w-full bg-slate-900 overflow-auto"><!-- Entry Form Screen -->
   <div id="entry-screen" class="flex items-center justify-center min-h-full p-6">
    <div class="text-center max-w-lg">
     <div class="w-20 h-20 bg-emerald-500 rounded-2xl flex items-center justify-center mx-auto mb-6"><i data-lucide="monitor" class="w-10 h-10 text-white"></i>
     </div>
     <h1 id="main-title" class="text-3xl font-bold text-white mb-3">TLE – ICT: Computer Systems Servicing</h1>
     <p class="text-slate-400 mb-6">50-Item Multiple Choice Pre-Test Quiz</p>
     <form onsubmit="proceedToQuiz(event)" class="space-y-4">
      <div class="text-left"><label class="block text-slate-300 text-sm font-medium mb-2">Full Name</label> <input id="student-name" type="text" placeholder="Enter your full name" class="w-full px-4 py-2 rounded-xl bg-slate-800 border-2 border-slate-700 text-white placeholder-slate-500 focus:border-emerald-500 focus:outline-none" required>
      </div>
      <div class="text-left"><label class="block text-slate-300 text-sm font-medium mb-2">Grade Level</label> <select id="student-grade" class="w-full px-4 py-2 rounded-xl bg-slate-800 border-2 border-slate-700 text-white focus:border-emerald-500 focus:outline-none" required> <option value="">Select Grade</option> <option value="7">Grade 7</option> <option value="8">Grade 8</option> <option value="9">Grade 9</option> <option value="10">Grade 10</option> </select>
      </div>
      <div class="text-left"><label class="block text-slate-300 text-sm font-medium mb-2">Section</label> <input id="student-section" type="text" placeholder="e.g., A, B, or CSS-1" class="w-full px-4 py-2 rounded-xl bg-slate-800 border-2 border-slate-700 text-white placeholder-slate-500 focus:border-emerald-500 focus:outline-none" required>
      </div><button type="submit" class="w-full bg-emerald-500 hover:bg-emerald-600 text-white font-semibold px-8 py-3 rounded-xl transition">Proceed to Quiz</button>
     </form>
    </div>
   </div><!-- Start Screen -->
   <div id="start-screen" class="hidden flex items-center justify-center min-h-full p-6">
    <div class="text-center max-w-lg">
     <div class="w-20 h-20 bg-emerald-500 rounded-2xl flex items-center justify-center mx-auto mb-6"><i data-lucide="monitor" class="w-10 h-10 text-white"></i>
     </div>
     <h1 id="main-title" class="text-3xl font-bold text-white mb-3">TLE – ICT: Computer Systems Servicing</h1>
     <p class="text-slate-400 mb-2">50-Item Multiple Choice Pre-Test Quiz</p>
     <p class="text-slate-500 text-sm mb-8">Read each question carefully. Choose the letter of the correct answer.</p>
     <div id="student-info" class="bg-slate-800 rounded-xl p-4 mb-6 text-left text-sm text-slate-300">
      <p><span class="text-emerald-400 font-medium">Name:</span> <span id="display-name"></span></p>
      <p><span class="text-emerald-400 font-medium">Grade:</span> <span id="display-grade"></span></p>
      <p><span class="text-emerald-400 font-medium">Section:</span> <span id="display-section"></span></p>
     </div>
     <p class="text-slate-500 text-sm mb-4">Time Limit: 60 minutes</p><button onclick="startQuiz()" class="bg-emerald-500 hover:bg-emerald-600 text-white font-semibold px-8 py-3 rounded-xl transition mr-3">Start Quiz</button> <button onclick="editInfo()" class="bg-slate-700 hover:bg-slate-600 text-white font-semibold px-8 py-3 rounded-xl transition">Edit Info</button>
    </div>
   </div><!-- Quiz Screen -->
   <div id="quiz-screen" class="hidden min-h-full p-4 md:p-6">
    <div class="max-w-2xl mx-auto">
     <div class="flex items-center justify-between mb-4"><span id="q-counter" class="text-emerald-400 font-medium text-sm">Question 1 of 50</span> <span id="timer-display" class="text-slate-400 text-sm">Time: 60:00</span>
     </div>
     <div class="w-full bg-slate-700 rounded-full h-2 mb-6">
      <div id="progress-bar" class="progress-fill bg-emerald-500 h-2 rounded-full" style="width:2%"></div>
     </div>
     <div class="bg-slate-800 rounded-2xl p-6 mb-4">
      <p id="category-label" class="text-emerald-400 text-xs font-medium uppercase tracking-wide mb-2"></p>
      <h2 id="question-text" class="text-white text-lg font-medium leading-relaxed"></h2>
     </div>
     <div id="options-container" class="space-y-3"></div>
     <div id="feedback" class="hidden mt-4 p-4 rounded-xl text-sm font-medium"></div><button id="next-btn" onclick="nextQuestion()" class="hidden mt-5 w-full bg-emerald-500 hover:bg-emerald-600 text-white font-semibold py-3 rounded-xl transition">Next Question</button>
    </div>
   </div><!-- Results Screen -->
   <div id="results-screen" class="hidden flex items-center justify-center min-h-full p-6">
    <div class="text-center max-w-lg">
     <div id="result-icon" class="w-20 h-20 rounded-2xl flex items-center justify-center mx-auto mb-6"></div>
     <h2 class="text-2xl font-bold text-white mb-2">Quiz Complete!</h2>
     <p id="result-score" class="text-4xl font-bold text-emerald-400 mb-2"></p>
     <p id="result-percent" class="text-slate-400 mb-6"></p>
     <div id="result-breakdown" class="bg-slate-800 rounded-xl p-4 mb-6 text-left text-sm text-slate-300 space-y-1"></div>
     <div class="bg-slate-800 rounded-xl p-4 mb-6 text-left text-sm text-slate-300">
      <p><span class="text-emerald-400 font-medium">Name:</span> <span id="result-name"></span></p>
      <p><span class="text-emerald-400 font-medium">Grade:</span> <span id="result-grade"></span></p>
      <p><span class="text-emerald-400 font-medium">Section:</span> <span id="result-section"></span></p>
     </div><button onclick="restartQuiz()" class="bg-emerald-500 hover:bg-emerald-600 text-white font-semibold px-8 py-3 rounded-xl transition">Retake Quiz</button>
    </div>
   </div><!-- Certificate Screen -->
   <div id="certificate-screen" class="hidden flex items-center justify-center min-h-full p-6 bg-gradient-to-br from-amber-900 via-slate-900 to-slate-900">
    <div class="max-w-2xl w-full">
     <div class="bg-gradient-to-b from-amber-50 to-yellow-50 rounded-2xl p-12 shadow-2xl border-4 border-amber-400">
      <div class="text-center mb-8">
       <div class="w-16 h-16 bg-emerald-500 rounded-full flex items-center justify-center mx-auto mb-4"><i data-lucide="award" class="w-8 h-8 text-white"></i>
       </div>
       <h1 class="text-4xl font-bold text-amber-900 mb-2">Certificate of Completion</h1>
       <p class="text-amber-700 text-sm">TLE – ICT: Computer Systems Servicing Pre-Test</p>
      </div>
      <div class="border-t-4 border-b-4 border-amber-400 py-8 mb-8 text-center">
       <p class="text-amber-900 text-sm mb-3">This is to certify that</p>
       <h2 id="cert-name" class="text-3xl font-bold text-emerald-600 mb-3"></h2>
       <p class="text-amber-900 text-sm mb-1">from</p>
       <p id="cert-grade-section" class="text-lg font-semibold text-amber-900 mb-4"></p>
       <p class="text-amber-900 text-sm leading-relaxed">has successfully completed the Pre-Test Assessment in<br><span class="font-semibold">TLE – ICT: Computer Systems Servicing</span></p>
      </div>
      <div class="grid grid-cols-3 gap-8 mb-6">
       <div class="text-center">
        <p class="text-amber-900 text-sm font-medium mb-2">Score</p>
        <p id="cert-score" class="text-2xl font-bold text-emerald-600"></p>
       </div>
       <div class="text-center">
        <p class="text-amber-900 text-sm font-medium mb-2">Percentage</p>
        <p id="cert-percent" class="text-2xl font-bold text-emerald-600"></p>
       </div>
       <div class="text-center">
        <p class="text-amber-900 text-sm font-medium mb-2">Date</p>
        <p id="cert-date" class="text-xl font-bold text-amber-900"></p>
       </div>
      </div>
      <div class="flex justify-between items-end mt-12 pt-8 border-t-2 border-amber-400">
       <div>
        <p class="text-amber-900 font-semibold text-sm">Joel P. Rodriguez</p>
        <p class="text-amber-700 text-xs">TLE Teacher</p>
       </div>
       <div class="text-right">
        <i data-lucide="stamp" class="w-12 h-12 text-amber-400 inline-block"></i>
       </div>
      </div>
     </div>
     <div class="text-center mt-8 space-y-3">
      <button onclick="downloadCertificate()" class="bg-emerald-500 hover:bg-emerald-600 text-white font-semibold px-8 py-3 rounded-xl transition mr-3"><i data-lucide="download" class="w-4 h-4 inline mr-2"></i>Download Certificate</button> <button onclick="retakeQuiz()" class="bg-slate-700 hover:bg-slate-600 text-white font-semibold px-8 py-3 rounded-xl transition"><i data-lucide="repeat" class="w-4 h-4 inline mr-2"></i>Retake Quiz</button>
     </div>
    </div>
   </div>
  </div>
  <script>
const questions = [
  {cat:"Career Opportunities and Tools",q:"Which career specializes in installing and repairing computer systems?",opts:["Chef","Computer Technician","Nurse","Architect"],ans:1},
  {cat:"Career Opportunities and Tools",q:"What is the primary function of a screwdriver in computer servicing?",opts:["Clean components","Test voltage","Tighten or loosen screws","Measure temperature"],ans:2},
  {cat:"Career Opportunities and Tools",q:"Which tool is used to prevent electrostatic discharge when handling computer parts?",opts:["Hammer","Paint Brush","Anti-static Wrist Strap","Tape Measure"],ans:2},
  {cat:"Career Opportunities and Tools",q:"Which of the following is considered a business opportunity in CSS?",opts:["Computer Repair Shop","Bakery","Farm Supply Store","Restaurant"],ans:0},
  {cat:"Career Opportunities and Tools",q:"Which tool is used to grip small objects and wires?",opts:["Pliers","Chisel","Saw","Ruler"],ans:0},
  {cat:"Parts of the Computer System Unit",q:'Which component is known as the "brain" of the computer?',opts:["RAM","Motherboard","CPU","Hard Drive"],ans:2},
  {cat:"Parts of the Computer System Unit",q:"What is the function of RAM?",opts:["Permanent storage","Temporary storage for active programs","Internet connection","Power supply"],ans:1},
  {cat:"Parts of the Computer System Unit",q:"Which component supplies electrical power to the computer?",opts:["PSU","CPU","SSD","GPU"],ans:0},
  {cat:"Parts of the Computer System Unit",q:"What component connects all parts of the computer together?",opts:["Monitor","Motherboard","Keyboard","Printer"],ans:1},
  {cat:"Parts of the Computer System Unit",q:"Which device stores data permanently?",opts:["RAM","Cache","SSD","Register"],ans:2},
  {cat:"System Software",q:"What is system software?",opts:["Software used for games only","Software that manages computer hardware","Software for drawing","Software for presentations"],ans:1},
  {cat:"System Software",q:"Which is an example of an operating system?",opts:["Microsoft Word","VLC","Windows 11","Photoshop"],ans:2},
  {cat:"System Software",q:"What is the function of a device driver?",opts:["Create documents","Control hardware devices","Edit videos","Browse websites"],ans:1},
  {cat:"System Software",q:"Which software helps maintain and optimize a computer?",opts:["Utility Software","Presentation Software","Spreadsheet Software","Multimedia Software"],ans:0},
  {cat:"System Software",q:"BIOS is an example of:",opts:["Application Software","Firmware","Game Software","Browser"],ans:1},
  {cat:"Application Software",q:"What is application software?",opts:["Software that performs user tasks","Hardware component","Computer cable","Network device"],ans:0},
  {cat:"Application Software",q:"Which software is commonly used for word processing?",opts:["Excel","PowerPoint","Microsoft Word","Paint"],ans:2},
  {cat:"Application Software",q:"Which type of software is used for calculations and data analysis?",opts:["Spreadsheet Software","Browser Software","Utility Software","Antivirus Software"],ans:0},
  {cat:"Application Software",q:"Which application is used for creating presentations?",opts:["PowerPoint","Word","Notepad","Calculator"],ans:0},
  {cat:"Application Software",q:"Google Chrome belongs to what type of software?",opts:["Utility Software","Web Browser","Operating System","Driver"],ans:1},
  {cat:"Computer Assembly and Safety",q:"What should be done before assembling a computer?",opts:["Disconnect power source","Turn on the computer","Remove RAM","Connect printer"],ans:0},
  {cat:"Computer Assembly and Safety",q:"Why should safety precautions be followed during assembly?",opts:["To waste time","To prevent accidents and damage","To increase cost","To slow down work"],ans:1},
  {cat:"Computer Assembly and Safety",q:"Which component should be installed onto the motherboard?",opts:["CPU","Monitor","Mouse","Scanner"],ans:0},
  {cat:"Computer Assembly and Safety",q:"What should be avoided when handling internal computer parts?",opts:["Static electricity","Clean workspace","Proper tools","Safety gloves"],ans:0},
  {cat:"Computer Assembly and Safety",q:"Which PPE helps protect technicians during servicing?",opts:["Safety Goggles","Slippers","Necklace","Cap"],ans:0},
  {cat:"Bootable Devices",q:"What is a bootable device?",opts:["Device used for cleaning","Device capable of starting a computer","Device for printing","Device for gaming"],ans:1},
  {cat:"Bootable Devices",q:"Which device is commonly used as a bootable installer?",opts:["USB Flash Drive","Speaker","Webcam","Microphone"],ans:0},
  {cat:"Bootable Devices",q:"Why is a bootable USB useful?",opts:["To install or repair operating systems","To increase RAM","To improve graphics","To cool the CPU"],ans:0},
  {cat:"Bootable Devices",q:"What software is often copied to a bootable device?",opts:["Operating System Files","Songs","Pictures","Documents"],ans:0},
  {cat:"Bootable Devices",q:"What must be configured to boot from a USB device?",opts:["BIOS/UEFI Settings","Monitor Settings","Speaker Settings","Keyboard Settings"],ans:0},
  {cat:"Operating System Installation",q:"What is the first step in OS installation?",opts:["Prepare installation media","Install printer","Connect speakers","Delete keyboard drivers"],ans:0},
  {cat:"Operating System Installation",q:"Which operating system is commonly installed on personal computers?",opts:["Windows","Chrome","Zoom","Canva"],ans:0},
  {cat:"Operating System Installation",q:"Why should important files be backed up before OS installation?",opts:["To increase speed","To prevent data loss","To save electricity","To improve graphics"],ans:1},
  {cat:"Operating System Installation",q:"During installation, users may need to:",opts:["Select a storage drive","Remove motherboard","Replace monitor","Cut wires"],ans:0},
  {cat:"Operating System Installation",q:"Which practice is important during OS installation?",opts:["Following proper procedures","Guessing settings","Disconnecting storage","Removing RAM"],ans:0},
  {cat:"Software and Driver Installation",q:"What is installed to allow hardware to communicate with the OS?",opts:["Drivers","Wallpapers","Documents","Games"],ans:0},
  {cat:"Software and Driver Installation",q:"Which software helps protect a computer from malware?",opts:["Antivirus","Calculator","Paint","Notepad"],ans:0},
  {cat:"Software and Driver Installation",q:"What should be checked before installing software?",opts:["System Requirements","Keyboard Color","Mouse Brand","Table Size"],ans:0},
  {cat:"Software and Driver Installation",q:"Why are software updates important?",opts:["Improve security and performance","Decrease storage","Remove applications","Damage files"],ans:0},
  {cat:"Software and Driver Installation",q:"Utility software is used to:",opts:["Maintain and manage systems","Create paintings","Watch movies only","Design buildings"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"What is troubleshooting?",opts:["Identifying and solving computer problems","Installing games","Buying hardware","Writing essays"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"Which step comes first in troubleshooting?",opts:["Identify the problem","Replace all parts","Format the drive","Restart repeatedly"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"Why should drivers be updated?",opts:["For compatibility and performance","To remove hardware","To decrease speed","To erase files"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"What should be done after repairing a computer?",opts:["Test the system","Turn it off permanently","Remove software","Delete drivers"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"Which maintenance task helps prevent overheating?",opts:["Cleaning dust from components","Removing fans","Closing programs only","Disconnecting RAM"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"What is preventive maintenance?",opts:["Actions taken to avoid future problems","Buying new computers","Playing games","Installing wallpapers"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"Which device is considered a peripheral?",opts:["Printer","CPU","Motherboard","RAM"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"What is the purpose of checking software updates regularly?",opts:["Improve security and functionality","Damage programs","Reduce memory","Remove files"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"Which action helps prolong computer life?",opts:["Regular maintenance","Ignoring updates","Blocking ventilation","Exposing to dust"],ans:0},
  {cat:"Testing, Troubleshooting, and Maintenance",q:"A technician should always document repairs because:",opts:["It helps track issues and solutions","It wastes time","It increases errors","It slows work"],ans:0},
];

let current = 0, score = 0, answered = false, timeLeft = 3600, timerInterval = null;
let studentName = '', studentGrade = '', studentSection = '';
const letters = ['A','B','C','D'];

function proceedToQuiz(e) {
  e.preventDefault();
  studentName = document.getElementById('student-name').value.trim();
  studentGrade = document.getElementById('student-grade').value;
  studentSection = document.getElementById('student-section').value.trim();
  
  if (!studentName || !studentGrade || !studentSection) {
    alert('Please fill in all fields');
    return;
  }
  
  document.getElementById('entry-screen').classList.add('hidden');
  document.getElementById('start-screen').classList.remove('hidden');
  document.getElementById('display-name').textContent = studentName;
  document.getElementById('display-grade').textContent = 'Grade ' + studentGrade;
  document.getElementById('display-section').textContent = studentSection;
}

function editInfo() {
  document.getElementById('start-screen').classList.add('hidden');
  document.getElementById('entry-screen').classList.remove('hidden');
  document.getElementById('student-name').value = studentName;
  document.getElementById('student-grade').value = studentGrade;
  document.getElementById('student-section').value = studentSection;
}

function startQuiz() {
  document.getElementById('start-screen').classList.add('hidden');
  document.getElementById('quiz-screen').classList.remove('hidden');
  current = 0; score = 0; answered = false; timeLeft = 3600;
  startTimer();
  showQuestion();
}

function startTimer() {
  if (timerInterval) clearInterval(timerInterval);
  timerInterval = setInterval(() => {
    timeLeft--;
    const mins = Math.floor(timeLeft / 60);
    const secs = timeLeft % 60;
    document.getElementById('timer-display').textContent = `Time: ${mins}:${secs.toString().padStart(2, '0')}`;
    
    if (timeLeft <= 0) {
      clearInterval(timerInterval);
      endQuiz();
    }
  }, 1000);
}

function showQuestion() {
  answered = false;
  const q = questions[current];
  document.getElementById('q-counter').textContent = `Question ${current+1} of 50`;
  document.getElementById('progress-bar').style.width = `${((current)/50)*100}%`;
  document.getElementById('category-label').textContent = q.cat;
  document.getElementById('question-text').textContent = `${current+1}. ${q.q}`;
  document.getElementById('feedback').classList.add('hidden');
  document.getElementById('next-btn').classList.add('hidden');

  const container = document.getElementById('options-container');
  container.innerHTML = '';
  q.opts.forEach((opt, i) => {
    const btn = document.createElement('button');
    btn.className = 'option-btn w-full text-left p-4 rounded-xl border-2 border-slate-700 bg-slate-800 text-slate-200 flex items-center gap-3';
    btn.innerHTML = `<span class="w-8 h-8 rounded-lg bg-slate-700 flex items-center justify-center text-sm font-bold shrink-0">${letters[i]}</span><span>${opt}</span>`;
    btn.onclick = () => selectAnswer(i);
    container.appendChild(btn);
  });
}

function selectAnswer(i) {
  if (answered) return;
  answered = true;
  const q = questions[current];

  if (i === q.ans) {
    score++;
  }
  
  // Add gray highlight to selected answer
  const buttons = document.querySelectorAll('.option-btn');
  buttons[i].style.background = '#6b7280';
  buttons[i].style.borderColor = '#4b5563';
  
  document.getElementById('next-btn').classList.remove('hidden');
  document.getElementById('next-btn').textContent = current < 49 ? 'Next Question' : 'See Results';
}

function nextQuestion() {
  current++;
  if (current >= 50) endQuiz();
  else showQuestion();
}

function endQuiz() {
  clearInterval(timerInterval);
  showResults();
}

function showResults() {
  document.getElementById('quiz-screen').classList.add('hidden');
  document.getElementById('results-screen').classList.remove('hidden');
  const pct = Math.round((score/50)*100);
  document.getElementById('result-score').textContent = `${score} / 50`;
  document.getElementById('result-percent').textContent = `${pct}% correct`;
  document.getElementById('result-name').textContent = studentName;
  document.getElementById('result-grade').textContent = 'Grade ' + studentGrade;
  document.getElementById('result-section').textContent = studentSection;
  const icon = document.getElementById('result-icon');
  if (pct >= 80) { icon.className = 'w-20 h-20 rounded-2xl flex items-center justify-center mx-auto mb-6 bg-emerald-500'; icon.innerHTML = '<i data-lucide="trophy" class="w-10 h-10 text-white"></i>'; }
  else if (pct >= 50) { icon.className = 'w-20 h-20 rounded-2xl flex items-center justify-center mx-auto mb-6 bg-amber-500'; icon.innerHTML = '<i data-lucide="target" class="w-10 h-10 text-white"></i>'; }
  else { icon.className = 'w-20 h-20 rounded-2xl flex items-center justify-center mx-auto mb-6 bg-red-500'; icon.innerHTML = '<i data-lucide="refresh-cw" class="w-10 h-10 text-white"></i>'; }
  const bd = document.getElementById('result-breakdown');
  let msg = pct >= 80 ? 'Excellent work! You have a strong understanding of CSS concepts.' : pct >= 50 ? 'Good effort! Review the topics you missed and try again.' : 'Keep studying! Focus on the categories where you struggled.';
  bd.innerHTML = `<p>${msg}</p>`;
  
  const btnContainer = document.querySelector('#results-screen button');
  if (btnContainer) {
    btnContainer.textContent = 'View Certificate';
    btnContainer.onclick = showCertificate;
  }
  lucide.createIcons();
}

function showCertificate() {
  document.getElementById('results-screen').classList.add('hidden');
  document.getElementById('certificate-screen').classList.remove('hidden');
  
  const pct = Math.round((score/50)*100);
  document.getElementById('cert-name').textContent = studentName;
  document.getElementById('cert-grade-section').textContent = `Grade ${studentGrade}, Section ${studentSection}`;
  document.getElementById('cert-score').textContent = `${score} / 50`;
  document.getElementById('cert-percent').textContent = `${pct}%`;
  
  const today = new Date();
  const dateStr = today.toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric' });
  document.getElementById('cert-date').textContent = dateStr;
  
  lucide.createIcons();
}

function downloadCertificate() {
  const cert = document.getElementById('certificate-screen').querySelector('.bg-gradient-to-b');
  const canvas = document.createElement('canvas');
  const ctx = canvas.getContext('2d');
  
  canvas.width = 1200;
  canvas.height = 850;
  
  // Background
  const gradient = ctx.createLinearGradient(0, 0, 0, canvas.height);
  gradient.addColorStop(0, '#fef3c7');
  gradient.addColorStop(1, '#fef9e7');
  ctx.fillStyle = gradient;
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  
  // Border
  ctx.strokeStyle = '#f59e0b';
  ctx.lineWidth = 12;
  ctx.strokeRect(30, 30, canvas.width - 60, canvas.height - 60);
  
  // Title
  ctx.font = 'bold 48px serif';
  ctx.fillStyle = '#78350f';
  ctx.textAlign = 'center';
  ctx.fillText('Certificate of Completion', canvas.width / 2, 100);
  
  ctx.font = '16px serif';
  ctx.fillStyle = '#92400e';
  ctx.fillText('TLE – ICT: Computer Systems Servicing Pre-Test', canvas.width / 2, 140);
  
  // Top divider
  ctx.strokeStyle = '#f59e0b';
  ctx.lineWidth = 4;
  ctx.beginPath();
  ctx.moveTo(100, 180);
  ctx.lineTo(canvas.width - 100, 180);
  ctx.stroke();
  
  // Certificate text
  ctx.font = '16px serif';
  ctx.fillStyle = '#78350f';
  ctx.textAlign = 'center';
  ctx.fillText('This is to certify that', canvas.width / 2, 240);
  
  ctx.font = 'bold 44px serif';
  ctx.fillStyle = '#059669';
  ctx.fillText(studentName, canvas.width / 2, 320);
  
  ctx.font = '16px serif';
  ctx.fillStyle = '#78350f';
  ctx.fillText('from', canvas.width / 2, 370);
  
  ctx.font = 'bold 20px serif';
  ctx.fillText(`Grade ${studentGrade}, Section ${studentSection}`, canvas.width / 2, 410);
  
  ctx.font = '16px serif';
  ctx.fillStyle = '#78350f';
  ctx.fillText('has successfully completed the Pre-Test Assessment in', canvas.width / 2, 470);
  
  ctx.font = 'bold 18px serif';
  ctx.fillText('TLE – ICT: Computer Systems Servicing', canvas.width / 2, 510);
  
  // Bottom divider
  ctx.strokeStyle = '#f59e0b';
  ctx.lineWidth = 3;
  ctx.beginPath();
  ctx.moveTo(100, 570);
  ctx.lineTo(canvas.width - 100, 570);
  ctx.stroke();
  
  // Stats
  const pct = Math.round((score/50)*100);
  ctx.font = 'bold 16px serif';
  ctx.fillStyle = '#78350f';
  ctx.fillText('Score', canvas.width / 4, 640);
  ctx.font = 'bold 32px serif';
  ctx.fillStyle = '#059669';
  ctx.fillText(`${score}/50`, canvas.width / 4, 690);
  
  ctx.font = 'bold 16px serif';
  ctx.fillStyle = '#78350f';
  ctx.textAlign = 'center';
  ctx.fillText('Percentage', canvas.width / 2, 640);
  ctx.font = 'bold 32px serif';
  ctx.fillStyle = '#059669';
  ctx.fillText(`${pct}%`, canvas.width / 2, 690);
  
  const today = new Date();
  const dateStr = today.toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric' });
  ctx.font = 'bold 16px serif';
  ctx.fillStyle = '#78350f';
  ctx.textAlign = 'center';
  ctx.fillText('Date', (canvas.width * 3) / 4, 640);
  ctx.font = 'bold 18px serif';
  ctx.fillStyle = '#78350f';
  ctx.fillText(dateStr, (canvas.width * 3) / 4, 690);
  
  // Signature
  ctx.font = 'bold 18px serif';
  ctx.fillStyle = '#78350f';
  ctx.textAlign = 'left';
  ctx.fillText('Joel P. Rodriguez', 100, 780);
  ctx.font = '14px serif';
  ctx.fillStyle = '#92400e';
  ctx.fillText('TLE Teacher', 100, 810);
  
  // Download
  canvas.toBlob(blob => {
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `Certificate_${studentName.replace(/\s+/g, '_')}_${new Date().getTime()}.png`;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
  });
}

function restartQuiz() {
  document.getElementById('results-screen').classList.add('hidden');
  document.getElementById('entry-screen').classList.remove('hidden');
  document.getElementById('student-name').value = '';
  document.getElementById('student-grade').value = '';
  document.getElementById('student-section').value = '';
  studentName = '';
  studentGrade = '';
  studentSection = '';
  if (timerInterval) clearInterval(timerInterval);
}

// Element SDK
const defaultConfig = { quiz_title: 'TLE – ICT: Computer Systems Servicing', background_color: '#0f172a', surface_color: '#1e293b', text_color: '#f1f5f9', primary_action_color: '#10b981', secondary_action_color: '#94a3b8', font_family: 'DM Sans', font_size: 16 };

window.elementSdk.init({
  defaultConfig,
  onConfigChange: async (config) => {
    const bg = config.background_color || defaultConfig.background_color;
    const sf = config.surface_color || defaultConfig.surface_color;
    const tx = config.text_color || defaultConfig.text_color;
    const pa = config.primary_action_color || defaultConfig.primary_action_color;
    const sa = config.secondary_action_color || defaultConfig.secondary_action_color;
    const ff = config.font_family || defaultConfig.font_family;
    const fs = config.font_size || defaultConfig.font_size;

    document.getElementById('app').style.background = bg;
    document.querySelectorAll('.bg-slate-800').forEach(el => el.style.background = sf);
    document.getElementById('main-title').textContent = config.quiz_title || defaultConfig.quiz_title;
    document.getElementById('main-title').style.color = tx;
    document.getElementById('main-title').style.fontFamily = `${ff}, sans-serif`;
    document.getElementById('main-title').style.fontSize = `${fs * 1.8}px`;
  },
  mapToCapabilities: (config) => ({
    recolorables: [
      { get: () => config.background_color || defaultConfig.background_color, set: (v) => { config.background_color = v; window.elementSdk.setConfig({ background_color: v }); } },
      { get: () => config.surface_color || defaultConfig.surface_color, set: (v) => { config.surface_color = v; window.elementSdk.setConfig({ surface_color: v }); } },
      { get: () => config.text_color || defaultConfig.text_color, set: (v) => { config.text_color = v; window.elementSdk.setConfig({ text_color: v }); } },
      { get: () => config.primary_action_color || defaultConfig.primary_action_color, set: (v) => { config.primary_action_color = v; window.elementSdk.setConfig({ primary_action_color: v }); } },
      { get: () => config.secondary_action_color || defaultConfig.secondary_action_color, set: (v) => { config.secondary_action_color = v; window.elementSdk.setConfig({ secondary_action_color: v }); } },
    ],
    borderables: [],
    fontEditable: { get: () => config.font_family || defaultConfig.font_family, set: (v) => { config.font_family = v; window.elementSdk.setConfig({ font_family: v }); } },
    fontSizeable: { get: () => config.font_size || defaultConfig.font_size, set: (v) => { config.font_size = v; window.elementSdk.setConfig({ font_size: v }); } },
  }),
  mapToEditPanelValues: (config) => new Map([["quiz_title", config.quiz_title || defaultConfig.quiz_title]])
});

lucide.createIcons();
</script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'a0bde9c520c98d0f',t:'MTc4MTQ4ODExMy4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
