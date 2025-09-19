<script>
  // --- Data (Plain JavaScript version) -----------------------------------
  const BASE = import.meta.env.BASE_URL; // '/' in dev, '/east-africa-bird-quiz/' on Pages

  const BIRDS = {
    roller: {
      name: "Lilac-breasted Roller",
      img: BASE + "birds/roller.jpg",
      blurb:
        "Showy, joyful, and allergic to beige. You bring color and courage wherever you land."
    },
    fishEagle: {
      name: "Martial Eagle",
      img: BASE + "birds/eagle.jpg",
      blurb:
        "Icon energy. When you speak, people look up. Big voice, bigger heart."
    },
    crownedCrane: {
      name: "Grey Crowned Crane",
      img: BASE + "/birds/crane.jpg",
      blurb:
        "Grace in motion. Loyal, steady, and always a little bit royal."
    },
    shoebill: {
      name: "Shoebill",
      img: BASE + "birds/shoebill.jpg",
      blurb:
        "Mysterious on the outside, marshmallow center. You move slowly and mean it."
    },
    secretarybird: {
      name: "Secretarybird",
      img: BASE +  "birds/secretary.jpg",
      blurb:
        "Long legs, longer stride. Fierce with a flair for drama and perfect eyeliner."
    },
    guineafowl: {
      name: "Helmeted Guineafowl",
      img: BASE + "birds/guinea.jpg",
      blurb:
        "Goofy, social, unstoppable in a squad. Chaos is your love language."
    },
    kingfisher: {
      name: "Malachite Kingfisher",
      img: BASE + "birds/kingfisher.jpg",
      blurb:
        "Tiny jewel of calm. Observant, kind, and quietly dazzling."
    },
    beeEater: {
      name: "Little Bee-eater",
      img: BASE + "birds/bee.jpg",
      blurb:
        "Pocket-sized sunshine. Playful, curious, and always chasing sparkles."
    },
    violetStarling: {
      name: "Violet-backed Starling",
      img: BASE + "birds/violet.jpg",
      blurb:
        "Soft-spoken brilliance. You surprise people with sudden, glorious shimmer."
    },
    superbStarling: {
      name: "Superb Starling",
      img: BASE + "birds/starling.jpg",
      blurb:
        "Sparkly extrovert and community builder. Every gathering is brighter with you."
    }
  };

  const QUESTIONS = [
    {
      text: "How do you make an entrance?",
      options: [
        { label: "Burst of color and flair — heads turn, jaws drop.", birds: ["roller", "violetStarling"] },
        { label: "Loud and proud — you announce yourself before anyone else does.", birds: ["fishEagle", "superbStarling"] },
        { label: "Graceful strut — every step says “royalty.“", birds: ["crownedCrane", "secretarybird"] },
        { label: "Odd but unforgettable — people can’t decide if they should clap or stare.", birds: ["shoebill", "guineafowl"] },
        { label: "Tiny sparkle — you slip in quietly, but the shimmer gives you away.", birds: ["kingfisher", "beeEater"] }
      ]
    },
    {
      text: "What’s your ideal way to spend the weekend?",
      options: [
        { label: "Dramatic adventure — skydiving, dancing, anything that feels epic.", birds: ["roller", "secretarybird"] },
        { label: "By the water — fishing, kayaking, or just chilling by a lake.", birds: ["fishEagle", "kingfisher"] },
        { label: "All dressed up — parties, weddings, anything with fancy food and a spotlight.", birds: ["crownedCrane", "superbStarling"] },
        { label: "Goofing with friends — big messy fun, laughter, and snacks everywhere.", birds: ["guineafowl", "beeEater"] },
        { label: "Alone time — mysterious wanderings, recharging your vibe.", birds: ["shoebill", "violetStarling"] }
      ]
    },
    {
      text: "Pick your spirit snack:",
      options: [
        { label: "Rainbow cupcake with too many sprinkles.", birds: ["roller", "beeEater"] },
        { label: "Grilled fish with lemon — bold and classic.", birds: ["fishEagle", "guineafowl"] },
        { label: "Champagne and hors d’oeuvres.", birds: ["crownedCrane", "violetStarling"] },
        { label: "Weird novelty snack (like a shoe-shaped marshmallow)", birds: ["shoebill", "secretarybird"] },
        { label: "A handful of berries dipped in honey", birds: ["kingfisher", "superbStarling"] }
      ]
    }
    ,
  {
    text: "How do you handle drama?",
    options: [
      { label: "Make it fabulous", birds: ["roller", "superbStarling"] },
      { label: "Shout louder than the rest", birds: ["fishEagle", "secretarybird"] },
      { label: "Stay calm and elegant", birds: ["crownedCrane", "kingfisher"] },
      { label: "Goof around until people laugh", birds: ["guineafowl", "beeEater"] },
      { label: "Give them a stare that ends the fight", birds: ["shoebill", "violetStarling"] }
    ]
  },
  {
    text: "What role do you play in your friend group?",
    options: [
      { label: "The entertainer", birds: ["roller", "beeEater"] },
      { label: "The loud protector", birds: ["fishEagle", "secretarybird"] },
      { label: "The graceful planner", birds: ["crownedCrane", "violetStarling"] },
      { label: "The silly one who keeps it fun", birds: ["guineafowl", "superbStarling"] },
      { label: "The quiet but magnetic presence", birds: ["shoebill", "kingfisher"] }
    ]
  },
  {
    text: "Pick a dream home:",
    options: [
      { label: "Treehouse painted in rainbow colors", birds: ["roller", "violetStarling"] },
      { label: "Lake house with a big porch", birds: ["fishEagle", "kingfisher"] },
      { label: "Palace with a chandelier", birds: ["crownedCrane", "superbStarling"] },
      { label: "Farm with lots of chickens running around", birds: ["guineafowl", "beeEater"] },
      { label: "Cabin deep in a swamp/forest", birds: ["shoebill", "secretarybird"] }
    ]
  }
  ];

  // --- State -------------------------------------------------------------
  let step = 0; // which question index
  let tally = {
    roller: 0,
    fishEagle: 0,
    crownedCrane: 0,
    shoebill: 0,
    secretarybird: 0,
    guineafowl: 0,
    kingfisher: 0,
    beeEater: 0,
    violetStarling: 0,
    superbStarling: 0
  };
  let resultId = null; // store the winner when quiz ends

  function pick(option) {
    option.birds.forEach((id) => (tally[id] = (tally[id] || 0) + 1));
    step += 1;
    if (step === QUESTIONS.length) {
      resultId = winner();
    }
  }

  function reset() {
    step = 0;
    resultId = null;
    Object.keys(tally).forEach((k) => (tally[k] = 0));
  }

  function winner() {
    const entries = Object.entries(tally);
    const max = Math.max(...entries.map(([, v]) => v));
    const tied = entries.filter(([, v]) => v === max).map(([k]) => k);
    return tied[Math.floor(Math.random() * tied.length)];
  }
