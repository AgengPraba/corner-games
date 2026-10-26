<script>
  let query = '';
  let activeCategory = 'All';

  // Ganti url dengan path file HTML game kamu, misalnya: /games/space-cat/index.html
  // Untuk sementara, game contoh memakai URL # dan berfungsi sebagai placeholder.
  const games = [
    { title: 'Pixel Pouncer', category: 'Platformer', description: 'Lompat, kumpulkan bintang, dan jangan sampai jatuh!', emoji: '🐸', color: 'cover-mint', badge: 'Featured', time: '5 MIN', url: '#', number: '01' },
    { title: 'Snack Attack', category: 'Arcade', description: 'Makan sebanyak mungkin sebelum waktu habis.', emoji: '🍊', color: 'cover-orange', badge: 'New', time: '2 MIN', url: '#', number: '02' },
    { title: 'Cosmic Buddy', category: 'Arcade', description: 'Jelajahi galaksi kecil penuh kejutan dan alien lucu.', emoji: '👾', color: 'cover-blue', badge: '', time: 'ENDLESS', url: '#', number: '03' },
    { title: 'Little Puzzler', category: 'Puzzle', description: 'Putar, cocokkan, dan pecahkan teka-teki mini.', emoji: '🧩', color: 'cover-yellow', badge: '', time: '3 MIN', url: '#', number: '04' },
    { title: 'Bubble Trouble', category: 'Casual', description: 'Pecahkan gelembung warna-warni untuk skor tertinggi.', emoji: '🫧', color: 'cover-lilac', badge: 'New', time: '2 MIN', url: '#', number: '05' },
    { title: 'Mochi Dash', category: 'Platformer', description: 'Bantu si mochi berlari menuju garis akhir.', emoji: '🍡', color: 'cover-pink', badge: '', time: '4 MIN', url: '#', number: '06' }
  ];

  const categories = ['All', 'Arcade', 'Puzzle', 'Platformer', 'Casual'];
  $: filteredGames = games.filter((game) => {
    const matchesCategory = activeCategory === 'All' || game.category === activeCategory;
    const term = query.trim().toLowerCase();
    const matchesQuery = !term || `${game.title} ${game.category} ${game.description}`.toLowerCase().includes(term);
    return matchesCategory && matchesQuery;
  });
</script>

<div class="catalog-tools" aria-label="Search and filter games">
  <label class="search">
    <span aria-hidden="true">⌕</span>
    <input bind:value={query} type="search" placeholder="Find your next favorite..." aria-label="Search games" />
  </label>
  <div class="filters" aria-label="Filter by category">
    {#each categories as category}
      <button class:active={activeCategory === category} class="filter" onclick={() => activeCategory = category} aria-pressed={activeCategory === category}>{category}</button>
    {/each}
  </div>
</div>

<div class="game-grid" aria-live="polite">
  {#each filteredGames as game (game.title)}
    <article class="game-card">
      <a class="game-link" href={game.url} aria-label={`Play ${game.title}`}>
        <div class={`game-cover ${game.color}`}>
          {#if game.badge}<span class:newBadge={game.badge === 'New'} class="game-badge">{game.badge}</span>{/if}
          <span class="cover-art" aria-hidden="true">{game.emoji}</span>
          <span class="cover-number">NO. {game.number}</span>
        </div>
        <div class="game-info">
          <div class="game-title-row"><h3 class="game-title">{game.title}</h3><span class="game-arrow" aria-hidden="true">↗</span></div>
          <p class="game-desc">{game.description}</p>
          <div class="game-meta"><span>{game.category}</span><span>{game.time}</span></div>
        </div>
      </a>
    </article>
  {:else}
    <div class="empty-state">
      <div style="font-size:2rem;margin-bottom:8px">🕹️</div>
      <strong>No games found... yet!</strong>
      <p>Try another search or pick a different category.</p>
      <button class="filter active" onclick={() => { query = ''; activeCategory = 'All'; }}>Show all games</button>
    </div>
  {/each}
</div>
