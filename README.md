<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>QCM — Vocabulaire du Théâtre & Figures de Style</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
    <style>
        :root {
          --bg: #0f0e0c;
          --surface: #1a1814;
          --card: #211f1b;
          --gold: #c9a84c;
          --gold-light: #e8c97a;
          --cream: #f0e8d5;
          --red: #c0392b;
          --green: #2ecc71;
          --muted: #6b6459;
          --border: #332e27;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
          background: var(--bg);
          color: var(--cream);
          font-family: 'DM Sans', sans-serif;
          min-height: 100vh;
          padding: 2rem 1rem 4rem;
        }

        /* Curtain texture background */
        body::before {
          content: '';
          position: fixed;
          inset: 0;
          background: repeating-linear-gradient(
            90deg,
            transparent,
            transparent 40px,
            rgba(201,168,76,0.015) 40px,
            rgba(201,168,76,0.015) 41px
          );
          pointer-events: none;
          z-index: 0;
        }

        .container {
          max-width: 760px;
          margin: 0 auto;
          position: relative;
          z-index: 1;
        }

        header {
          text-align: center;
          margin-bottom: 3rem;
          padding-bottom: 2rem;
          border-bottom: 1px solid var(--border);
        }

        .stage-icon {
          font-size: 2.5rem;
          margin-bottom: 0.75rem;
          display: block;
          filter: drop-shadow(0 0 12px rgba(201,168,76,0.4));
        }

        h1 {
          font-family: 'Playfair Display', serif;
          font-size: clamp(1.6rem, 4vw, 2.4rem);
          color: var(--gold-light);
          letter-spacing: 0.02em;
          line-height: 1.2;
        }

        .subtitle {
          margin-top: 0.5rem;
          color: var(--muted);
          font-size: 0.9rem;
          letter-spacing: 0.05em;
          text-transform: uppercase;
        }

        /* Progress */
        .progress-bar-wrap {
          background: var(--border);
          border-radius: 99px;
          height: 4px;
          margin-bottom: 2.5rem;
          overflow: hidden;
        }
        .progress-bar-fill {
          height: 100%;
          background: linear-gradient(90deg, var(--gold), var(--gold-light));
          border-radius: 99px;
          transition: width 0.5s ease;
        }

        .progress-label {
          text-align: right;
          font-size: 0.78rem;
          color: var(--muted);
          margin-bottom: 0.5rem;
          letter-spacing: 0.04em;
        }

        /* Question card */
        .question-card {
          background: var(--card);
          border: 1px solid var(--border);
          border-radius: 12px;
          padding: 2rem 2rem 1.6rem;
          margin-bottom: 1.5rem;
          animation: slideIn 0.35s ease forwards;
        }

        @keyframes slideIn {
          from { opacity: 0; transform: translateY(18px); }
          to   { opacity: 1; transform: translateY(0); }
        }

        .question-meta {
          display: flex;
          align-items: center;
          gap: 0.6rem;
          margin-bottom: 1.1rem;
        }

        .q-number {
          background: var(--gold);
          color: var(--bg);
          font-size: 0.72rem;
          font-weight: 700;
          padding: 0.2em 0.7em;
          border-radius: 99px;
          letter-spacing: 0.05em;
          text-transform: uppercase;
        }

        .q-category {
          color: var(--muted);
          font-size: 0.75rem;
          text-transform: uppercase;
          letter-spacing: 0.07em;
        }

        .question-text {
          font-family: 'Playfair Display', serif;
          font-size: 1.15rem;
          line-height: 1.6;
          color: var(--cream);
          margin-bottom: 1.4rem;
        }

        /* Options */
        .options {
          display: flex;
          flex-direction: column;
          gap: 0.65rem;
        }

        .option-btn {
          background: var(--surface);
          border: 1.5px solid var(--border);
          border-radius: 8px;
          color: var(--cream);
          font-family: 'DM Sans', sans-serif;
          font-size: 0.95rem;
          padding: 0.85rem 1.2rem;
          text-align: left;
          cursor: pointer;
          transition: border-color 0.2s, background 0.2s, transform 0.1s;
          display: flex;
          align-items: center;
          gap: 0.75rem;
        }

        .option-btn .letter {
          width: 26px;
          height: 26px;
          border-radius: 50%;
          background: var(--border);
          color: var(--gold);
          font-size: 0.8rem;
          font-weight: 600;
          display: flex;
          align-items: center;
          justify-content: center;
          flex-shrink: 0;
          transition: background 0.2s, color 0.2s;
        }

        .option-btn:hover:not(:disabled) {
          border-color: var(--gold);
          background: rgba(201,168,76,0.06);
          transform: translateX(3px);
        }
        .option-btn:hover:not(:disabled) .letter {
          background: var(--gold);
          color: var(--bg);
        }

        .option-btn.correct {
          border-color: var(--green);
          background: rgba(46,204,113,0.08);
        }
        .option-btn.correct .letter { background: var(--green); color: #fff; }

        .option-btn.wrong {
          border-color: var(--red);
          background: rgba(192,57,43,0.08);
        }
        .option-btn.wrong .letter { background: var(--red); color: #fff; }

        .option-btn:disabled { cursor: default; transform: none !important; }

        /* Feedback */
        .feedback {
          margin-top: 1.1rem;
          padding: 0.9rem 1.1rem;
          border-radius: 8px;
          font-size: 0.88rem;
          line-height: 1.55;
          display: none;
        }
        .feedback.show { display: block; animation: fadeIn 0.3s ease; }
        .feedback.correct-fb { background: rgba(46,204,113,0.1); border-left: 3px solid var(--green); color: #7ee8a2; }
        .feedback.wrong-fb   { background: rgba(192,57,43,0.1);  border-left: 3px solid var(--red);   color: #e8a0a0; }

        /* Nav */
        .nav {
          display: flex;
          justify-content: flex-end;
          margin-top: 1rem;
        }

        .nav-btn {
          background: var(--gold);
          color: var(--bg);
          border: none;
          border-radius: 8px;
          padding: 0.7rem 1.8rem;
          font-family: 'DM Sans', sans-serif;
          font-size: 0.92rem;
          font-weight: 600;
          cursor: pointer;
          letter-spacing: 0.03em;
          transition: background 0.2s, transform 0.1s;
        }
        .nav-btn:hover { background: var(--gold-light); transform: translateY(-1px); }
        .nav-btn:disabled { background: var(--border); color: var(--muted); cursor: default; transform: none; }

        /* Score screen */
        .score-screen {
          display: none;
          text-align: center;
          padding: 3rem 2rem;
          background: var(--card);
          border: 1px solid var(--border);
          border-radius: 12px;
          animation: slideIn 0.4s ease;
        }
        .score-screen.show { display: block; }

        .score-emoji { font-size: 3.5rem; margin-bottom: 1rem; }
        .score-title {
          font-family: 'Playfair Display', serif;
          font-size: 2rem;
          color: var(--gold-light);
          margin-bottom: 0.5rem;
        }
        .score-fraction { font-size: 3.5rem; font-weight: 700; color: var(--gold); margin: 1rem 0; }
        .score-msg { color: var(--muted); font-size: 0.95rem; line-height: 1.6; max-width: 400px; margin: 0 auto 2rem; }

        .restart-btn {
          background: transparent;
          border: 1.5px solid var(--gold);
          color: var(--gold);
          border-radius: 8px;
          padding: 0.75rem 2.2rem;
          font-family: 'DM Sans', sans-serif;
          font-size: 0.95rem;
          font-weight: 500;
          cursor: pointer;
          transition: background 0.2s, color 0.2s;
        }
        .restart-btn:hover { background: var(--gold); color: var(--bg); }

        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
    </style>
</head>
<body>
<div class="container">
    <header>
        <span class="stage-icon">🎭</span>
        <h1>Vocabulaire du Théâtre<br><em style="font-style:italic;font-weight:400">& Figures de Style</em></h1>
        <p class="subtitle">Quiz de révision · Français</p>
    </header>

    <div id="quiz-area">
        <div class="progress-label" id="progress-label">Question 1 / 30</div>
        <div class="progress-bar-wrap"><div class="progress-bar-fill" id="progress-bar" style="width:3.3%"></div></div>
        <div class="question-card" id="q-card">
            <!-- injected by JS -->
        </div>
        <div class="nav">
            <button class="nav-btn" id="next-btn" disabled onclick="nextQuestion()">Suivant →</button>
        </div>
    </div>

    <div class="score-screen" id="score-screen">
        <div class="score-emoji" id="score-emoji">🎉</div>
        <div class="score-title">Résultat final</div>
        <div class="score-fraction" id="score-fraction">0 / 30</div>
        <div class="score-msg" id="score-msg"></div>
        <button class="restart-btn" onclick="restart()">↺ Recommencer</button>
    </div>
</div>

<script>
    const ALL_QUESTIONS = [
      // === VOCAB DU THÉÂTRE ===
      {
        cat: "Vocab du théâtre",
        q: "Qu'est-ce qu'un <strong>acte</strong> dans une pièce de théâtre ?",
        opts: [
          "Une réplique longue prononcée par un seul personnage",
          "Une grande division de la pièce, souvent marquée par la fermeture du rideau",
          "Un ensemble de répliques courtes entre deux personnages",
          "Une indication scénique destinée au metteur en scène"
        ],
        ans: 1,
        fb: "Un acte marque les grands moments de l'histoire et est caractérisé par la fermeture du rideau."
      },
      {
        cat: "Vocab du théâtre",
        q: "Qu'est-ce qui marque traditionnellement le début d'une nouvelle <strong>scène</strong> ?",
        opts: [
          "La fermeture du rideau",
          "Un changement de décor",
          "L'entrée ou la sortie d'un personnage sur scène",
          "Un monologue du personnage principal"
        ],
        ans: 2,
        fb: "Une scène est traditionnellement marquée par l'entrée ou la sortie d'un personnage sur scène."
      },
      {
        cat: "Vocab du théâtre",
        q: "Une <strong>réplique</strong>, c'est…",
        opts: [
          "Un texte non destiné à être prononcé sur scène",
          "Une prise de parole destinée à être prononcée sur scène",
          "Une longue tirade d'un personnage seul",
          "Un échange rapide entre deux personnages"
        ],
        ans: 1,
        fb: "Une réplique est une prise de parole destinée à être prononcée sur scène."
      },
      {
        cat: "Vocab du théâtre",
        q: "Quelle est la définition d'une <strong>didascalie</strong> ?",
        opts: [
          "Une réplique très longue prononcée par le héros",
          "Un aparté destiné au public uniquement",
          "Une partie du texte non destinée à être prononcée, donnant des indications scéniques",
          "Un échange rythmé entre deux personnages"
        ],
        ans: 2,
        fb: "La didascalie donne des indications sur l'attitude des personnages, le ton, le décor, etc. Elle n'est pas prononcée."
      },
      {
        cat: "Vocab du théâtre",
        q: "Quel est le rôle d'une <strong>tirade</strong> ?",
        opts: [
          "Accélérer le rythme de l'action",
          "Ralentir le rythme pour laisser un personnage développer ses pensées",
          "Permettre au personnage de s'adresser discrètement au public",
          "Indiquer les changements de décor"
        ],
        ans: 1,
        fb: "La tirade ralentit le rythme de l'intrigue pour se concentrer sur un personnage qui développe ses pensées."
      },
      {
        cat: "Vocab du théâtre",
        q: "Un <strong>monologue</strong> est prononcé par un personnage qui est…",
        opts: [
          "Entouré de plusieurs autres personnages",
          "Caché dans les coulisses",
          "Seul sur scène",
          "En dialogue avec le metteur en scène"
        ],
        ans: 2,
        fb: "Le monologue est une longue réplique prononcée par un personnage seul sur scène qui livre ses états d'âme."
      },
      {
        cat: "Vocab du théâtre",
        q: "Quelle figure théâtrale permet à une réplique d'être entendue par les spectateurs ou un personnage précis, mais pas par tous ceux présents sur scène ?",
        opts: [
          "La tirade",
          "Le monologue",
          "La didascalie",
          "L'aparté"
        ],
        ans: 3,
        fb: "L'aparté est prononcé «à part» pour être entendu soit par les spectateurs, soit par un personnage spécifique."
      },
      {
        cat: "Vocab du théâtre",
        q: "La <strong>stichomythie</strong> se caractérise par…",
        opts: [
          "Des répliques longues qui ralentissent l'action",
          "Un ensemble de répliques courtes qui donnent un rythme rapide",
          "Un discours prononcé par un personnage seul",
          "Des indications de mise en scène intercalées dans les dialogues"
        ],
        ans: 1,
        fb: "La stichomythie est un ensemble de répliques courtes qui accélèrent le rythme, souvent lors d'affrontements."
      },
      // === STRUCTURATION DES MOTS ===
      {
        cat: "Structuration des mots",
        q: "Des <strong>synonymes</strong> sont des mots qui…",
        opts: [
          "Ont un sens opposé",
          "Se prononcent identiquement mais ont un sens différent",
          "Ont le même sens",
          "Se ressemblent dans leur graphie"
        ],
        ans: 2,
        fb: "Les synonymes ont le même sens, comme 'rapide' et 'vite'."
      },
      {
        cat: "Structuration des mots",
        q: "Quel terme désigne des mots de sens différents mais de prononciation identique ?",
        opts: [
          "Antonymes",
          "Homonymes",
          "Paronymes",
          "Synonymes"
        ],
        ans: 1,
        fb: "Les homonymes se prononcent pareil mais ont un sens différent (ex : 'verre', 'vers', 'vert')."
      },
      {
        cat: "Structuration des mots",
        q: "Les <strong>antonymes</strong> sont des mots…",
        opts: [
          "Qui se ressemblent à l'écrit",
          "Qui ont le même sens",
          "De sens opposés",
          "Qui sont synonymes dans certains contextes"
        ],
        ans: 2,
        fb: "Les antonymes ont des sens opposés, comme 'chaud' et 'froid'."
      },
      {
        cat: "Structuration des mots",
        q: "Quelle est la différence entre <strong>inepte</strong> et <strong>inapte</strong> ? Ce sont des exemples de…",
        opts: [
          "Synonymes",
          "Homonymes",
          "Antonymes",
          "Paronymes"
        ],
        ans: 3,
        fb: "Les paronymes se ressemblent beaucoup dans leur graphie ou prononciation mais ont un sens différent."
      },
      {
        cat: "Structuration des mots",
        q: "Les <strong>connotations</strong> d'un mot, c'est…",
        opts: [
          "Sa définition première dans le dictionnaire",
          "Les images et associations que l'on peut lier à ce mot",
          "L'ensemble des mots qui ont le même sens",
          "Le sens opposé du mot"
        ],
        ans: 1,
        fb: "Les connotations sont les images et évocations associées à un mot, au-delà de sa définition stricte."
      },
      {
        cat: "Structuration des mots",
        q: "La <strong>dénotation</strong> d'un mot est…",
        opts: [
          "L'ensemble des images qu'on lui associe",
          "Un mot qui lui ressemble à l'écrit",
          "Sa définition la plus communément admise, le sens premier du dictionnaire",
          "Le sens qu'il prend dans un contexte précis"
        ],
        ans: 2,
        fb: "La dénotation est le sens premier et objectif du dictionnaire, sans associations subjectives."
      },
      {
        cat: "Structuration des mots",
        q: "Un <strong>champ lexical</strong>, c'est…",
        opts: [
          "Un mot qui peut avoir plusieurs sens",
          "L'ensemble des mots réunis autour d'un même thème",
          "Deux mots qui ont le même sens",
          "Un mot dont le sens est opposé à un autre"
        ],
        ans: 1,
        fb: "Le champ lexical regroupe tous les mots d'un texte qui se rapportent à un même thème."
      },
      {
        cat: "Structuration des mots",
        q: "Le mot «voler» peut désigner un oiseau dans l'air ou un criminel. C'est un exemple de mot…",
        opts: [
          "Antonyme",
          "Paronyme",
          "Polysémique",
          "Homonyme"
        ],
        ans: 2,
        fb: "Un mot polysémique possède plusieurs sens tout en étant le même mot (ex : 'voler')."
      },
      // === FIGURES DE STYLE ===
      {
        cat: "Figures de style",
        q: "La <strong>comparaison</strong> se distingue de la métaphore car elle…",
        opts: [
          "Fusionne deux éléments implicitement",
          "Utilise un outil de comparaison explicite (comme, tel que…)",
          "Attribue des traits humains à un objet",
          "Dure sur plusieurs lignes"
        ],
        ans: 1,
        fb: "La comparaison relie deux éléments à l'aide d'un outil de comparaison explicite (comme, tel, pareil à…)."
      },
      {
        cat: "Figures de style",
        q: "Dans une comparaison, l'élément qui est rapproché d'un autre s'appelle le…",
        opts: [
          "Comparant",
          "Outil de comparaison",
          "Comparé",
          "Référent"
        ],
        ans: 2,
        fb: "Le comparé est l'élément dont on parle, que l'on rapproche d'un autre (le comparant)."
      },
      {
        cat: "Figures de style",
        q: "Une <strong>métaphore filée</strong>, c'est une métaphore qui…",
        opts: [
          "Compare deux éléments de manière explicite",
          "Se prolonge sur plusieurs lignes",
          "Attribue des émotions à un animal",
          "Oppose deux notions contraires"
        ],
        ans: 1,
        fb: "La métaphore filée est une métaphore étendue sur plusieurs lignes d'un texte."
      },
      {
        cat: "Figures de style",
        q: "La <strong>personnification</strong> consiste à…",
        opts: [
          "Exagérer la réalité pour frapper l'imagination",
          "Attribuer des comportements humains à des animaux, objets ou éléments de la nature",
          "Opposer deux notions contraires dans une même phrase",
          "Répéter des termes de plus en plus forts"
        ],
        ans: 1,
        fb: "La personnification est une forme de métaphore qui prête des caractéristiques humaines à des non-humains."
      },
      {
        cat: "Figures de style",
        q: "Laquelle de ces figures consiste à exagérer la réalité pour renforcer une idée ?",
        opts: [
          "Antithèse",
          "Gradation",
          "Hyperbole",
          "Chiasme"
        ],
        ans: 2,
        fb: "L'hyperbole exagère la réalité de façon à frapper l'imagination ou à renforcer l'idée exprimée."
      },
      {
        cat: "Figures de style",
        q: "Une <strong>gradation ascendante</strong> est une énumération de termes…",
        opts: [
          "De moins en moins forts",
          "De même intensité",
          "De plus en plus forts",
          "En ordre alphabétique"
        ],
        ans: 2,
        fb: "La gradation ascendante enchaîne des termes de plus en plus forts pour accroître l'intensité."
      },
      {
        cat: "Figures de style",
        q: "L'<strong>antithèse</strong> permet de…",
        opts: [
          "Atténuer une idée par comparaison",
          "Faire ressortir un contraste saisissant en opposant deux notions contraires",
          "Dire le contraire de ce qu'on pense",
          "Attribuer des traits humains à un objet"
        ],
        ans: 1,
        fb: "L'antithèse oppose deux mots ou expressions contraires pour créer un contraste frappant."
      },
      {
        cat: "Figures de style",
        q: "Un <strong>oxymore</strong> est…",
        opts: [
          "Une exagération de la réalité",
          "Une comparaison avec outil explicite",
          "Une juxtaposition paradoxale de termes contraires (souvent nom + adjectif)",
          "Une énumération de termes croissants"
        ],
        ans: 2,
        fb: "L'oxymore unit deux termes contraires (ex : 'une obscure clarté') souvent sous la forme nom + adjectif épithète."
      },
      {
        cat: "Figures de style",
        q: "L'<strong>antiphrase</strong> est souvent utilisée au service de…",
        opts: [
          "La gradation",
          "L'ironie",
          "La comparaison",
          "La personnification"
        ],
        ans: 1,
        fb: "L'antiphrase dit le contraire de ce qu'on pense et est souvent utilisée pour exprimer l'ironie."
      },
      {
        cat: "Figures de style",
        q: "Quel schéma correspond au <strong>chiasme</strong> ?",
        opts: [
          "AB / AB",
          "AB / BA",
          "AA / BB",
          "A / B / A / B"
        ],
        ans: 1,
        fb: "Le chiasme suit le schéma AB/BA : «Il faut manger pour vivre, et non vivre pour manger.»"
      },
      // === TYPES ET FORMES DE PHRASES ===
      {
        cat: "Types et formes de phrases",
        q: "Une phrase <strong>injonctive</strong> se termine par…",
        opts: [
          "Un point d'interrogation uniquement",
          "Un point ou un point d'exclamation, et donne un ordre",
          "Un point, et donne une information",
          "Un point d'exclamation, et exprime une émotion"
        ],
        ans: 1,
        fb: "La phrase injonctive exprime un ordre et se termine par un point ou un point d'exclamation."
      },
      {
        cat: "Types et formes de phrases",
        q: "«Il vient» est une phrase personnelle, tandis que «Il pleut» est…",
        opts: [
          "Une phrase passive",
          "Une phrase affirmative",
          "Une phrase impersonnelle",
          "Une phrase exclamative"
        ],
        ans: 2,
        fb: "Dans une phrase impersonnelle, le sujet ne représente ni une personne ni un lieu (ex : il pleut, il faut)."
      },
      {
        cat: "Types et formes de phrases",
        q: "«Roxane est aimée par Cyrano» est un exemple de phrase…",
        opts: [
          "Active",
          "Négative",
          "Passive",
          "Impersonnelle"
        ],
        ans: 2,
        fb: "Dans la phrase passive, le sujet subit l'action. Le complément d'agent introduit par 'par' réalise l'action."
      },
      {
        cat: "Types et formes de phrases",
        q: "Quelle forme de phrase est marquée par l'emploi de marques de la négation ?",
        opts: [
          "Phrase exclamative",
          "Phrase négative",
          "Phrase passive",
          "Phrase impersonnelle"
        ],
        ans: 1,
        fb: "La forme négative utilise les marques de la négation (ne…pas, ne…jamais, etc.)."
      }
    ];

    // Shuffle
    function shuffle(arr) {
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      return arr;
    }

    let questions = shuffle([...ALL_QUESTIONS]);
    let current = 0;
    let score = 0;
    let answered = false;

    function renderQuestion() {
      const q = questions[current];
      const total = questions.length;
      document.getElementById('progress-label').textContent = `Question ${current + 1} / ${total}`;
      document.getElementById('progress-bar').style.width = `${((current + 1) / total) * 100}%`;

      const letters = ['A', 'B', 'C', 'D'];
      // Shuffle options while keeping track of correct answer
      const indices = [0, 1, 2, 3];
      shuffle(indices);
      const newAns = indices.indexOf(q.ans);

      let optHTML = '';
      indices.forEach((origIdx, newIdx) => {
        optHTML += `
          <button class="option-btn" onclick="selectAnswer(this, ${newIdx}, ${newAns})">
            <span class="letter">${letters[newIdx]}</span>
            <span>${q.opts[origIdx]}</span>
          </button>`;
      });

      document.getElementById('q-card').innerHTML = `
        <div class="question-meta">
          <span class="q-number">Q${current + 1}</span>
          <span class="q-category">${q.cat}</span>
        </div>
        <div class="question-text">${q.q}</div>
        <div class="options">${optHTML}</div>
        <div class="feedback" id="feedback"></div>
      `;
      document.getElementById('next-btn').disabled = true;
      answered = false;
    }

    function selectAnswer(btn, selected, correct) {
      if (answered) return;
      answered = true;
      const q = questions[current];
      const allBtns = document.querySelectorAll('.option-btn');
      allBtns.forEach(b => b.disabled = true);

      const fb = document.getElementById('feedback');
      if (selected === correct) {
        btn.classList.add('correct');
        score++;
        fb.className = 'feedback correct-fb show';
        fb.innerHTML = `✓ Correct ! ${q.fb}`;
      } else {
        btn.classList.add('wrong');
        allBtns[correct].classList.add('correct');
        fb.className = 'feedback wrong-fb show';
        fb.innerHTML = `✗ Pas tout à fait. ${q.fb}`;
      }
      document.getElementById('next-btn').disabled = false;
    }

    function nextQuestion() {
      current++;
      if (current >= questions.length) {
        showScore();
      } else {
        renderQuestion();
      }
    }

    function showScore() {
      document.getElementById('quiz-area').style.display = 'none';
      const screen = document.getElementById('score-screen');
      screen.classList.add('show');
      const pct = Math.round((score / questions.length) * 100);
      document.getElementById('score-fraction').textContent = `${score} / ${questions.length}`;
      let emoji, msg;
      if (pct >= 90) { emoji = '🏆'; msg = "Excellent travail ! Vous maîtrisez parfaitement ce vocabulaire."; }
      else if (pct >= 70) { emoji = '🎭'; msg = "Très bien ! Quelques révisions encore et vous serez au top."; }
      else if (pct >= 50) { emoji = '📖'; msg = "Pas mal ! Relisez les définitions et retentez le quiz."; }
      else { emoji = '💪'; msg = "Continuez à réviser — une bonne lecture de la fiche et vous progresserez vite !"; }
      document.getElementById('score-emoji').textContent = emoji;
      document.getElementById('score-msg').textContent = msg;
    }

    function restart() {
      questions = shuffle([...ALL_QUESTIONS]);
      current = 0;
      score = 0;
      document.getElementById('score-screen').classList.remove('show');
      document.getElementById('quiz-area').style.display = 'block';
      renderQuestion();
    }

    renderQuestion();
</script>
</body>
</html><script>
(function() {
  var ws = new WebSocket('ws://' + window.location.host + 
             '/jb-server-page?reloadMode=RELOAD_ON_SAVE&'+
             'referrer=' + encodeURIComponent(window.location.pathname));
  ws.onmessage = function (msg) {
      if (msg.data === 'reload') {
          window.location.reload();
      }
      if (msg.data.startsWith('update-css ')) {
          var messageId = msg.data.substring(11);
          var links = document.getElementsByTagName('link');
          for (var i = 0; i < links.length; i++) {
              var link = links[i];
              if (link.rel !== 'stylesheet') continue;
              var clonedLink = link.cloneNode(true);
              var newHref = link.href.replace(/(&|\?)jbUpdateLinksId=\d+/, "$1jbUpdateLinksId=" + messageId);
              if (newHref !== link.href) {
                clonedLink.href = newHref;
              }
              else {
                var indexOfQuest = newHref.indexOf('?');
                if (indexOfQuest >= 0) {
                  // to support ?foo#hash 
                  clonedLink.href = newHref.substring(0, indexOfQuest + 1) + 'jbUpdateLinksId=' + messageId + '&' + 
                                    newHref.substring(indexOfQuest + 1);
                }
                else {
                  clonedLink.href += '?' + 'jbUpdateLinksId=' + messageId;
                }
              }
              link.replaceWith(clonedLink);
          }
      }
  };
})();
</script>