</script>

<!-- --- UI -------------------------------------------------------------- -->
<div class="wrap">
  <header class="mx">
    <h1>Which East African Bird Are You?</h1>
    <p class="sub">100% Accurate Bird Personality Test - Backed by Science 🐦</p>
    <div class="progress" aria-label="quiz progress">
      <div class="bar" style="width: {(step / QUESTIONS.length) * 100}%"></div>
    </div>
  </header>

  {#if step < QUESTIONS.length}
    <section class="card mx">
      <h2 class="q">{QUESTIONS[step].text}</h2>
      <div class="grid">
        {#each QUESTIONS[step].options as opt}
          <button class="opt" on:click={() => pick(opt)}>{opt.label}</button>
        {/each}
      </div>
      <p class="hint">Pick what feels right, but remember that there are wrong answers.</p>
    </section>
  {:else}
    <section class="result mx">
      <div class="result-card">
        <img class="result-img" src={BIRDS[resultId].img} alt={BIRDS[resultId].name} />
        <h2 class="name">{BIRDS[resultId].name}</h2>
        <p class="blurb">{BIRDS[resultId].blurb}</p>
        <details class="why">
          <summary>Why this match?</summary>
          <ul>
            {#each Object.entries(tally) as [k,v]}
              {#if v > 0}
                <li><strong>{BIRDS[k].name}:</strong> {v} point{v>1?"s":""}</li>
              {/if}
            {/each}
          </ul>
        </details>
        <button class="again" on:click={reset}>Take it again</button>
      </div>
    </section>
  {/if}

  <footer class="mx foot">
    <small>
      This personality test is 1000% accurate and backed by science.
    </small>
  </footer>
</div>

<style>
  :global(html, body) { margin: 0; font-family: system-ui, -apple-system, Segoe UI, Roboto, "DM Sans", Arial, sans-serif; background: #0b0b0b; color: #f5f5f5; }
  .wrap { min-height: 100vh; display: grid; grid-template-rows: auto 1fr auto; }
  .mx { max-width: 760px; margin: 0 auto; padding: 24px; }
  h1 { font-size: 2rem; margin: 16px 0 8px; }
  .sub { opacity: 0.8; margin: 0 0 12px; }
  .progress { width: 100%; height: 8px; background: #222; border-radius: 999px; overflow: hidden; }
  .bar { height: 100%; background: linear-gradient(90deg, #7c3aed, #22d3ee, #f472b6); }

  .card { background: #121212; border: 1px solid #222; border-radius: 16px; box-shadow: 0 10px 30px rgba(0,0,0,0.35); }
  .q { font-size: 1.35rem; margin: 8px 0 12px; }
  .grid { display: grid; gap: 12px; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); }
  .opt { padding: 14px 16px; border-radius: 14px; border: 1px solid #2a2a2a; background: #181818; color: inherit; text-align: left; cursor: pointer; transition: transform .06s ease, border-color .2s ease, background .2s ease; }
  .opt:hover { transform: translateY(-1px); border-color: #3a3a3a; background: #1d1d1d; }
  .hint { opacity: .7; margin: 10px 4px 16px; }

  .result { display: grid; place-items: center; }
  .result-card { background: #121212; border:1px solid #222; border-radius: 18px; padding: 24px; max-width: 680px; text-align: center; box-shadow: 0 10px 30px rgba(0,0,0,.35); }
  .emoji { font-size: 56px; margin-bottom: 8px; }
  .name { font-size: 1.6rem; margin: 0 0 8px; }
  .blurb { opacity: .9; margin: 0 0 14px; }
  details.why { text-align: left; margin: 8px auto 16px; background: #0f0f0f; border: 1px solid #222; border-radius: 12px; padding: 10px 14px; }
  .again { padding: 12px 16px; border-radius: 12px; border: 1px solid #3a3a3a; background: #181818; color: inherit; cursor: pointer; }
  .again:hover { background: #1d1d1d; }
  .foot { opacity: .65; }

  .result-img {
  width: 160px;
  height: 160px;
  object-fit: cover;
  border-radius: 16px;
  margin-bottom: 12px;
  box-shadow: 0 6px 16px rgba(0,0,0,0.4);
}
</style>
