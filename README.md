[<!doctype html>
<html lang="vi">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Tiến Lên Online PeerJS</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/peerjs/1.5.5/peerjs.min.js"></script>
  <style>
    :root {
      --bg: #0f172a;
      --panel: #111827;
      --panel2: #1f2937;
      --text: #e5e7eb;
      --muted: #9ca3af;
      --accent: #22c55e;
      --danger: #ef4444;
      --warn: #f59e0b;
      --card: #f8fafc;
      --cardText: #111827;
      --red: #dc2626;
      --border: rgba(255,255,255,.12);
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: radial-gradient(circle at top, #1e3a8a 0, var(--bg) 46%);
      color: var(--text);
      min-height: 100vh;
    }

    .app {
      max-width: 1180px;
      margin: 0 auto;
      padding: 18px;
    }

    header {
      display: flex;
      gap: 12px;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      margin-bottom: 14px;
    }

    h1 {
      font-size: clamp(24px, 4vw, 42px);
      margin: 0;
      letter-spacing: -.04em;
    }

    .pill {
      background: rgba(255,255,255,.1);
      border: 1px solid var(--border);
      border-radius: 999px;
      padding: 8px 12px;
      color: var(--muted);
      font-size: 14px;
    }

    .grid {
      display: grid;
      grid-template-columns: 320px 1fr;
      gap: 14px;
    }

    @media (max-width: 850px) {
      .grid { grid-template-columns: 1fr; }
    }

    .panel {
      background: rgba(17, 24, 39, .88);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 14px;
      box-shadow: 0 20px 50px rgba(0,0,0,.25);
      backdrop-filter: blur(10px);
    }

    .panel h2 {
      margin: 0 0 12px;
      font-size: 18px;
    }

    label {
      display: block;
      margin: 10px 0 6px;
      color: var(--muted);
      font-size: 14px;
    }

    input, button, select {
      width: 100%;
](https://anhhai2012creator-coder.github.io/g/)      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 11px 12px;
      font: inherit;
    }

    input, select {
      background: #020617;
      color: var(--text);
      outline: none;
    }

    button {
      background: var(--accent);
      color: #052e16;
      font-weight: 800;
      cursor: pointer;
      transition: transform .12s ease, opacity .12s ease, filter .12s ease;
    }

    button:hover { transform: translateY(-1px); filter: brightness(1.05); }
    button:disabled { opacity: .5; cursor: not-allowed; transform: none; }

    .btn-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-top: 10px;
    }

    .secondary { background: #38bdf8; color: #082f49; }
    .danger { background: var(--danger); color: #450a0a; }
    .warn { background: var(--warn); color: #451a03; }

    .room-code {
      font-size: 28px;
      font-weight: 900;
      letter-spacing: .08em;
      background: #020617;
      border: 1px dashed var(--border);
      border-radius: 16px;
      padding: 12px;
      text-align: center;
      user-select: all;
    }

    .players {
      display: grid;
      gap: 8px;
      margin-top: 12px;
    }

    .player {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: var(--panel2);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 10px;
    }

    .player.active { outline: 2px solid var(--accent); }
    .player .name { font-weight: 800; }
    .player .meta { color: var(--muted); font-size: 13px; }

    .table {
      min-height: 280px;
      display: grid;
      gap: 12px;
    }

    .status {
      background: rgba(2,6,23,.65);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 12px;
      color: var(--muted);
      line-height: 1.45;
    }

    .last-play {
      background: rgba(255,255,255,.08);
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: 14px;
      min-height: 112px;
    }

    .cards {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      align-items: center;
    }

    .card {
      width: 54px;
      height: 76px;
      border-radius: 10px;
      background: var(--card);
      color: var(--cardText);
      border: 2px solid #cbd5e1;
      display: grid;
      place-items: center;
      font-weight: 900;
      box-shadow: 0 8px 18px rgba(0,0,0,.24);
      cursor: pointer;
      user-select: none;
      position: relative;
    }

    .card.red { color: var(--red); }
    .card.selected {
      transform: translateY(-16px);
      border-color: var(--accent);
      box-shadow: 0 12px 26px rgba(34,197,94,.35);
    }

    .card.small {
      width: 44px;
      height: 62px;
      font-size: 14px;
      cursor: default;
      transform: none;
    }

    .card.back {
      background: linear-gradient(135deg, #2563eb, #7c3aed);
      border-color: #93c5fd;
      color: white;
    }

    .hand-wrap {
      margin-top: 12px;
      background: rgba(2,6,23,.5);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 14px;
    }

    .controls {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin-top: 12px;
    }

    @media (max-width: 620px) {
      .controls { grid-template-columns: 1fr; }
      .card { width: 46px; height: 66px; font-size: 14px; }
    }

    .log {
      height: 180px;
      overflow: auto;
      display: grid;
      gap: 6px;
      font-size: 13px;
      color: var(--muted);
      background: #020617;
      border-radius: 14px;
      padding: 10px;
      border: 1px solid var(--border);
    }

    .hidden { display: none !important; }
    .note { color: var(--muted); font-size: 13px; line-height: 1.45; }
    .ok { color: #86efac; }
    .bad { color: #fca5a5; }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <div>
        <h1>Tiến Lên Online</h1>
        <div class="pill">GitHub Pages + PeerJS + mã phòng</div>
      </div>
      <div class="pill" id="netStatus">Chưa kết nối</div>
    </header>

    <div class="grid">
      <aside class="panel">
        <h2>Phòng chơi</h2>
        <label>Tên của bạn</label>
        <input id="nameInput" maxlength="18" placeholder="Ví dụ: Hải" />

        <div class="btn-row">
          <button id="createBtn">Tạo phòng</button>
          <button class="secondary" id="joinBtn">Vào phòng</button>
        </div>

        <label>Mã phòng</label>
        <input id="roomInput" maxlength="12" placeholder="Nhập mã phòng" />
        <div class="room-code hidden" id="roomCodeBox"></div>

        <p class="note">
          Người tạo phòng bấm “Tạo phòng”, gửi mã cho bạn bè. Người khác nhập mã rồi bấm “Vào phòng”. Nên chơi 2–4 người.
        </p>

        <div class="btn-row">
          <button class="warn" id="startBtn" disabled>Bắt đầu</button>
          <button class="danger" id="resetBtn" disabled>Ván mới</button>
        </div>

        <h2 style="margin-top:18px">Người chơi</h2>
        <div class="players" id="playersBox"></div>
      </aside>

      <main class="panel table">
        <div class="status" id="statusBox">
          Tạo phòng hoặc vào phòng để bắt đầu.
        </div>

        <section class="last-play">
          <h2>Bài vừa đánh</h2>
          <div id="lastPlayInfo" class="note">Chưa có lượt đánh.</div>
          <div class="cards" id="lastCards"></div>
        </section>

        <section class="hand-wrap">
          <h2>Bài của bạn</h2>
          <div class="cards" id="handBox"></div>
          <div class="controls">
            <button id="playBtn" disabled>Đánh bài</button>
            <button class="secondary" id="passBtn" disabled>Bỏ lượt</button>
            <button class="warn" id="sortBtn">Sắp xếp</button>
          </div>
        </section>

        <section>
          <h2>Nhật ký</h2>
          <div class="log" id="logBox"></div>
        </section>
      </main>
    </div>
  </div>

  <script>
    const $ = (id) => document.getElementById(id);

    const SUITS = ["♠", "♣", "♦", "♥"];
    const RANKS = ["3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"];
    const SUIT_POWER = { "♠": 0, "♣": 1, "♦": 2, "♥": 3 };

    let peer = null;
    let isHost = false;
    let roomCode = "";
    let myId = "";
    let myName = "";
    let selected = new Set();
    let connections = new Map();

    let state = freshState();

    function freshState() {
      return {
        phase: "lobby",
        hostId: "",
        players: [],
        hands: {},
        turn: 0,
        lastPlay: null,
        passes: [],
        winnerIds: [],
        log: []
      };
    }

    function roomId(code) {
      return "tl-" + code.trim().toLowerCase().replace(/[^a-z0-9]/g, "");
    }

    function makeRoomCode() {
      const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      let out = "";
      for (let i = 0; i < 5; i++) out += chars[Math.floor(Math.random() * chars.length)];
      return out;
    }

    function addLog(msg) {
      const time = new Date().toLocaleTimeString("vi-VN", { hour: "2-digit", minute: "2-digit" });
      state.log.unshift(`[${time}] ${msg}`);
      state.log = state.log.slice(0, 80);
    }

    function logLocal(msg) {
      const time = new Date().toLocaleTimeString("vi-VN", { hour: "2-digit", minute: "2-digit" });
      state.log.unshift(`[${time}] ${msg}`);
      render();
    }

    function normalizeName() {
      return ($("nameInput").value || "Người chơi").trim().slice(0, 18) || "Người chơi";
    }

    function send(conn, type, payload = {}) {
      if (conn && conn.open) conn.send({ type, payload });
    }

    function broadcast(type, payload = {}) {
      for (const conn of connections.values()) send(conn, type, payload);
    }

    function syncAll() {
      if (!isHost) return;
      broadcast("state", publicState());
      render();
    }

    function publicState() {
      const clone = JSON.parse(JSON.stringify(state));
      for (const p of clone.players) {
        if (p.id !== myId) clone.hands[p.id] = Array(clone.hands[p.id]?.length || 0).fill({ back: true });
      }
      return clone;
    }

    function stateForPlayer(playerId) {
      const clone = JSON.parse(JSON.stringify(state));
      for (const p of clone.players) {
        if (p.id !== playerId) clone.hands[p.id] = Array(clone.hands[p.id]?.length || 0).fill({ back: true });
      }
      return clone;
    }

    function syncTo(conn, playerId) {
      send(conn, "state", stateForPlayer(playerId));
    }

    function createDeck() {
      const deck = [];
      for (const rank of RANKS) {
        for (const suit of SUITS) {
          deck.push({ rank, suit, id: rank + suit });
        }
      }
      return deck;
    }

    function cardValue(card) {
      return RANKS.indexOf(card.rank) * 4 + SUIT_POWER[card.suit];
    }

    function rankValue(card) {
      return RANKS.indexOf(card.rank);
    }

    function sortCards(cards) {
      return [...cards].sort((a, b) => cardValue(a) - cardValue(b));
    }

    function shuffle(arr) {
      const a = [...arr];
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    }

    function secretlyGiveBoFourOfAKind(deck) {
      const boPlayer = state.players.find(p => p.name.trim().toLowerCase() === "bo");
      if (!boPlayer) return deck;

      const ranks = RANKS.filter(r => r !== "2");
      const rank = ranks[Math.floor(Math.random() * ranks.length)];
      const fourCards = SUITS.map(suit => ({ rank, suit, id: rank + suit }));
      const fourIds = new Set(fourCards.map(c => c.id));
      const rest = deck.filter(c => !fourIds.has(c.id));

      const boIndex = state.players.findIndex(p => p.id === boPlayer.id);
      const playerCount = state.players.length;
      const fixedDeck = [];
      let restIndex = 0;
      let fourIndex = 0;

      for (let round = 0; round < 13; round++) {
        for (let playerIndex = 0; playerIndex < playerCount; playerIndex++) {
          if (playerIndex === boIndex && fourIndex < fourCards.length) {
            fixedDeck.push(fourCards[fourIndex++]);
          } else {
            fixedDeck.push(rest[restIndex++]);
          }
        }
      }

      while (restIndex < rest.length) fixedDeck.push(rest[restIndex++]);
      return fixedDeck;
    }

    function sameRank(cards) {
      return cards.every(c => c.rank === cards[0].rank);
    }

    function isConsecutiveRank(values) {
      for (let i = 1; i < values.length; i++) {
        if (values[i] !== values[i - 1] + 1) return false;
      }
      return true;
    }

    function analyze(cards) {
      cards = sortCards(cards);
      if (!cards.length) return null;
      const n = cards.length;
      const ranks = cards.map(rankValue);
      const uniqueRanks = [...new Set(ranks)];
      const high = cards[cards.length - 1];

      if (n === 1) return { type: "single", size: 1, high, power: cardValue(high) };
      if (n === 2 && sameRank(cards)) return { type: "pair", size: 2, high, power: cardValue(high) };
      if (n === 3 && sameRank(cards)) return { type: "triple", size: 3, high, power: cardValue(high) };

      const hasTwo = ranks.includes(RANKS.indexOf("2"));
      if (n >= 3 && uniqueRanks.length === n && !hasTwo && isConsecutiveRank(ranks)) {
        return { type: "straight", size: n, high, power: rankValue(high) };
      }

      if (n % 2 === 0 && n >= 6 && !hasTwo) {
        const pairs = [];
        for (let i = 0; i < n; i += 2) {
          if (cards[i].rank !== cards[i + 1].rank) return null;
          pairs.push(rankValue(cards[i]));
        }
        if (isConsecutiveRank(pairs)) {
          return { type: "pairStraight", size: n, pairs: n / 2, high, power: rankValue(high) };
        }
      }

      if (n === 4 && sameRank(cards)) return { type: "four", size: 4, high, power: rankValue(high) };
      return null;
    }

    function canBeat(play, last) {
      if (!last) return true;
      if (play.type === last.type && play.size === last.size) return play.power > last.power;

      // Luật chặt đơn giản kiểu miền Nam:
      // Tứ quý chặt 1 lá 2 hoặc đôi 2. Ba đôi thông chặt 1 lá 2.
      if (play.type === "four" && last.type === "single" && last.high.rank === "2") return true;
      if (play.type === "four" && last.type === "pair" && last.high.rank === "2") return true;
      if (play.type === "pairStraight" && play.pairs >= 3 && last.type === "single" && last.high.rank === "2") return true;
      if (play.type === "pairStraight" && last.type === "pairStraight" && play.pairs === last.pairs) return play.power > last.power;
      return false;
    }

    function currentPlayer() {
      return state.players[state.turn];
    }

    function alivePlayers() {
      return state.players.filter(p => !state.winnerIds.includes(p.id));
    }

    function advanceTurn() {
      const alive = alivePlayers();
      if (alive.length <= 1) return;
      for (let i = 1; i <= state.players.length; i++) {
        const next = (state.turn + i) % state.players.length;
        const p = state.players[next];
        if (!state.winnerIds.includes(p.id)) {
          state.turn = next;
          return;
        }
      }
    }

    function resetRoundIfNeeded() {
      const alive = alivePlayers();
      if (!state.lastPlay) return;
      const activeIds = alive.map(p => p.id);
      const passedCount = state.passes.filter(id => activeIds.includes(id) && id !== state.lastPlay.playerId).length;
      if (passedCount >= Math.max(0, alive.length - 1)) {
        const leadIndex = state.players.findIndex(p => p.id === state.lastPlay.playerId && !state.winnerIds.includes(p.id));
        state.turn = leadIndex >= 0 ? leadIndex : state.turn;
        state.lastPlay = null;
        state.passes = [];
        addLog("Vòng mới: người thắng lượt trước được đánh bất kỳ.");
      }
    }

    function hostStartGame() {
      if (!isHost) return;
      if (state.players.length < 2) return alert("Cần ít nhất 2 người chơi.");
      state.phase = "playing";
      state.hands = {};
      state.lastPlay = null;
      state.passes = [];
      state.winnerIds = [];

      let deck = shuffle(createDeck());
      deck = secretlyGiveBoFourOfAKind(deck);
      state.players.forEach(p => state.hands[p.id] = []);

      for (let round = 0; round < 13; round++) {
        for (const p of state.players) {
          const card = deck.shift();
          if (card) state.hands[p.id].push(card);
        }
      }

      for (const p of state.players) state.hands[p.id] = sortCards(state.hands[p.id]);

      let firstId = state.players[0].id;
      for (const p of state.players) {
        if (state.hands[p.id].some(c => c.rank === "3" && c.suit === "♠")) firstId = p.id;
      }
      state.turn = state.players.findIndex(p => p.id === firstId);
      addLog("Bắt đầu ván. Người có 3♠ đi trước.");
      syncAllPerPlayer();
    }

    function syncAllPerPlayer() {
      if (!isHost) return;
      for (const [pid, conn] of connections.entries()) syncTo(conn, pid);
      render();
    }

    function hostPlay(playerId, cardIds) {
      if (!isHost || state.phase !== "playing") return;
      const player = currentPlayer();
      if (!player || player.id !== playerId) return syncAllPerPlayer();

      const hand = state.hands[playerId] || [];
      const chosen = hand.filter(c => cardIds.includes(c.id));
      if (chosen.length !== cardIds.length) return;

      const play = analyze(chosen);
      if (!play) return reject(playerId, "Bộ bài không hợp lệ.");
      if (!canBeat(play, state.lastPlay)) return reject(playerId, "Bài chưa đủ lớn để đè lượt trước.");

      state.hands[playerId] = hand.filter(c => !cardIds.includes(c.id));
      state.lastPlay = { ...play, cards: chosen, playerId, playerName: player.name };
      state.passes = [];
      addLog(`${player.name} đánh ${chosen.map(cardLabel).join(" ")}.`);

      if (state.hands[playerId].length === 0 && !state.winnerIds.includes(playerId)) {
        state.winnerIds.push(playerId);
        addLog(`${player.name} đã hết bài!`);
      }

      const alive = alivePlayers();
      if (alive.length <= 1) {
        if (alive[0] && !state.winnerIds.includes(alive[0].id)) state.winnerIds.push(alive[0].id);
        state.phase = "ended";
        addLog("Ván đấu kết thúc.");
      } else {
        advanceTurn();
      }
      syncAllPerPlayer();
    }

    function hostPass(playerId) {
      if (!isHost || state.phase !== "playing") return;
      const player = currentPlayer();
      if (!player || player.id !== playerId) return syncAllPerPlayer();
      if (!state.lastPlay) return reject(playerId, "Đầu vòng không được bỏ lượt.");
      if (!state.passes.includes(playerId)) state.passes.push(playerId);
      addLog(`${player.name} bỏ lượt.`);
      advanceTurn();
      resetRoundIfNeeded();
      syncAllPerPlayer();
    }

    function reject(playerId, reason) {
      if (playerId === myId) alert(reason);
      else send(connections.get(playerId), "reject", { reason });
    }

    function cardLabel(c) {
      return c.back ? "🂠" : `${c.rank}${c.suit}`;
    }

    function setupConn(conn) {
      conn.on("open", () => {
        connections.set(conn.peer, conn);
        render();
      });
      conn.on("data", msg => handleMessage(conn, msg));
      conn.on("close", () => {
        connections.delete(conn.peer);
        if (isHost) {
          const p = state.players.find(x => x.id === conn.peer);
          if (p) addLog(`${p.name} mất kết nối.`);
          syncAllPerPlayer();
        } else {
          logLocal("Mất kết nối với chủ phòng.");
        }
      });
      conn.on("error", err => {
        console.error(err);
        alert("Lỗi kết nối phòng. Hãy kiểm tra mã phòng và bảo đảm chủ phòng đang mở tab.");
      });
    }

    function handleMessage(conn, msg) {
      if (!msg || !msg.type) return;
      const { type, payload } = msg;

      if (isHost) {
        if (type === "join") {
          if (state.phase !== "lobby") return send(conn, "reject", { reason: "Phòng đã bắt đầu ván." });
          if (state.players.length >= 4) return send(conn, "reject", { reason: "Phòng đã đủ 4 người." });
          if (!state.players.some(p => p.id === conn.peer)) {
            state.players.push({ id: conn.peer, name: payload.name || "Người chơi" });
            addLog(`${payload.name || "Người chơi"} vào phòng.`);
          }
          syncAllPerPlayer();
        }
        if (type === "play") hostPlay(conn.peer, payload.cardIds || []);
        if (type === "pass") hostPass(conn.peer);
        if (type === "chatlog") addLog(payload.text || "");
        return;
      }

      if (type === "state") {
        state = payload;
        selected.clear();
        render();
      }
      if (type === "reject") alert(payload.reason || "Yêu cầu bị từ chối.");
    }

    function render() {
      $("netStatus").textContent = peer ? `Peer: ${myId || "đang mở..."}` : "Chưa kết nối";
      $("roomCodeBox").classList.toggle("hidden", !roomCode);
      $("roomCodeBox").textContent = roomCode;
      $("startBtn").disabled = !(isHost && state.phase === "lobby" && state.players.length >= 2);
      $("resetBtn").disabled = !isHost;

      const playersBox = $("playersBox");
      playersBox.innerHTML = "";
      for (const p of state.players) {
        const div = document.createElement("div");
        div.className = "player" + (currentPlayer()?.id === p.id ? " active" : "");
        const order = state.winnerIds.indexOf(p.id);
        div.innerHTML = `<div><div class="name">${escapeHtml(p.name)}${p.id === myId ? " (Bạn)" : ""}</div><div class="meta">${order >= 0 ? "Về thứ " + (order + 1) : "Đang chơi"}</div></div><div>${(state.hands[p.id] || []).length} lá</div>`;
        playersBox.appendChild(div);
      }

      const active = currentPlayer();
      const winners = state.winnerIds.map(id => state.players.find(p => p.id === id)?.name).filter(Boolean);
      $("statusBox").innerHTML = statusText(active, winners);

      const lastCards = $("lastCards");
      lastCards.innerHTML = "";
      if (state.lastPlay) {
        $("lastPlayInfo").textContent = `${state.lastPlay.playerName} vừa đánh.`;
        for (const c of state.lastPlay.cards) lastCards.appendChild(cardEl(c, false, true));
      } else {
        $("lastPlayInfo").textContent = state.phase === "playing" ? "Đầu vòng: có thể đánh bất kỳ bộ hợp lệ." : "Chưa có lượt đánh.";
      }

      const handBox = $("handBox");
      handBox.innerHTML = "";
      const myHand = sortCards(state.hands[myId] || []);
      for (const c of myHand) handBox.appendChild(cardEl(c, true));

      const myTurn = state.phase === "playing" && active?.id === myId;
      $("playBtn").disabled = !myTurn || selected.size === 0;
      $("passBtn").disabled = !myTurn || !state.lastPlay;

      $("logBox").innerHTML = state.log.map(x => `<div>${escapeHtml(x)}</div>`).join("");
    }

    function statusText(active, winners) {
      if (state.phase === "lobby") return `Đang chờ người chơi. Chủ phòng bấm <b>Bắt đầu</b> khi đủ người.`;
      if (state.phase === "ended") return `<b class="ok">Ván kết thúc.</b><br>Kết quả: ${winners.map(escapeHtml).join(" → ") || "chưa có"}.`;
      const turnName = active ? escapeHtml(active.name) : "?";
      const yourTurn = active?.id === myId ? "<b class='ok'>Đến lượt bạn.</b>" : `Đến lượt <b>${turnName}</b>.`;
      return `${yourTurn}<br>Chọn bài rồi bấm <b>Đánh bài</b>. Bộ hỗ trợ: lẻ, đôi, sám, sảnh, ba đôi thông trở lên, tứ quý.`;
    }

    function cardEl(c, clickable, small = false) {
      const div = document.createElement("div");
      div.className = "card" + (c.suit === "♦" || c.suit === "♥" ? " red" : "") + (selected.has(c.id) ? " selected" : "") + (small ? " small" : "") + (c.back ? " back" : "");
      div.textContent = cardLabel(c);
      if (clickable && !c.back) {
        div.onclick = () => {
          if (selected.has(c.id)) selected.delete(c.id);
          else selected.add(c.id);
          render();
        };
      }
      return div;
    }

    function escapeHtml(str) {
      return String(str).replace(/[&<>"]/g, s => ({ "&":"&amp;", "<":"&lt;", ">":"&gt;", '"':"&quot;" }[s]));
    }

    function hostAddSelf() {
      state = freshState();
      state.hostId = myId;
      state.players = [{ id: myId, name: myName }];
      addLog(`${myName} tạo phòng.`);
    }

    $("createBtn").onclick = () => {
      myName = normalizeName();
      roomCode = makeRoomCode();
      myId = roomId(roomCode);
      isHost = true;
      connections.clear();
      selected.clear();
      if (peer) peer.destroy();
      peer = new Peer(myId, { debug: 1 });
      peer.on("open", id => {
        myId = id;
        hostAddSelf();
        render();
      });
      peer.on("connection", conn => setupConn(conn));
      peer.on("error", err => {
        alert("Không tạo được phòng. Thử lại mã khác. " + (err.type || ""));
        console.error(err);
      });
    };

    $("joinBtn").onclick = () => {
      myName = normalizeName();
      roomCode = ($("roomInput").value || "").trim().toUpperCase();
      if (!roomCode) return alert("Nhập mã phòng trước.");
      isHost = false;
      connections.clear();
      selected.clear();
      state = freshState();
      if (peer) peer.destroy();
      peer = new Peer(undefined, { debug: 1 });
      peer.on("open", id => {
        myId = id;
        const hostId = roomId(roomCode);
        const conn = peer.connect(hostId, { reliable: true });
        setupConn(conn);

        const sendJoin = () => send(conn, "join", { name: myName });
        conn.on("open", sendJoin);
        setTimeout(() => {
          if (conn.open && state.players.length === 0) sendJoin();
        }, 700);
        setTimeout(() => {
          if (state.players.length === 0) {
            alert("Chưa vào được phòng. Kiểm tra đúng mã, chủ phòng còn mở tab, rồi bấm Vào phòng lại.");
          }
        }, 5000);
        render();
      });
      peer.on("error", err => {
        alert("Không kết nối được phòng. Kiểm tra mã hoặc thử tải lại trang. " + (err.type || ""));
        console.error(err);
      });
    };

    $("startBtn").onclick = hostStartGame;
    $("resetBtn").onclick = () => {
      if (!isHost) return;
      hostStartGame();
    };

    $("playBtn").onclick = () => {
      const ids = [...selected];
      if (isHost) hostPlay(myId, ids);
      else {
        const hostConn = [...connections.values()][0];
        send(hostConn, "play", { cardIds: ids });
      }
      selected.clear();
      render();
    };

    $("passBtn").onclick = () => {
      if (isHost) hostPass(myId);
      else {
        const hostConn = [...connections.values()][0];
        send(hostConn, "pass", {});
      }
    };

    $("sortBtn").onclick = () => {
      if (state.hands[myId]) state.hands[myId] = sortCards(state.hands[myId]);
      render();
    };

    render();
  </script>
</body>
</html>
      background: #020617;
      color: var(--text);
      outline: none;
    }

    button {
      background: var(--accent);
      color: #052e16;
      font-weight: 800;
      cursor: pointer;
      transition: transform .12s ease, opacity .12s ease, filter .12s ease;
    }

    button:hover { transform: translateY(-1px); filter: brightness(1.05); }
    button:disabled { opacity: .5; cursor: not-allowed; transform: none; }

    .btn-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-top: 10px;
    }

    .secondary { background: #38bdf8; color: #082f49; }
    .danger { background: var(--danger); color: #450a0a; }
    .warn { background: var(--warn); color: #451a03; }

    .room-code {
      font-size: 28px;
      font-weight: 900;
      letter-spacing: .08em;
      background: #020617;
      border: 1px dashed var(--border);
      border-radius: 16px;
      padding: 12px;
      text-align: center;
      user-select: all;
    }

    .players {
      display: grid;
      gap: 8px;
      margin-top: 12px;
    }

    .player {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: var(--panel2);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 10px;
    }

    .player.active { outline: 2px solid var(--accent); }
    .player .name { font-weight: 800; }
    .player .meta { color: var(--muted); font-size: 13px; }

    .table {
      min-height: 280px;
      display: grid;
      gap: 12px;
    }

    .status {
      background: rgba(2,6,23,.65);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 12px;
      color: var(--muted);
      line-height: 1.45;
    }

    .last-play {
      background: rgba(255,255,255,.08);
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: 14px;
      min-height: 112px;
    }

    .cards {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      align-items: center;
    }

    .card {
      width: 54px;
      height: 76px;
      border-radius: 10px;
      background: var(--card);
      color: var(--cardText);
      border: 2px solid #cbd5e1;
      display: grid;
      place-items: center;
      font-weight: 900;
      box-shadow: 0 8px 18px rgba(0,0,0,.24);
      cursor: pointer;
      user-select: none;
      position: relative;
    }

    .card.red { color: var(--red); }
    .card.selected {
      transform: translateY(-16px);
      border-color: var(--accent);
      box-shadow: 0 12px 26px rgba(34,197,94,.35);
    }

    .card.small {
      width: 44px;
      height: 62px;
      font-size: 14px;
      cursor: default;
      transform: none;
    }

    .card.back {
      background: linear-gradient(135deg, #2563eb, #7c3aed);
      border-color: #93c5fd;
      color: white;
    }

    .hand-wrap {
      margin-top: 12px;
      background: rgba(2,6,23,.5);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 14px;
    }

    .controls {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin-top: 12px;
    }

    @media (max-width: 620px) {
      .controls { grid-template-columns: 1fr; }
      .card { width: 46px; height: 66px; font-size: 14px; }
    }

    .log {
      height: 180px;
      overflow: auto;
      display: grid;
      gap: 6px;
      font-size: 13px;
      color: var(--muted);
      background: #020617;
      border-radius: 14px;
      padding: 10px;
      border: 1px solid var(--border);
    }

    .hidden { display: none !important; }
    .note { color: var(--muted); font-size: 13px; line-height: 1.45; }
    .ok { color: #86efac; }
    .bad { color: #fca5a5; }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <div>
        <h1>Tiến Lên Online</h1>
        <div class="pill">GitHub Pages + PeerJS + mã phòng</div>
      </div>
      <div class="pill" id="netStatus">Chưa kết nối</div>
    </header>

    <div class="grid">
      <aside class="panel">
        <h2>Phòng chơi</h2>
        <label>Tên của bạn</label>
        <input id="nameInput" maxlength="18" placeholder="Ví dụ: Hải" />

        <div class="btn-row">
          <button id="createBtn">Tạo phòng</button>
          <button class="secondary" id="joinBtn">Vào phòng</button>
        </div>

        <label>Mã phòng</label>
        <input id="roomInput" maxlength="12" placeholder="Nhập mã phòng" />
        <div class="room-code hidden" id="roomCodeBox"></div>

        <p class="note">
          Người tạo phòng bấm “Tạo phòng”, gửi mã cho bạn bè. Người khác nhập mã rồi bấm “Vào phòng”. Nên chơi 2–4 người.
        </p>

        <div class="btn-row">
          <button class="warn" id="startBtn" disabled>Bắt đầu</button>
          <button class="danger" id="resetBtn" disabled>Ván mới</button>
        </div>

        <h2 style="margin-top:18px">Người chơi</h2>
        <div class="players" id="playersBox"></div>
      </aside>

      <main class="panel table">
        <div class="status" id="statusBox">
          Tạo phòng hoặc vào phòng để bắt đầu.
        </div>

        <section class="last-play">
          <h2>Bài vừa đánh</h2>
          <div id="lastPlayInfo" class="note">Chưa có lượt đánh.</div>
          <div class="cards" id="lastCards"></div>
        </section>

        <section class="hand-wrap">
          <h2>Bài của bạn</h2>
          <div class="cards" id="handBox"></div>
          <div class="controls">
            <button id="playBtn" disabled>Đánh bài</button>
            <button class="secondary" id="passBtn" disabled>Bỏ lượt</button>
            <button class="warn" id="sortBtn">Sắp xếp</button>
          </div>
        </section>

        <section>
          <h2>Nhật ký</h2>
          <div class="log" id="logBox"></div>
        </section>
      </main>
    </div>
  </div>

  <script>
    const $ = (id) => document.getElementById(id);

    const SUITS = ["♠", "♣", "♦", "♥"];
    const RANKS = ["3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"];
    const SUIT_POWER = { "♠": 0, "♣": 1, "♦": 2, "♥": 3 };

    let peer = null;
    let isHost = false;
    let roomCode = "";
    let myId = "";
    let myName = "";
    let selected = new Set();
    let connections = new Map();

    let state = freshState();

    function freshState() {
      return {
        phase: "lobby",
        hostId: "",
        players: [],
        hands: {},
        turn: 0,
        lastPlay: null,
        passes: [],
        winnerIds: [],
        log: []
      };
    }

    function roomId(code) {
      return "tl-" + code.trim().toUpperCase();
    }

    function makeRoomCode() {
      const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      let out = "";
      for (let i = 0; i < 5; i++) out += chars[Math.floor(Math.random() * chars.length)];
      return out;
    }

    function addLog(msg) {
      const time = new Date().toLocaleTimeString("vi-VN", { hour: "2-digit", minute: "2-digit" });
      state.log.unshift(`[${time}] ${msg}`);
      state.log = state.log.slice(0, 80);
    }

    function logLocal(msg) {
      const time = new Date().toLocaleTimeString("vi-VN", { hour: "2-digit", minute: "2-digit" });
      state.log.unshift(`[${time}] ${msg}`);
      render();
    }

    function normalizeName() {
      return ($("nameInput").value || "Người chơi").trim().slice(0, 18) || "Người chơi";
    }

    function send(conn, type, payload = {}) {
      if (conn && conn.open) conn.send({ type, payload });
    }

    function broadcast(type, payload = {}) {
      for (const conn of connections.values()) send(conn, type, payload);
    }

    function syncAll() {
      if (!isHost) return;
      broadcast("state", publicState());
      render();
    }

    function publicState() {
      const clone = JSON.parse(JSON.stringify(state));
      for (const p of clone.players) {
        if (p.id !== myId) clone.hands[p.id] = Array(clone.hands[p.id]?.length || 0).fill({ back: true });
      }
      return clone;
    }

    function stateForPlayer(playerId) {
      const clone = JSON.parse(JSON.stringify(state));
      for (const p of clone.players) {
        if (p.id !== playerId) clone.hands[p.id] = Array(clone.hands[p.id]?.length || 0).fill({ back: true });
      }
      return clone;
    }

    function syncTo(conn, playerId) {
      send(conn, "state", stateForPlayer(playerId));
    }

    function createDeck() {
      const deck = [];
      for (const rank of RANKS) {
        for (const suit of SUITS) {
          deck.push({ rank, suit, id: rank + suit });
        }
      }
      return deck;
    }

    function cardValue(card) {
      return RANKS.indexOf(card.rank) * 4 + SUIT_POWER[card.suit];
    }

    function rankValue(card) {
      return RANKS.indexOf(card.rank);
    }

    function sortCards(cards) {
      return [...cards].sort((a, b) => cardValue(a) - cardValue(b));
    }

    function shuffle(arr) {
      const a = [...arr];
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    }

    function secretlyGiveBoFourOfAKind(deck) {
      const boPlayer = state.players.find(p => p.name.trim().toLowerCase() === "bo");
      if (!boPlayer) return deck;

      const ranks = RANKS.filter(r => r !== "2");
      const rank = ranks[Math.floor(Math.random() * ranks.length)];
      const fourCards = SUITS.map(suit => ({ rank, suit, id: rank + suit }));
      const fourIds = new Set(fourCards.map(c => c.id));
      const rest = deck.filter(c => !fourIds.has(c.id));

      const boIndex = state.players.findIndex(p => p.id === boPlayer.id);
      const playerCount = state.players.length;
      const fixedDeck = [];
      let restIndex = 0;
      let fourIndex = 0;

      for (let round = 0; round < 13; round++) {
        for (let playerIndex = 0; playerIndex < playerCount; playerIndex++) {
          if (playerIndex === boIndex && fourIndex < fourCards.length) {
            fixedDeck.push(fourCards[fourIndex++]);
          } else {
            fixedDeck.push(rest[restIndex++]);
          }
        }
      }

      while (restIndex < rest.length) fixedDeck.push(rest[restIndex++]);
      return fixedDeck;
    }

    function sameRank(cards) {
      return cards.every(c => c.rank === cards[0].rank);
    }

    function isConsecutiveRank(values) {
      for (let i = 1; i < values.length; i++) {
        if (values[i] !== values[i - 1] + 1) return false;
      }
      return true;
    }

    function analyze(cards) {
      cards = sortCards(cards);
      if (!cards.length) return null;
      const n = cards.length;
      const ranks = cards.map(rankValue);
      const uniqueRanks = [...new Set(ranks)];
      const high = cards[cards.length - 1];

      if (n === 1) return { type: "single", size: 1, high, power: cardValue(high) };
      if (n === 2 && sameRank(cards)) return { type: "pair", size: 2, high, power: cardValue(high) };
      if (n === 3 && sameRank(cards)) return { type: "triple", size: 3, high, power: cardValue(high) };

      const hasTwo = ranks.includes(RANKS.indexOf("2"));
      if (n >= 3 && uniqueRanks.length === n && !hasTwo && isConsecutiveRank(ranks)) {
        return { type: "straight", size: n, high, power: rankValue(high) };
      }

      if (n % 2 === 0 && n >= 6 && !hasTwo) {
        const pairs = [];
        for (let i = 0; i < n; i += 2) {
          if (cards[i].rank !== cards[i + 1].rank) return null;
          pairs.push(rankValue(cards[i]));
        }
        if (isConsecutiveRank(pairs)) {
          return { type: "pairStraight", size: n, pairs: n / 2, high, power: rankValue(high) };
        }
      }

      if (n === 4 && sameRank(cards)) return { type: "four", size: 4, high, power: rankValue(high) };
      return null;
    }

    function canBeat(play, last) {
      if (!last) return true;
      if (play.type === last.type && play.size === last.size) return play.power > last.power;

      // Luật chặt đơn giản kiểu miền Nam:
      // Tứ quý chặt 1 lá 2 hoặc đôi 2. Ba đôi thông chặt 1 lá 2.
      if (play.type === "four" && last.type === "single" && last.high.rank === "2") return true;
      if (play.type === "four" && last.type === "pair" && last.high.rank === "2") return true;
      if (play.type === "pairStraight" && play.pairs >= 3 && last.type === "single" && last.high.rank === "2") return true;
      if (play.type === "pairStraight" && last.type === "pairStraight" && play.pairs === last.pairs) return play.power > last.power;
      return false;
    }

    function currentPlayer() {
      return state.players[state.turn];
    }

    function alivePlayers() {
      return state.players.filter(p => !state.winnerIds.includes(p.id));
    }

    function advanceTurn() {
      const alive = alivePlayers();
      if (alive.length <= 1) return;
      for (let i = 1; i <= state.players.length; i++) {
        const next = (state.turn + i) % state.players.length;
        const p = state.players[next];
        if (!state.winnerIds.includes(p.id)) {
          state.turn = next;
          return;
        }
      }
    }

    function resetRoundIfNeeded() {
      const alive = alivePlayers();
      if (!state.lastPlay) return;
      const activeIds = alive.map(p => p.id);
      const passedCount = state.passes.filter(id => activeIds.includes(id) && id !== state.lastPlay.playerId).length;
      if (passedCount >= Math.max(0, alive.length - 1)) {
        const leadIndex = state.players.findIndex(p => p.id === state.lastPlay.playerId && !state.winnerIds.includes(p.id));
        state.turn = leadIndex >= 0 ? leadIndex : state.turn;
        state.lastPlay = null;
        state.passes = [];
        addLog("Vòng mới: người thắng lượt trước được đánh bất kỳ.");
      }
    }

    function hostStartGame() {
      if (!isHost) return;
      if (state.players.length < 2) return alert("Cần ít nhất 2 người chơi.");
      state.phase = "playing";
      state.hands = {};
      state.lastPlay = null;
      state.passes = [];
      state.winnerIds = [];

      let deck = shuffle(createDeck());
      deck = secretlyGiveBoFourOfAKind(deck);
      state.players.forEach(p => state.hands[p.id] = []);

      for (let round = 0; round < 13; round++) {
        for (const p of state.players) {
          const card = deck.shift();
          if (card) state.hands[p.id].push(card);
        }
      }

      for (const p of state.players) state.hands[p.id] = sortCards(state.hands[p.id]);

      let firstId = state.players[0].id;
      for (const p of state.players) {
        if (state.hands[p.id].some(c => c.rank === "3" && c.suit === "♠")) firstId = p.id;
      }
      state.turn = state.players.findIndex(p => p.id === firstId);
      addLog("Bắt đầu ván. Người có 3♠ đi trước.");
      syncAllPerPlayer();
    }

    function syncAllPerPlayer() {
      if (!isHost) return;
      for (const [pid, conn] of connections.entries()) syncTo(conn, pid);
      render();
    }

    function hostPlay(playerId, cardIds) {
      if (!isHost || state.phase !== "playing") return;
      const player = currentPlayer();
      if (!player || player.id !== playerId) return syncAllPerPlayer();

      const hand = state.hands[playerId] || [];
      const chosen = hand.filter(c => cardIds.includes(c.id));
      if (chosen.length !== cardIds.length) return;

      const play = analyze(chosen);
      if (!play) return reject(playerId, "Bộ bài không hợp lệ.");
      if (!canBeat(play, state.lastPlay)) return reject(playerId, "Bài chưa đủ lớn để đè lượt trước.");

      state.hands[playerId] = hand.filter(c => !cardIds.includes(c.id));
      state.lastPlay = { ...play, cards: chosen, playerId, playerName: player.name };
      state.passes = [];
      addLog(`${player.name} đánh ${chosen.map(cardLabel).join(" ")}.`);

      if (state.hands[playerId].length === 0 && !state.winnerIds.includes(playerId)) {
        state.winnerIds.push(playerId);
        addLog(`${player.name} đã hết bài!`);
      }

      const alive = alivePlayers();
      if (alive.length <= 1) {
        if (alive[0] && !state.winnerIds.includes(alive[0].id)) state.winnerIds.push(alive[0].id);
        state.phase = "ended";
        addLog("Ván đấu kết thúc.");
      } else {
        advanceTurn();
      }
      syncAllPerPlayer();
    }

    function hostPass(playerId) {
      if (!isHost || state.phase !== "playing") return;
      const player = currentPlayer();
      if (!player || player.id !== playerId) return syncAllPerPlayer();
      if (!state.lastPlay) return reject(playerId, "Đầu vòng không được bỏ lượt.");
      if (!state.passes.includes(playerId)) state.passes.push(playerId);
      addLog(`${player.name} bỏ lượt.`);
      advanceTurn();
      resetRoundIfNeeded();
      syncAllPerPlayer();
    }

    function reject(playerId, reason) {
      if (playerId === myId) alert(reason);
      else send(connections.get(playerId), "reject", { reason });
    }

    function cardLabel(c) {
      return c.back ? "🂠" : `${c.rank}${c.suit}`;
    }

    function setupConn(conn) {
      conn.on("open", () => {
        connections.set(conn.peer, conn);
      });
      conn.on("data", msg => handleMessage(conn, msg));
      conn.on("close", () => {
        connections.delete(conn.peer);
        if (isHost) {
          const p = state.players.find(x => x.id === conn.peer);
          if (p) addLog(`${p.name} mất kết nối.`);
          syncAllPerPlayer();
        }
      });
    }

    function handleMessage(conn, msg) {
      if (!msg || !msg.type) return;
      const { type, payload } = msg;

      if (isHost) {
        if (type === "join") {
          if (state.phase !== "lobby") return send(conn, "reject", { reason: "Phòng đã bắt đầu ván." });
          if (state.players.length >= 4) return send(conn, "reject", { reason: "Phòng đã đủ 4 người." });
          if (!state.players.some(p => p.id === conn.peer)) {
            state.players.push({ id: conn.peer, name: payload.name || "Người chơi" });
            addLog(`${payload.name || "Người chơi"} vào phòng.`);
          }
          syncAllPerPlayer();
        }
        if (type === "play") hostPlay(conn.peer, payload.cardIds || []);
        if (type === "pass") hostPass(conn.peer);
        if (type === "chatlog") addLog(payload.text || "");
        return;
      }

      if (type === "state") {
        state = payload;
        selected.clear();
        render();
      }
      if (type === "reject") alert(payload.reason || "Yêu cầu bị từ chối.");
    }

    function render() {
      $("netStatus").textContent = peer ? `Peer: ${myId || "đang mở..."}` : "Chưa kết nối";
      $("roomCodeBox").classList.toggle("hidden", !roomCode);
      $("roomCodeBox").textContent = roomCode;
      $("startBtn").disabled = !(isHost && state.phase === "lobby" && state.players.length >= 2);
      $("resetBtn").disabled = !isHost;

      const playersBox = $("playersBox");
      playersBox.innerHTML = "";
      for (const p of state.players) {
        const div = document.createElement("div");
        div.className = "player" + (currentPlayer()?.id === p.id ? " active" : "");
        const order = state.winnerIds.indexOf(p.id);
        div.innerHTML = `<div><div class="name">${escapeHtml(p.name)}${p.id === myId ? " (Bạn)" : ""}</div><div class="meta">${order >= 0 ? "Về thứ " + (order + 1) : "Đang chơi"}</div></div><div>${(state.hands[p.id] || []).length} lá</div>`;
        playersBox.appendChild(div);
      }

      const active = currentPlayer();
      const winners = state.winnerIds.map(id => state.players.find(p => p.id === id)?.name).filter(Boolean);
      $("statusBox").innerHTML = statusText(active, winners);

      const lastCards = $("lastCards");
      lastCards.innerHTML = "";
      if (state.lastPlay) {
        $("lastPlayInfo").textContent = `${state.lastPlay.playerName} vừa đánh.`;
        for (const c of state.lastPlay.cards) lastCards.appendChild(cardEl(c, false, true));
      } else {
        $("lastPlayInfo").textContent = state.phase === "playing" ? "Đầu vòng: có thể đánh bất kỳ bộ hợp lệ." : "Chưa có lượt đánh.";
      }

      const handBox = $("handBox");
      handBox.innerHTML = "";
      const myHand = sortCards(state.hands[myId] || []);
      for (const c of myHand) handBox.appendChild(cardEl(c, true));

      const myTurn = state.phase === "playing" && active?.id === myId;
      $("playBtn").disabled = !myTurn || selected.size === 0;
      $("passBtn").disabled = !myTurn || !state.lastPlay;

      $("logBox").innerHTML = state.log.map(x => `<div>${escapeHtml(x)}</div>`).join("");
    }

    function statusText(active, winners) {
      if (state.phase === "lobby") return `Đang chờ người chơi. Chủ phòng bấm <b>Bắt đầu</b> khi đủ người.`;
      if (state.phase === "ended") return `<b class="ok">Ván kết thúc.</b><br>Kết quả: ${winners.map(escapeHtml).join(" → ") || "chưa có"}.`;
      const turnName = active ? escapeHtml(active.name) : "?";
      const yourTurn = active?.id === myId ? "<b class='ok'>Đến lượt bạn.</b>" : `Đến lượt <b>${turnName}</b>.`;
      return `${yourTurn}<br>Chọn bài rồi bấm <b>Đánh bài</b>. Bộ hỗ trợ: lẻ, đôi, sám, sảnh, ba đôi thông trở lên, tứ quý.`;
    }

    function cardEl(c, clickable, small = false) {
      const div = document.createElement("div");
      div.className = "card" + (c.suit === "♦" || c.suit === "♥" ? " red" : "") + (selected.has(c.id) ? " selected" : "") + (small ? " small" : "") + (c.back ? " back" : "");
      div.textContent = cardLabel(c);
      if (clickable && !c.back) {
        div.onclick = () => {
          if (selected.has(c.id)) selected.delete(c.id);
          else selected.add(c.id);
          render();
        };
      }
      return div;
    }

    function escapeHtml(str) {
      return String(str).replace(/[&<>"]/g, s => ({ "&":"&amp;", "<":"&lt;", ">":"&gt;", '"':"&quot;" }[s]));
    }

    function hostAddSelf() {
      state = freshState();
      state.hostId = myId;
      state.players = [{ id: myId, name: myName }];
      addLog(`${myName} tạo phòng.`);
    }

    $("createBtn").onclick = () => {
      myName = normalizeName();
      roomCode = makeRoomCode();
      myId = roomId(roomCode);
      isHost = true;
      if (peer) peer.destroy();
      peer = new Peer(myId, { debug: 1 });
      peer.on("open", id => {
        myId = id;
        hostAddSelf();
        render();
      });
      peer.on("connection", conn => setupConn(conn));
      peer.on("error", err => {
        alert("Không tạo được phòng. Thử lại mã khác. " + err.type);
        console.error(err);
      });
    };

    $("joinBtn").onclick = () => {
      myName = normalizeName();
      roomCode = ($("roomInput").value || "").trim().toUpperCase();
      if (!roomCode) return alert("Nhập mã phòng trước.");
      isHost = false;
      if (peer) peer.destroy();
      peer = new Peer(undefined, { debug: 1 });
      peer.on("open", id => {
        myId = id;
        const conn = peer.connect(roomId(roomCode), { reliable: true });
        setupConn(conn);
        conn.on("open", () => send(conn, "join", { name: myName }));
        render();
      });
      peer.on("error", err => {
        alert("Không kết nối được phòng. Kiểm tra mã hoặc thử tải lại trang. " + err.type);
        console.error(err);
      });
    };

    $("startBtn").onclick = hostStartGame;
    $("resetBtn").onclick = () => {
      if (!isHost) return;
      hostStartGame();
    };

    $("playBtn").onclick = () => {
      const ids = [...selected];
      if (isHost) hostPlay(myId, ids);
      else {
        const hostConn = [...connections.values()][0];
        send(hostConn, "play", { cardIds: ids });
      }
      selected.clear();
      render();
    };

    $("passBtn").onclick = () => {
      if (isHost) hostPass(myId);
      else {
        const hostConn = [...connections.values()][0];
        send(hostConn, "pass", {});
      }
    };

    $("sortBtn").onclick = () => {
      if (state.hands[myId]) state.hands[myId] = sortCards(state.hands[myId]);
      render();
    };

    render();
  </script>
</body>
</html>
    button:disabled { opacity: .5; cursor: not-allowed; transform: none; }

    .btn-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8px;
      margin-top: 10px;
    }

    .secondary { background: #38bdf8; color: #082f49; }
    .danger { background: var(--danger); color: #450a0a; }
    .warn { background: var(--warn); color: #451a03; }

    .room-code {
      font-size: 28px;
      font-weight: 900;
      letter-spacing: .08em;
      background: #020617;
      border: 1px dashed var(--border);
      border-radius: 16px;
      padding: 12px;
      text-align: center;
      user-select: all;
    }

    .players {
      display: grid;
      gap: 8px;
      margin-top: 12px;
    }

    .player {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: var(--panel2);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 10px;
    }

    .player.active { outline: 2px solid var(--accent); }
    .player .name { font-weight: 800; }
    .player .meta { color: var(--muted); font-size: 13px; }

    .table {
      min-height: 280px;
      display: grid;
      gap: 12px;
    }

    .status {
      background: rgba(2,6,23,.65);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 12px;
      color: var(--muted);
      line-height: 1.45;
    }

    .last-play {
      background: rgba(255,255,255,.08);
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: 14px;
      min-height: 112px;
    }

    .cards {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      align-items: center;
    }

    .card {
      width: 54px;
      height: 76px;
      border-radius: 10px;
      background: var(--card);
      color: var(--cardText);
      border: 2px solid #cbd5e1;
      display: grid;
      place-items: center;
      font-weight: 900;
      box-shadow: 0 8px 18px rgba(0,0,0,.24);
      cursor: pointer;
      user-select: none;
      position: relative;
    }

    .card.red { color: var(--red); }
    .card.selected {
      transform: translateY(-16px);
      border-color: var(--accent);
      box-shadow: 0 12px 26px rgba(34,197,94,.35);
    }

    .card.small {
      width: 44px;
      height: 62px;
      font-size: 14px;
      cursor: default;
      transform: none;
    }

    .card.back {
      background: linear-gradient(135deg, #2563eb, #7c3aed);
      border-color: #93c5fd;
      color: white;
    }

    .hand-wrap {
      margin-top: 12px;
      background: rgba(2,6,23,.5);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 14px;
    }

    .controls {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin-top: 12px;
    }

    @media (max-width: 620px) {
      .controls { grid-template-columns: 1fr; }
      .card { width: 46px; height: 66px; font-size: 14px; }
    }

    .log {
      height: 180px;
      overflow: auto;
      display: grid;
      gap: 6px;
      font-size: 13px;
      color: var(--muted);
      background: #020617;
      border-radius: 14px;
      padding: 10px;
      border: 1px solid var(--border);
    }

    .hidden { display: none !important; }
    .note { color: var(--muted); font-size: 13px; line-height: 1.45; }
    .ok { color: #86efac; }
    .bad { color: #fca5a5; }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <div>
        <h1>Tiến Lên Online</h1>
        <div class="pill">GitHub Pages + PeerJS + mã phòng</div>
      </div>
      <div class="pill" id="netStatus">Chưa kết nối</div>
    </header>

    <div class="grid">
      <aside class="panel">
        <h2>Phòng chơi</h2>
        <label>Tên của bạn</label>
        <input id="nameInput" maxlength="18" placeholder="Ví dụ: Hải" />

        <div class="btn-row">
          <button id="createBtn">Tạo phòng</button>
          <button class="secondary" id="joinBtn">Vào phòng</button>
        </div>

        <label>Mã phòng</label>
        <input id="roomInput" maxlength="12" placeholder="Nhập mã phòng" />
        <div class="room-code hidden" id="roomCodeBox"></div>

        <p class="note">
          Người tạo phòng bấm “Tạo phòng”, gửi mã cho bạn bè. Người khác nhập mã rồi bấm “Vào phòng”. Nên chơi 2–4 người.
        </p>

        <div class="btn-row">
          <button class="warn" id="startBtn" disabled>Bắt đầu</button>
          <button class="danger" id="resetBtn" disabled>Ván mới</button>
        </div>

        <h2 style="margin-top:18px">Người chơi</h2>
        <div class="players" id="playersBox"></div>
      </aside>

      <main class="panel table">
        <div class="status" id="statusBox">
          Tạo phòng hoặc vào phòng để bắt đầu.
        </div>

        <section class="last-play">
          <h2>Bài vừa đánh</h2>
          <div id="lastPlayInfo" class="note">Chưa có lượt đánh.</div>
          <div class="cards" id="lastCards"></div>
        </section>

        <section class="hand-wrap">
          <h2>Bài của bạn</h2>
          <div class="cards" id="handBox"></div>
          <div class="controls">
            <button id="playBtn" disabled>Đánh bài</button>
            <button class="secondary" id="passBtn" disabled>Bỏ lượt</button>
            <button class="warn" id="sortBtn">Sắp xếp</button>
          </div>
        </section>

        <section>
          <h2>Nhật ký</h2>
          <div class="log" id="logBox"></div>
        </section>
      </main>
    </div>
  </div>

  <script>
    const $ = (id) => document.getElementById(id);

    const SUITS = ["♠", "♣", "♦", "♥"];
    const RANKS = ["3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K", "A", "2"];
    const SUIT_POWER = { "♠": 0, "♣": 1, "♦": 2, "♥": 3 };

    let peer = null;
    let isHost = false;
    let roomCode = "";
    let myId = "";
    let myName = "";
    let selected = new Set();
    let connections = new Map();

    let state = freshState();

    function freshState() {
      return {
        phase: "lobby",
        hostId: "",
        players: [],
        hands: {},
        turn: 0,
        lastPlay: null,
        passes: [],
        winnerIds: [],
        log: []
      };
    }

    function roomId(code) {
      return "tl-" + code.trim().toUpperCase();
    }

    function makeRoomCode() {
      const chars = "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      let out = "";
      for (let i = 0; i < 5; i++) out += chars[Math.floor(Math.random() * chars.length)];
      return out;
    }

    function addLog(msg) {
      const time = new Date().toLocaleTimeString("vi-VN", { hour: "2-digit", minute: "2-digit" });
      state.log.unshift(`[${time}] ${msg}`);
      state.log = state.log.slice(0, 80);
    }

    function logLocal(msg) {
      const time = new Date().toLocaleTimeString("vi-VN", { hour: "2-digit", minute: "2-digit" });
      state.log.unshift(`[${time}] ${msg}`);
      render();
    }

    function normalizeName() {
      return ($("nameInput").value || "Người chơi").trim().slice(0, 18) || "Người chơi";
    }

    function send(conn, type, payload = {}) {
      if (conn && conn.open) conn.send({ type, payload });
    }

    function broadcast(type, payload = {}) {
      for (const conn of connections.values()) send(conn, type, payload);
    }

    function syncAll() {
      if (!isHost) return;
      broadcast("state", publicState());
      render();
    }

    function publicState() {
      const clone = JSON.parse(JSON.stringify(state));
      for (const p of clone.players) {
        if (p.id !== myId) clone.hands[p.id] = Array(clone.hands[p.id]?.length || 0).fill({ back: true });
      }
      return clone;
    }

    function stateForPlayer(playerId) {
      const clone = JSON.parse(JSON.stringify(state));
      for (const p of clone.players) {
        if (p.id !== playerId) clone.hands[p.id] = Array(clone.hands[p.id]?.length || 0).fill({ back: true });
      }
      return clone;
    }

    function syncTo(conn, playerId) {
      send(conn, "state", stateForPlayer(playerId));
    }

    function createDeck() {
      const deck = [];
      for (const rank of RANKS) {
        for (const suit of SUITS) {
          deck.push({ rank, suit, id: rank + suit });
        }
      }
      return deck;
    }

    function cardValue(card) {
      return RANKS.indexOf(card.rank) * 4 + SUIT_POWER[card.suit];
    }

    function rankValue(card) {
      return RANKS.indexOf(card.rank);
    }

    function sortCards(cards) {
      return [...cards].sort((a, b) => cardValue(a) - cardValue(b));
    }

    function shuffle(arr) {
      const a = [...arr];
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    }

    function sameRank(cards) {
      return cards.every(c => c.rank === cards[0].rank);
    }

    function isConsecutiveRank(values) {
      for (let i = 1; i < values.length; i++) {
        if (values[i] !== values[i - 1] + 1) return false;
      }
      return true;
    }

    function analyze(cards) {
      cards = sortCards(cards);
      if (!cards.length) return null;
      const n = cards.length;
      const ranks = cards.map(rankValue);
      const uniqueRanks = [...new Set(ranks)];
      const high = cards[cards.length - 1];

      if (n === 1) return { type: "single", size: 1, high, power: cardValue(high) };
      if (n === 2 && sameRank(cards)) return { type: "pair", size: 2, high, power: cardValue(high) };
      if (n === 3 && sameRank(cards)) return { type: "triple", size: 3, high, power: cardValue(high) };

      const hasTwo = ranks.includes(RANKS.indexOf("2"));
      if (n >= 3 && uniqueRanks.length === n && !hasTwo && isConsecutiveRank(ranks)) {
        return { type: "straight", size: n, high, power: rankValue(high) };
      }

      if (n % 2 === 0 && n >= 6 && !hasTwo) {
        const pairs = [];
        for (let i = 0; i < n; i += 2) {
          if (cards[i].rank !== cards[i + 1].rank) return null;
          pairs.push(rankValue(cards[i]));
        }
        if (isConsecutiveRank(pairs)) {
          return { type: "pairStraight", size: n, pairs: n / 2, high, power: rankValue(high) };
        }
      }

      if (n === 4 && sameRank(cards)) return { type: "four", size: 4, high, power: rankValue(high) };
      return null;
    }

    function canBeat(play, last) {
      if (!last) return true;
      if (play.type === last.type && play.size === last.size) return play.power > last.power;

      // Luật chặt đơn giản kiểu miền Nam:
      // Tứ quý chặt 1 lá 2 hoặc đôi 2. Ba đôi thông chặt 1 lá 2.
      if (play.type === "four" && last.type === "single" && last.high.rank === "2") return true;
      if (play.type === "four" && last.type === "pair" && last.high.rank === "2") return true;
      if (play.type === "pairStraight" && play.pairs >= 3 && last.type === "single" && last.high.rank === "2") return true;
      if (play.type === "pairStraight" && last.type === "pairStraight" && play.pairs === last.pairs) return play.power > last.power;
      return false;
    }

    function currentPlayer() {
      return state.players[state.turn];
    }

    function alivePlayers() {
      return state.players.filter(p => !state.winnerIds.includes(p.id));
    }

    function advanceTurn() {
      const alive = alivePlayers();
      if (alive.length <= 1) return;
      for (let i = 1; i <= state.players.length; i++) {
        const next = (state.turn + i) % state.players.length;
        const p = state.players[next];
        if (!state.winnerIds.includes(p.id)) {
          state.turn = next;
          return;
        }
      }
    }

    function resetRoundIfNeeded() {
      const alive = alivePlayers();
      if (!state.lastPlay) return;
      const activeIds = alive.map(p => p.id);
      const passedCount = state.passes.filter(id => activeIds.includes(id) && id !== state.lastPlay.playerId).length;
      if (passedCount >= Math.max(0, alive.length - 1)) {
        const leadIndex = state.players.findIndex(p => p.id === state.lastPlay.playerId && !state.winnerIds.includes(p.id));
        state.turn = leadIndex >= 0 ? leadIndex : state.turn;
        state.lastPlay = null;
        state.passes = [];
        addLog("Vòng mới: người thắng lượt trước được đánh bất kỳ.");
      }
    }

    function hostStartGame() {
      if (!isHost) return;
      if (state.players.length < 2) return alert("Cần ít nhất 2 người chơi.");
      state.phase = "playing";
      state.hands = {};
      state.lastPlay = null;
      state.passes = [];
      state.winnerIds = [];

      const deck = shuffle(createDeck());
      state.players.forEach(p => state.hands[p.id] = []);
      deck.forEach((card, i) => {
        const p = state.players[i % state.players.length];
        state.hands[p.id].push(card);
      });
      for (const p of state.players) state.hands[p.id] = sortCards(state.hands[p.id]);

      let firstId = state.players[0].id;
      for (const p of state.players) {
        if (state.hands[p.id].some(c => c.rank === "3" && c.suit === "♠")) firstId = p.id;
      }
      state.turn = state.players.findIndex(p => p.id === firstId);
      addLog("Bắt đầu ván. Người có 3♠ đi trước.");
      syncAllPerPlayer();
    }

    function syncAllPerPlayer() {
      if (!isHost) return;
      for (const [pid, conn] of connections.entries()) syncTo(conn, pid);
      render();
    }

    function hostPlay(playerId, cardIds) {
      if (!isHost || state.phase !== "playing") return;
      const player = currentPlayer();
      if (!player || player.id !== playerId) return syncAllPerPlayer();

      const hand = state.hands[playerId] || [];
      const chosen = hand.filter(c => cardIds.includes(c.id));
      if (chosen.length !== cardIds.length) return;

      const play = analyze(chosen);
      if (!play) return reject(playerId, "Bộ bài không hợp lệ.");
      if (!canBeat(play, state.lastPlay)) return reject(playerId, "Bài chưa đủ lớn để đè lượt trước.");

      state.hands[playerId] = hand.filter(c => !cardIds.includes(c.id));
      state.lastPlay = { ...play, cards: chosen, playerId, playerName: player.name };
      state.passes = [];
      addLog(`${player.name} đánh ${chosen.map(cardLabel).join(" ")}.`);

      if (state.hands[playerId].length === 0 && !state.winnerIds.includes(playerId)) {
        state.winnerIds.push(playerId);
        addLog(`${player.name} đã hết bài!`);
      }

      const alive = alivePlayers();
      if (alive.length <= 1) {
        if (alive[0] && !state.winnerIds.includes(alive[0].id)) state.winnerIds.push(alive[0].id);
        state.phase = "ended";
        addLog("Ván đấu kết thúc.");
      } else {
        advanceTurn();
      }
      syncAllPerPlayer();
    }

    function hostPass(playerId) {
      if (!isHost || state.phase !== "playing") return;
      const player = currentPlayer();
      if (!player || player.id !== playerId) return syncAllPerPlayer();
      if (!state.lastPlay) return reject(playerId, "Đầu vòng không được bỏ lượt.");
      if (!state.passes.includes(playerId)) state.passes.push(playerId);
      addLog(`${player.name} bỏ lượt.`);
      advanceTurn();
      resetRoundIfNeeded();
      syncAllPerPlayer();
    }

    function reject(playerId, reason) {
      if (playerId === myId) alert(reason);
      else send(connections.get(playerId), "reject", { reason });
    }

    function cardLabel(c) {
      return c.back ? "🂠" : `${c.rank}${c.suit}`;
    }

    function setupConn(conn) {
      conn.on("open", () => {
        connections.set(conn.peer, conn);
      });
      conn.on("data", msg => handleMessage(conn, msg));
      conn.on("close", () => {
        connections.delete(conn.peer);
        if (isHost) {
          const p = state.players.find(x => x.id === conn.peer);
          if (p) addLog(`${p.name} mất kết nối.`);
          syncAllPerPlayer();
        }
      });
    }

    function handleMessage(conn, msg) {
      if (!msg || !msg.type) return;
      const { type, payload } = msg;

      if (isHost) {
        if (type === "join") {
          if (state.phase !== "lobby") return send(conn, "reject", { reason: "Phòng đã bắt đầu ván." });
          if (state.players.length >= 4) return send(conn, "reject", { reason: "Phòng đã đủ 4 người." });
          if (!state.players.some(p => p.id === conn.peer)) {
            state.players.push({ id: conn.peer, name: payload.name || "Người chơi" });
            addLog(`${payload.name || "Người chơi"} vào phòng.`);
          }
          syncAllPerPlayer();
        }
        if (type === "play") hostPlay(conn.peer, payload.cardIds || []);
        if (type === "pass") hostPass(conn.peer);
        if (type === "chatlog") addLog(payload.text || "");
        return;
      }

      if (type === "state") {
        state = payload;
        selected.clear();
        render();
      }
      if (type === "reject") alert(payload.reason || "Yêu cầu bị từ chối.");
    }

    function render() {
      $("netStatus").textContent = peer ? `Peer: ${myId || "đang mở..."}` : "Chưa kết nối";
      $("roomCodeBox").classList.toggle("hidden", !roomCode);
      $("roomCodeBox").textContent = roomCode;
      $("startBtn").disabled = !(isHost && state.phase === "lobby" && state.players.length >= 2);
      $("resetBtn").disabled = !isHost;

      const playersBox = $("playersBox");
      playersBox.innerHTML = "";
      for (const p of state.players) {
        const div = document.createElement("div");
        div.className = "player" + (currentPlayer()?.id === p.id ? " active" : "");
        const order = state.winnerIds.indexOf(p.id);
        div.innerHTML = `<div><div class="name">${escapeHtml(p.name)}${p.id === myId ? " (Bạn)" : ""}</div><div class="meta">${order >= 0 ? "Về thứ " + (order + 1) : "Đang chơi"}</div></div><div>${(state.hands[p.id] || []).length} lá</div>`;
        playersBox.appendChild(div);
      }

      const active = currentPlayer();
      const winners = state.winnerIds.map(id => state.players.find(p => p.id === id)?.name).filter(Boolean);
      $("statusBox").innerHTML = statusText(active, winners);

      const lastCards = $("lastCards");
      lastCards.innerHTML = "";
      if (state.lastPlay) {
        $("lastPlayInfo").textContent = `${state.lastPlay.playerName} vừa đánh.`;
        for (const c of state.lastPlay.cards) lastCards.appendChild(cardEl(c, false, true));
      } else {
        $("lastPlayInfo").textContent = state.phase === "playing" ? "Đầu vòng: có thể đánh bất kỳ bộ hợp lệ." : "Chưa có lượt đánh.";
      }

      const handBox = $("handBox");
      handBox.innerHTML = "";
      const myHand = sortCards(state.hands[myId] || []);
      for (const c of myHand) handBox.appendChild(cardEl(c, true));

      const myTurn = state.phase === "playing" && active?.id === myId;
      $("playBtn").disabled = !myTurn || selected.size === 0;
      $("passBtn").disabled = !myTurn || !state.lastPlay;

      $("logBox").innerHTML = state.log.map(x => `<div>${escapeHtml(x)}</div>`).join("");
    }

    function statusText(active, winners) {
      if (state.phase === "lobby") return `Đang chờ người chơi. Chủ phòng bấm <b>Bắt đầu</b> khi đủ người.`;
      if (state.phase === "ended") return `<b class="ok">Ván kết thúc.</b><br>Kết quả: ${winners.map(escapeHtml).join(" → ") || "chưa có"}.`;
      const turnName = active ? escapeHtml(active.name) : "?";
      const yourTurn = active?.id === myId ? "<b class='ok'>Đến lượt bạn.</b>" : `Đến lượt <b>${turnName}</b>.`;
      return `${yourTurn}<br>Chọn bài rồi bấm <b>Đánh bài</b>. Bộ hỗ trợ: lẻ, đôi, sám, sảnh, ba đôi thông trở lên, tứ quý.`;
    }

    function cardEl(c, clickable, small = false) {
      const div = document.createElement("div");
      div.className = "card" + (c.suit === "♦" || c.suit === "♥" ? " red" : "") + (selected.has(c.id) ? " selected" : "") + (small ? " small" : "") + (c.back ? " back" : "");
      div.textContent = cardLabel(c);
      if (clickable && !c.back) {
        div.onclick = () => {
          if (selected.has(c.id)) selected.delete(c.id);
          else selected.add(c.id);
          render();
        };
      }
      return div;
    }

    function escapeHtml(str) {
      return String(str).replace(/[&<>"]/g, s => ({ "&":"&amp;", "<":"&lt;", ">":"&gt;", '"':"&quot;" }[s]));
    }

    function hostAddSelf() {
      state = freshState();
      state.hostId = myId;
      state.players = [{ id: myId, name: myName }];
      addLog(`${myName} tạo phòng.`);
    }

    $("createBtn").onclick = () => {
      myName = normalizeName();
      roomCode = makeRoomCode();
      myId = roomId(roomCode);
      isHost = true;
      if (peer) peer.destroy();
      peer = new Peer(myId, { debug: 1 });
      peer.on("open", id => {
        myId = id;
        hostAddSelf();
        render();
      });
      peer.on("connection", conn => setupConn(conn));
      peer.on("error", err => {
        alert("Không tạo được phòng. Thử lại mã khác. " + err.type);
        console.error(err);
      });
    };

    $("joinBtn").onclick = () => {
      myName = normalizeName();
      roomCode = ($("roomInput").value || "").trim().toUpperCase();
      if (!roomCode) return alert("Nhập mã phòng trước.");
      isHost = false;
      if (peer) peer.destroy();
      peer = new Peer(undefined, { debug: 1 });
      peer.on("open", id => {
        myId = id;
        const conn = peer.connect(roomId(roomCode), { reliable: true });
        setupConn(conn);
        conn.on("open", () => send(conn, "join", { name: myName }));
        render();
      });
      peer.on("error", err => {
        alert("Không kết nối được phòng. Kiểm tra mã hoặc thử tải lại trang. " + err.type);
        console.error(err);
      });
    };

    $("startBtn").onclick = hostStartGame;
    $("resetBtn").onclick = () => {
      if (!isHost) return;
      hostStartGame();
    };

    $("playBtn").onclick = () => {
      const ids = [...selected];
      if (isHost) hostPlay(myId, ids);
      else {
        const hostConn = [...connections.values()][0];
        send(hostConn, "play", { cardIds: ids });
      }
      selected.clear();
      render();
    };

    $("passBtn").onclick = () => {
      if (isHost) hostPass(myId);
      else {
        const hostConn = [...connections.values()][0];
        send(hostConn, "pass", {});
      }
    };

    $("sortBtn").onclick = () => {
      if (state.hands[myId]) state.hands[myId] = sortCards(state.hands[myId]);
      render();
    };

    render();
  </script>
</body>
</html>
  </style>
</head>
<body>
  <div class="app">
    <section class="hero">
      <div class="card">
        <h1>Pokemon Odyssey<br/>Peer Battle</h1>
        <p class="muted">Bản online không Firebase: dùng PeerJS để 2 người chơi kết nối trực tiếp bằng mã phòng. Rất hợp để đưa lên GitHub Pages vì không cần database, không cần đăng nhập.</p>
        <div class="row" style="margin-top:12px">
          <button onclick="openTab('online')">🌐 Tạo / nhập mã phòng</button>
          <button class="btn-green" onclick="openTab('battle')">⚔️ Đấu online</button>
          <button class="btn-blue" onclick="openTab('team')">📦 Chọn đội</button>
          <button class="ghost" onclick="openTab('guide')">📘 Hướng dẫn</button>
        </div>
      </div>
      <div class="card">
        <h3>Trạng thái</h3>
        <div class="list" id="status"></div>
      </div>
    </section>

    <nav class="tabs" id="tabs"></nav>

    <main>
      <section id="home" class="pane active"></section>
      <section id="online" class="pane"></section>
      <section id="battle" class="pane"></section>
      <section id="team" class="pane"></section>
      <section id="guide" class="pane"></section>
    </main>

    <footer class="footer">Pokemon Odyssey Peer Battle • Không Firebase • Không tài khoản • GitHub Pages ready</footer>
  </div>

  <script src="https://unpkg.com/peerjs@1.5.4/dist/peerjs.min.js"></script>
  <script>
    const tabs = [["home","🏠 Trang chủ"],["online","🌐 Online Peer"],["battle","⚔️ Battle"],["team","📦 Đội hình"],["guide","📘 Hướng dẫn"]];
    const starters = [
      {id:1,name:"Bulbasaur",types:["grass","poison"],hp:116,maxHp:116,energy:40,maxEnergy:100,atk:48,def:44,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png",moves:[m("Leaf Cutter","grass",20,0),m("Vine Lash","grass",34,15),m("Toxic Bloom","poison",45,30),m("Solar Storm","grass",68,50)]},
      {id:4,name:"Charmander",types:["fire"],hp:104,maxHp:104,energy:45,maxEnergy:100,atk:55,def:38,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/4.png",moves:[m("Ember Burst","fire",21,0),m("Flame Dash","fire",34,15),m("Inferno Fang","fire",48,32),m("Solar Inferno","fire",70,52)]},
      {id:7,name:"Squirtle",types:["water"],hp:112,maxHp:112,energy:40,maxEnergy:100,atk:45,def:60,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png",moves:[m("Bubble Jet","water",19,0),m("Aqua Slash","water",33,14),m("Tidal Crush","water",47,31),m("Ocean Breaker","water",69,52)]},
      {id:25,name:"Pikachu",types:["electric"],hp:96,maxHp:96,energy:55,maxEnergy:110,atk:58,def:35,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png",moves:[m("Spark Bolt","electric",20,0),m("Volt Dash","electric",36,16),m("Thunder Cage","electric",51,34),m("Heaven Thunder","electric",74,55)]},
      {id:133,name:"Eevee",types:["normal"],hp:110,maxHp:110,energy:45,maxEnergy:100,atk:52,def:45,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/133.png",moves:[m("Quick Strike","normal",20,0),m("Double Hit","normal",35,15),m("Adaptive Rush","normal",49,32),m("Evolution Pulse","normal",72,55)]},
      {id:150,name:"Mewtwo",types:["psychic"],hp:140,maxHp:140,energy:60,maxEnergy:120,atk:70,def:55,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/150.png",moves:[m("Mind Tap","psychic",24,0),m("Psy Cut","psychic",40,18),m("Dream Nova","psychic",58,38),m("Astral Collapse","psychic",86,62)]},
      {id:6,name:"Charizard",types:["fire","flying"],hp:132,maxHp:132,energy:55,maxEnergy:115,atk:68,def:58,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/6.png",moves:[m("Flame Wing","fire",26,0),m("Air Cutter","flying",38,18),m("Dragon Heat","dragon",56,36),m("Volcano Sky","fire",82,60)]},
      {id:9,name:"Blastoise",types:["water"],hp:145,maxHp:145,energy:50,maxEnergy:110,atk:62,def:72,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/9.png",moves:[m("Water Cannon","water",25,0),m("Shell Guard","water",34,14),m("Hydro Crush","water",56,36),m("Ocean Fortress","water",80,60)]}
    ];
    function m(name,type,power,cost){return {name,type,power,cost}}
    const S = {
      tab:"home", peer:null, conn:null, myPeerId:"", joinCode:"", host:false, connected:false, playerName:localStorage.getItem('peerName')||'Trainer',
      myTeam:JSON.parse(localStorage.getItem('peerTeam')||'null')||[clone(starters[0]),clone(starters[3]),clone(starters[4])],
      enemyTeam:[], myActive:0, enemyActive:0, myTurn:false, battleStarted:false, winner:null,
      log:["Chào mừng đến Peer Battle. Người A tạo mã, người B nhập mã để vào."]
    };
    const $=id=>document.getElementById(id);const cap=s=>s?s.charAt(0).toUpperCase()+s.slice(1):'';const rand=(a,b)=>Math.floor(Math.random()*(b-a+1))+a;function clone(x){return JSON.parse(JSON.stringify(x))}
    function openTab(id){S.tab=id;document.querySelectorAll('.pane').forEach(p=>p.classList.remove('active'));$(id).classList.add('active');render()} window.openTab=openTab;
    function addLog(msg){S.log.unshift('• '+msg);S.log=S.log.slice(0,80);render()} function toast(msg){alert(msg)}
    function roomId(){return 'poke-'+Math.random().toString(36).slice(2,7).toUpperCase()}
    function send(data){if(S.conn&&S.conn.open)S.conn.send(data)}
    function resetBattle(){S.enemyTeam=[];S.myActive=0;S.enemyActive=0;S.myTurn=false;S.battleStarted=false;S.winner=null;S.myTeam=S.myTeam.map(x=>{let y=clone(x);y.hp=y.maxHp;y.energy=Math.max(40,y.energy||40);return y});}

    function render(){renderShell();renderHome();renderOnline();renderBattle();renderTeam();renderGuide()}
    function renderShell(){
      $('tabs').innerHTML=tabs.map(([id,label])=>`<button class="tab ${S.tab===id?'active':''}" onclick="openTab('${id}')">${label}</button>`).join('');
      $('status').innerHTML=`
        <div class="stat"><span class="dot ${window.Peer?'ok':''}"></span>PeerJS: ${window.Peer?'đã tải':'chưa tải'}</div>
        <div class="stat"><span class="dot ${S.peer?'ok':''}"></span>Phòng của bạn: <span class="copy">${S.myPeerId||'chưa tạo'}</span></div>
        <div class="stat"><span class="dot ${S.connected?'ok':''}"></span>Kết nối: ${S.connected?'đã có đối thủ':'chưa kết nối'}</div>
        <div class="stat">Vai trò: ${S.host?'Chủ phòng':'Người tham gia / chưa chọn'}</div>
        <div class="stat">Lượt: ${S.battleStarted?(S.myTurn?'bạn':'đối thủ'):'chưa bắt đầu'}</div>`;
    }
    function renderHome(){
      $('home').innerHTML=`<div class="grid2"><div class="card"><h2>🎮 Online đơn giản hơn Firebase</h2><p class="muted">Cách này dùng PeerJS. Không lưu hồ sơ lên server, không cần Firebase Rules. Một người tạo mã phòng, người kia nhập mã. Hai trình duyệt kết nối trực tiếp với nhau.</p><div class="grid3"><div class="mini"><h3>1. Tạo mã</h3><p class="muted">Người A bấm Tạo phòng.</p></div><div class="mini"><h3>2. Gửi mã</h3><p class="muted">Copy mã phòng gửi bạn.</p></div><div class="mini"><h3>3. Đấu</h3><p class="muted">Người B nhập mã rồi vào trận.</p></div></div><div class="row" style="margin-top:12px"><button onclick="openTab('online')">Bắt đầu online</button><button class="btn-blue" onclick="openTab('team')">Chọn đội</button></div></div><div class="card"><h2>📜 Nhật ký</h2><div class="log">${S.log.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`;
    }
    function renderOnline(){
      $('online').innerHTML=`<div class="grid2"><div class="card"><h2>🌐 Tạo phòng</h2><p class="muted">Người tạo phòng bấm nút dưới, sau đó gửi mã phòng cho bạn.</p><div class="row"><input id="nameInput" placeholder="Tên của bạn" value="${S.playerName}"><button onclick="saveName()">Lưu tên</button></div><div class="row" style="margin-top:12px"><button onclick="createPeerRoom()">🏠 Tạo phòng</button><button class="btn-red" onclick="disconnectPeer()">Ngắt kết nối</button></div><div class="mini" style="margin-top:12px"><b>Mã phòng của bạn</b><h2 class="copy">${S.myPeerId||'------'}</h2><p class="muted">Gửi mã này cho bạn. Ví dụ qua Messenger, Zalo, Discord.</p></div></div><div class="card"><h2>🚪 Vào phòng</h2><p class="muted">Người tham gia nhập mã phòng của chủ phòng.</p><div class="row"><input id="joinInput" placeholder="Nhập mã phòng, ví dụ poke-ABCDE" value="${S.joinCode}" oninput="setJoinCode(this.value)" onchange="setJoinCode(this.value)"><button class="btn-blue" onclick="joinPeerRoom()">Vào phòng</button><button class="ghost" onclick="joinPeerRoomPrompt()">Dán mã bằng hộp thoại</button></div><div class="good" style="margin-top:12px"><b>Không cần Firebase.</b><br>Nhưng cả hai người phải đang mở game cùng lúc. Nếu chủ phòng tắt tab, phòng cũng mất.</div></div></div>`;
    }
    function monBox(mon,i,active){return `<div class="mon ${active?'active':''}" onclick="chooseActive(${i})"><img src="${mon.sprite}"><b>${mon.name}</b><div>${mon.types.map(t=>`<span class="type">${cap(t)}</span>`).join('')}</div><div class="muted">HP ${mon.hp}/${mon.maxHp} • EN ${mon.energy}/${mon.maxEnergy}</div></div>`}
    function renderBattle(){
      const me=S.myTeam[S.myActive], foe=S.enemyTeam[S.enemyActive];
      $('battle').innerHTML=`<div class="grid2"><div class="card"><h2>⚔️ Peer PvP Battle</h2>${S.battleStarted&&me&&foe?battleHtml(me,foe):preBattleHtml()}</div><div class="card"><h2>📜 Battle log</h2><div class="log">${S.log.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`;
    }
    function preBattleHtml(){return `<div class="mini"><p class="muted">Kết nối với bạn trước, rồi chủ phòng bấm bắt đầu trận.</p><div class="row"><button class="btn-green" onclick="startBattle()" ${S.connected&&S.host?'':'disabled'}>Bắt đầu trận</button><button class="btn-blue" onclick="sendTeam()" ${S.connected?'':'disabled'}>Gửi lại đội hình</button></div></div>`}
    function battleHtml(me,foe){
      return `<div class="battle-scene" id="scene"><div class="fx" id="fx"></div><div class="shadow left"></div><div class="shadow right"></div><img class="poke me" src="${me.sprite}"><img class="poke foe" src="${foe.sprite}"></div><div class="grid2" style="margin-top:12px"><div class="mini"><b>${me.name}</b><div class="bar"><span class="hp" style="width:${Math.max(0,me.hp/me.maxHp*100)}%"></span></div><small>HP ${me.hp}/${me.maxHp}</small><div class="bar"><span class="en" style="width:${Math.max(0,me.energy/me.maxEnergy*100)}%"></span></div><small>Energy ${me.energy}/${me.maxEnergy}</small></div><div class="mini"><b>${foe.name}</b><div class="bar"><span class="hp" style="width:${Math.max(0,foe.hp/foe.maxHp*100)}%"></span></div><small>HP ${foe.hp}/${foe.maxHp}</small><div class="bar"><span class="en" style="width:${Math.max(0,foe.energy/foe.maxEnergy*100)}%"></span></div><small>Energy ${foe.energy}/${foe.maxEnergy}</small></div></div><div class="moves">${me.moves.map((mv,i)=>`<button class="move" onclick="useMove(${i})" ${S.myTurn&&me.energy>=mv.cost&&me.hp>0&&foe.hp>0&&!S.winner?'':'disabled'}>${mv.name}<br><small>${cap(mv.type)} • Power ${mv.power} • Cost ${mv.cost}</small></button>`).join('')}</div><div class="row" style="margin-top:12px"><button class="btn-blue" onclick="chargeEnergy()" ${S.myTurn&&me.hp>0&&!S.winner?'':'disabled'}>⚡ Tích năng lượng</button><button class="ghost" onclick="sendSync()">Đồng bộ lại</button></div><p class="muted">${S.winner?('Người thắng: '+S.winner):(S.myTurn?'Đến lượt bạn.':'Đang chờ đối thủ.')}</p>`
    }
    function renderTeam(){
      $('team').innerHTML=`<div class="card"><h2>📦 Chọn đội hình</h2><p class="muted">Chọn tối đa 3 Pokémon để đấu online. Đội hình lưu trên trình duyệt, không cần tài khoản.</p><div class="pokemon-grid">${starters.map((mon,i)=>`<div class="mon ${S.myTeam.some(x=>x.id===mon.id)?'active':''}" onclick="toggleTeam(${i})"><img src="${mon.sprite}"><b>${mon.name}</b><div>${mon.types.map(t=>`<span class="type">${cap(t)}</span>`).join('')}</div><div class="muted">HP ${mon.maxHp} • ATK ${mon.atk}</div></div>`).join('')}</div></div>`;
    }
    function renderGuide(){
      $('guide').innerHTML=`<div class="grid2"><div class="card"><h2>📘 Cách dùng</h2><ol class="muted"><li>Cả hai người mở cùng link game.</li><li>Người A vào tab Online Peer, bấm Tạo phòng.</li><li>Người A copy mã phòng gửi người B.</li><li>Người B nhập mã và bấm Vào phòng.</li><li>Người A bấm Bắt đầu trận.</li></ol><div class="warn"><b>Lưu ý:</b> cách PeerJS không lưu tài khoản/bạn bè lâu dài. Đây là online trực tiếp 1v1, đơn giản hơn Firebase.</div></div><div class="card"><h2>🚀 Đưa lên GitHub Pages</h2><p class="muted">Chỉ cần file index.html. Không cần npm, không cần build, không cần Firebase.</p><div class="code">repo/
├── index.html
├── README.md
└── LICENSE</div><p class="muted">Vì game dùng CDN PeerJS, người chơi vẫn cần mạng để tải thư viện PeerJS và ảnh Pokémon.</p></div></div>`;
    }

    function saveName(){S.playerName=($('nameInput').value||'Trainer').trim().slice(0,24);localStorage.setItem('peerName',S.playerName);addLog('Đã lưu tên: '+S.playerName)} window.saveName=saveName;
    function setupConn(conn){S.conn=conn;conn.on('open',()=>{S.connected=true;addLog('Đã kết nối với đối thủ.');send({type:'hello',name:S.playerName,team:S.myTeam});openTab('battle')});conn.on('data',onData);conn.on('close',()=>{S.connected=false;addLog('Đối thủ đã rời kết nối.');render()});conn.on('error',e=>{addLog('Lỗi kết nối: '+e);render()})}
    function createPeerRoom(){
      saveName();disconnectPeer(false);const id=roomId();S.host=true;S.myPeerId=id;S.peer=new Peer(id,{debug:1});
      S.peer.on('open',pid=>{S.myPeerId=pid;addLog('Đã tạo phòng: '+pid);render()});
      S.peer.on('connection',conn=>{addLog('Có người đang vào phòng...');setupConn(conn)});
      S.peer.on('error',e=>{addLog('Peer error: '+e.type+'. Hãy tạo mã khác hoặc tải lại trang.');render()});render();
    } window.createPeerRoom=createPeerRoom;
    function setJoinCode(value){S.joinCode=(value||'').trim();} window.setJoinCode=setJoinCode;
    function getJoinCode(){
      const byId=$('joinInput')?.value;
      const byQuery=document.querySelector('#online #joinInput')?.value;
      return ((byId||byQuery||S.joinCode||'')+'').trim();
    }
    function joinPeerRoomPrompt(){
      const typed=prompt('Dán mã phòng của bạn vào đây. Ví dụ: poke-ABCDE', getJoinCode());
      if(typed!==null){S.joinCode=typed.trim();joinPeerRoom();}
    } window.joinPeerRoomPrompt=joinPeerRoomPrompt;
    function joinPeerRoom(){
      let id=getJoinCode();
      if(!id){
        const typed=prompt('Game chưa đọc được ô mã phòng. Hãy dán mã phòng vào đây:', '');
        id=(typed||'').trim();
      }
      S.joinCode=id;
      if(!id)return toast('Vẫn chưa có mã phòng. Hãy copy đúng mã của chủ phòng, ví dụ poke-ABCDE, rồi dán vào ô hoặc hộp thoại.');
      const nameValue=($('nameInput')?.value||S.playerName||'Trainer').trim().slice(0,24);
      S.playerName=nameValue||'Trainer';
      localStorage.setItem('peerName',S.playerName);
      disconnectPeer(false);S.host=false;S.peer=new Peer(undefined,{debug:1});
      S.peer.on('open',()=>{S.myPeerId=S.peer.id;const conn=S.peer.connect(id,{reliable:true});setupConn(conn);addLog('Đang kết nối tới phòng '+id+'...');render()});
      S.peer.on('error',e=>{addLog('Peer error: '+e.type+'. Kiểm tra mã phòng hoặc mạng.');render()});
    } window.joinPeerRoom=joinPeerRoom;
    function disconnectPeer(logIt=true){try{if(S.conn)S.conn.close();if(S.peer)S.peer.destroy()}catch(e){}S.peer=null;S.conn=null;S.connected=false;S.myPeerId='';S.host=false;S.battleStarted=false;S.enemyTeam=[];if(logIt)addLog('Đã ngắt kết nối.');render()} window.disconnectPeer=disconnectPeer;
    function sendTeam(){send({type:'team',name:S.playerName,team:S.myTeam});addLog('Đã gửi đội hình cho đối thủ.')} window.sendTeam=sendTeam;
    function startBattle(){if(!S.host||!S.connected)return;resetBattle();S.battleStarted=true;S.myTurn=true;send({type:'start',team:S.myTeam});addLog('Trận đấu bắt đầu. Bạn đi trước.');openTab('battle')} window.startBattle=startBattle;
    function onData(d){
      if(!d||!d.type)return;
      if(d.type==='hello'){S.enemyTeam=clone(d.team||[]);addLog((d.name||'Đối thủ')+' đã kết nối.');send({type:'team',name:S.playerName,team:S.myTeam});render()}
      if(d.type==='team'){S.enemyTeam=clone(d.team||[]);addLog('Đã nhận đội hình của '+(d.name||'đối thủ')+'.');render()}
      if(d.type==='start'){resetBattle();S.enemyTeam=clone(d.team||S.enemyTeam);S.battleStarted=true;S.myTurn=false;addLog('Chủ phòng đã bắt đầu trận. Đối thủ đi trước.');openTab('battle')}
      if(d.type==='state'){S.enemyTeam=clone(d.myTeam);S.myTeam=clone(d.enemyTeam);S.myTurn=d.yourTurn;S.battleStarted=d.battleStarted;S.winner=d.winner||null;if(d.log)addLog(d.log);render()}
      if(d.type==='syncRequest'){sendSync()}
    }
    function current(){return {me:S.myTeam[S.myActive],foe:S.enemyTeam[S.enemyActive]}}
    function damage(att,def,mv){const crit=Math.random()<.12?1.65:1;const raw=mv.power+att.atk*.42-def.def*.18;const dmg=Math.max(4,Math.round(raw*crit*(.9+Math.random()*.22)));def.hp=Math.max(0,def.hp-dmg);att.energy=Math.min(att.maxEnergy,att.energy+10);return {dmg,crit:crit>1}}
    function nextAlive(team){return team.findIndex(x=>x.hp>0)}
    function useMove(i){const {me,foe}=current();if(!S.myTurn||!me||!foe)return;const mv=me.moves[i];if(me.energy<mv.cost)return;me.energy-=mv.cost;const r=damage(me,foe,mv);animate(mv.type);let text=me.name+' dùng '+mv.name+', gây '+r.dmg+' sát thương'+(r.crit?' chí mạng!':'!');let next=nextAlive(S.enemyTeam);if(foe.hp<=0){text+=' '+foe.name+' đã gục!';if(next>=0)S.enemyActive=next;else{S.winner=S.playerName;S.myTurn=false;sendState(text);addLog(text);return}}S.myTurn=false;sendState(text);addLog(text)} window.useMove=useMove;
    function chargeEnergy(){const {me}=current();if(!S.myTurn||!me)return;me.energy=Math.min(me.maxEnergy,me.energy+35);const text=me.name+' tích thêm năng lượng.';S.myTurn=false;sendState(text);addLog(text)} window.chargeEnergy=chargeEnergy;
    function sendState(text='Đồng bộ trạng thái trận đấu.'){send({type:'state',myTeam:S.myTeam,enemyTeam:S.enemyTeam,yourTurn:true,battleStarted:S.battleStarted,winner:S.winner,log:text});render()} window.sendSync=()=>{send({type:'state',myTeam:S.myTeam,enemyTeam:S.enemyTeam,yourTurn:S.myTurn,battleStarted:S.battleStarted,winner:S.winner,log:'Đã đồng bộ lại trận đấu.'});addLog('Đã gửi đồng bộ lại.')};
    function toggleTeam(index){const mon=clone(starters[index]);const exists=S.myTeam.some(x=>x.id===mon.id);if(exists)S.myTeam=S.myTeam.filter(x=>x.id!==mon.id);else{if(S.myTeam.length>=3)return toast('Đội tối đa 3 Pokémon.');S.myTeam.push(mon)}if(!S.myTeam.length)S.myTeam.push(clone(starters[0]));localStorage.setItem('peerTeam',JSON.stringify(S.myTeam));renderTeam()} window.toggleTeam=toggleTeam;
    function chooseActive(i){if(S.myTeam[i]?.hp>0){S.myActive=i;renderBattle()}} window.chooseActive=chooseActive;
    function animate(type){const fx=$('fx');if(!fx)return;fx.innerHTML='';const colors={fire:'#fb923c',water:'#38bdf8',grass:'#22c55e',electric:'#fde047',psychic:'#c084fc',normal:'#e2e8f0',poison:'#a855f7',flying:'#93c5fd',dragon:'#818cf8'};for(let i=0;i<12;i++){let p=document.createElement('div');p.className='particle';let s=rand(14,34);p.style.width=s+'px';p.style.height=s+'px';p.style.left=rand(130,230)+'px';p.style.top=rand(150,240)+'px';p.style.background='radial-gradient(circle,#fff,'+(colors[type]||'#fff')+')';p.style.setProperty('--dx',rand(260,430)+'px');p.style.setProperty('--dy',rand(-120,40)+'px');p.style.animationDelay=(i*.025)+'s';fx.appendChild(p)}setTimeout(()=>fx.innerHTML='',800)}
    render();
  </script>
</body>
</html>
  </style>
</head>
<body>
  <div class="app">
    <section class="hero">
      <div class="card">
        <h1>Pokemon Odyssey<br/>Peer Battle</h1>
        <p class="muted">Bản online không Firebase: dùng PeerJS để 2 người chơi kết nối trực tiếp bằng mã phòng. Rất hợp để đưa lên GitHub Pages vì không cần database, không cần đăng nhập.</p>
        <div class="row" style="margin-top:12px">
          <button onclick="openTab('online')">🌐 Tạo / nhập mã phòng</button>
          <button class="btn-green" onclick="openTab('battle')">⚔️ Đấu online</button>
          <button class="btn-blue" onclick="openTab('team')">📦 Chọn đội</button>
          <button class="ghost" onclick="openTab('guide')">📘 Hướng dẫn</button>
        </div>
      </div>
      <div class="card">
        <h3>Trạng thái</h3>
        <div class="list" id="status"></div>
      </div>
    </section>

    <nav class="tabs" id="tabs"></nav>

    <main>
      <section id="home" class="pane active"></section>
      <section id="online" class="pane"></section>
      <section id="battle" class="pane"></section>
      <section id="team" class="pane"></section>
      <section id="guide" class="pane"></section>
    </main>

    <footer class="footer">Pokemon Odyssey Peer Battle • Không Firebase • Không tài khoản • GitHub Pages ready</footer>
  </div>

  <script src="https://unpkg.com/peerjs@1.5.4/dist/peerjs.min.js"></script>
  <script>
    const tabs = [["home","🏠 Trang chủ"],["online","🌐 Online Peer"],["battle","⚔️ Battle"],["team","📦 Đội hình"],["guide","📘 Hướng dẫn"]];
    const starters = [
      {id:1,name:"Bulbasaur",types:["grass","poison"],hp:116,maxHp:116,energy:40,maxEnergy:100,atk:48,def:44,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png",moves:[m("Leaf Cutter","grass",20,0),m("Vine Lash","grass",34,15),m("Toxic Bloom","poison",45,30),m("Solar Storm","grass",68,50)]},
      {id:4,name:"Charmander",types:["fire"],hp:104,maxHp:104,energy:45,maxEnergy:100,atk:55,def:38,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/4.png",moves:[m("Ember Burst","fire",21,0),m("Flame Dash","fire",34,15),m("Inferno Fang","fire",48,32),m("Solar Inferno","fire",70,52)]},
      {id:7,name:"Squirtle",types:["water"],hp:112,maxHp:112,energy:40,maxEnergy:100,atk:45,def:60,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png",moves:[m("Bubble Jet","water",19,0),m("Aqua Slash","water",33,14),m("Tidal Crush","water",47,31),m("Ocean Breaker","water",69,52)]},
      {id:25,name:"Pikachu",types:["electric"],hp:96,maxHp:96,energy:55,maxEnergy:110,atk:58,def:35,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png",moves:[m("Spark Bolt","electric",20,0),m("Volt Dash","electric",36,16),m("Thunder Cage","electric",51,34),m("Heaven Thunder","electric",74,55)]},
      {id:133,name:"Eevee",types:["normal"],hp:110,maxHp:110,energy:45,maxEnergy:100,atk:52,def:45,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/133.png",moves:[m("Quick Strike","normal",20,0),m("Double Hit","normal",35,15),m("Adaptive Rush","normal",49,32),m("Evolution Pulse","normal",72,55)]},
      {id:150,name:"Mewtwo",types:["psychic"],hp:140,maxHp:140,energy:60,maxEnergy:120,atk:70,def:55,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/150.png",moves:[m("Mind Tap","psychic",24,0),m("Psy Cut","psychic",40,18),m("Dream Nova","psychic",58,38),m("Astral Collapse","psychic",86,62)]},
      {id:6,name:"Charizard",types:["fire","flying"],hp:132,maxHp:132,energy:55,maxEnergy:115,atk:68,def:58,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/6.png",moves:[m("Flame Wing","fire",26,0),m("Air Cutter","flying",38,18),m("Dragon Heat","dragon",56,36),m("Volcano Sky","fire",82,60)]},
      {id:9,name:"Blastoise",types:["water"],hp:145,maxHp:145,energy:50,maxEnergy:110,atk:62,def:72,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/9.png",moves:[m("Water Cannon","water",25,0),m("Shell Guard","water",34,14),m("Hydro Crush","water",56,36),m("Ocean Fortress","water",80,60)]}
    ];
    function m(name,type,power,cost){return {name,type,power,cost}}
    const S = {
      tab:"home", peer:null, conn:null, myPeerId:"", host:false, connected:false, playerName:localStorage.getItem('peerName')||'Trainer',
      myTeam:JSON.parse(localStorage.getItem('peerTeam')||'null')||[clone(starters[0]),clone(starters[3]),clone(starters[4])],
      enemyTeam:[], myActive:0, enemyActive:0, myTurn:false, battleStarted:false, winner:null,
      log:["Chào mừng đến Peer Battle. Người A tạo mã, người B nhập mã để vào."]
    };
    const $=id=>document.getElementById(id);const cap=s=>s?s.charAt(0).toUpperCase()+s.slice(1):'';const rand=(a,b)=>Math.floor(Math.random()*(b-a+1))+a;function clone(x){return JSON.parse(JSON.stringify(x))}
    function openTab(id){S.tab=id;document.querySelectorAll('.pane').forEach(p=>p.classList.remove('active'));$(id).classList.add('active');render()} window.openTab=openTab;
    function addLog(msg){S.log.unshift('• '+msg);S.log=S.log.slice(0,80);render()} function toast(msg){alert(msg)}
    function roomId(){return 'poke-'+Math.random().toString(36).slice(2,7).toUpperCase()}
    function send(data){if(S.conn&&S.conn.open)S.conn.send(data)}
    function resetBattle(){S.enemyTeam=[];S.myActive=0;S.enemyActive=0;S.myTurn=false;S.battleStarted=false;S.winner=null;S.myTeam=S.myTeam.map(x=>{let y=clone(x);y.hp=y.maxHp;y.energy=Math.max(40,y.energy||40);return y});}

    function render(){renderShell();renderHome();renderOnline();renderBattle();renderTeam();renderGuide()}
    function renderShell(){
      $('tabs').innerHTML=tabs.map(([id,label])=>`<button class="tab ${S.tab===id?'active':''}" onclick="openTab('${id}')">${label}</button>`).join('');
      $('status').innerHTML=`
        <div class="stat"><span class="dot ${window.Peer?'ok':''}"></span>PeerJS: ${window.Peer?'đã tải':'chưa tải'}</div>
        <div class="stat"><span class="dot ${S.peer?'ok':''}"></span>Phòng của bạn: <span class="copy">${S.myPeerId||'chưa tạo'}</span></div>
        <div class="stat"><span class="dot ${S.connected?'ok':''}"></span>Kết nối: ${S.connected?'đã có đối thủ':'chưa kết nối'}</div>
        <div class="stat">Vai trò: ${S.host?'Chủ phòng':'Người tham gia / chưa chọn'}</div>
        <div class="stat">Lượt: ${S.battleStarted?(S.myTurn?'bạn':'đối thủ'):'chưa bắt đầu'}</div>`;
    }
    function renderHome(){
      $('home').innerHTML=`<div class="grid2"><div class="card"><h2>🎮 Online đơn giản hơn Firebase</h2><p class="muted">Cách này dùng PeerJS. Không lưu hồ sơ lên server, không cần Firebase Rules. Một người tạo mã phòng, người kia nhập mã. Hai trình duyệt kết nối trực tiếp với nhau.</p><div class="grid3"><div class="mini"><h3>1. Tạo mã</h3><p class="muted">Người A bấm Tạo phòng.</p></div><div class="mini"><h3>2. Gửi mã</h3><p class="muted">Copy mã phòng gửi bạn.</p></div><div class="mini"><h3>3. Đấu</h3><p class="muted">Người B nhập mã rồi vào trận.</p></div></div><div class="row" style="margin-top:12px"><button onclick="openTab('online')">Bắt đầu online</button><button class="btn-blue" onclick="openTab('team')">Chọn đội</button></div></div><div class="card"><h2>📜 Nhật ký</h2><div class="log">${S.log.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`;
    }
    function renderOnline(){
      $('online').innerHTML=`<div class="grid2"><div class="card"><h2>🌐 Tạo phòng</h2><p class="muted">Người tạo phòng bấm nút dưới, sau đó gửi mã phòng cho bạn.</p><div class="row"><input id="nameInput" placeholder="Tên của bạn" value="${S.playerName}"><button onclick="saveName()">Lưu tên</button></div><div class="row" style="margin-top:12px"><button onclick="createPeerRoom()">🏠 Tạo phòng</button><button class="btn-red" onclick="disconnectPeer()">Ngắt kết nối</button></div><div class="mini" style="margin-top:12px"><b>Mã phòng của bạn</b><h2 class="copy">${S.myPeerId||'------'}</h2><p class="muted">Gửi mã này cho bạn. Ví dụ qua Messenger, Zalo, Discord.</p></div></div><div class="card"><h2>🚪 Vào phòng</h2><p class="muted">Người tham gia nhập mã phòng của chủ phòng.</p><div class="row"><input id="joinInput" placeholder="Nhập mã phòng, ví dụ poke-ABCDE"><button class="btn-blue" onclick="joinPeerRoom()">Vào phòng</button></div><div class="good" style="margin-top:12px"><b>Không cần Firebase.</b><br>Nhưng cả hai người phải đang mở game cùng lúc. Nếu chủ phòng tắt tab, phòng cũng mất.</div></div></div>`;
    }
    function monBox(mon,i,active){return `<div class="mon ${active?'active':''}" onclick="chooseActive(${i})"><img src="${mon.sprite}"><b>${mon.name}</b><div>${mon.types.map(t=>`<span class="type">${cap(t)}</span>`).join('')}</div><div class="muted">HP ${mon.hp}/${mon.maxHp} • EN ${mon.energy}/${mon.maxEnergy}</div></div>`}
    function renderBattle(){
      const me=S.myTeam[S.myActive], foe=S.enemyTeam[S.enemyActive];
      $('battle').innerHTML=`<div class="grid2"><div class="card"><h2>⚔️ Peer PvP Battle</h2>${S.battleStarted&&me&&foe?battleHtml(me,foe):preBattleHtml()}</div><div class="card"><h2>📜 Battle log</h2><div class="log">${S.log.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`;
    }
    function preBattleHtml(){return `<div class="mini"><p class="muted">Kết nối với bạn trước, rồi chủ phòng bấm bắt đầu trận.</p><div class="row"><button class="btn-green" onclick="startBattle()" ${S.connected&&S.host?'':'disabled'}>Bắt đầu trận</button><button class="btn-blue" onclick="sendTeam()" ${S.connected?'':'disabled'}>Gửi lại đội hình</button></div></div>`}
    function battleHtml(me,foe){
      return `<div class="battle-scene" id="scene"><div class="fx" id="fx"></div><div class="shadow left"></div><div class="shadow right"></div><img class="poke me" src="${me.sprite}"><img class="poke foe" src="${foe.sprite}"></div><div class="grid2" style="margin-top:12px"><div class="mini"><b>${me.name}</b><div class="bar"><span class="hp" style="width:${Math.max(0,me.hp/me.maxHp*100)}%"></span></div><small>HP ${me.hp}/${me.maxHp}</small><div class="bar"><span class="en" style="width:${Math.max(0,me.energy/me.maxEnergy*100)}%"></span></div><small>Energy ${me.energy}/${me.maxEnergy}</small></div><div class="mini"><b>${foe.name}</b><div class="bar"><span class="hp" style="width:${Math.max(0,foe.hp/foe.maxHp*100)}%"></span></div><small>HP ${foe.hp}/${foe.maxHp}</small><div class="bar"><span class="en" style="width:${Math.max(0,foe.energy/foe.maxEnergy*100)}%"></span></div><small>Energy ${foe.energy}/${foe.maxEnergy}</small></div></div><div class="moves">${me.moves.map((mv,i)=>`<button class="move" onclick="useMove(${i})" ${S.myTurn&&me.energy>=mv.cost&&me.hp>0&&foe.hp>0&&!S.winner?'':'disabled'}>${mv.name}<br><small>${cap(mv.type)} • Power ${mv.power} • Cost ${mv.cost}</small></button>`).join('')}</div><div class="row" style="margin-top:12px"><button class="btn-blue" onclick="chargeEnergy()" ${S.myTurn&&me.hp>0&&!S.winner?'':'disabled'}>⚡ Tích năng lượng</button><button class="ghost" onclick="sendSync()">Đồng bộ lại</button></div><p class="muted">${S.winner?('Người thắng: '+S.winner):(S.myTurn?'Đến lượt bạn.':'Đang chờ đối thủ.')}</p>`
    }
    function renderTeam(){
      $('team').innerHTML=`<div class="card"><h2>📦 Chọn đội hình</h2><p class="muted">Chọn tối đa 3 Pokémon để đấu online. Đội hình lưu trên trình duyệt, không cần tài khoản.</p><div class="pokemon-grid">${starters.map((mon,i)=>`<div class="mon ${S.myTeam.some(x=>x.id===mon.id)?'active':''}" onclick="toggleTeam(${i})"><img src="${mon.sprite}"><b>${mon.name}</b><div>${mon.types.map(t=>`<span class="type">${cap(t)}</span>`).join('')}</div><div class="muted">HP ${mon.maxHp} • ATK ${mon.atk}</div></div>`).join('')}</div></div>`;
    }
    function renderGuide(){
      $('guide').innerHTML=`<div class="grid2"><div class="card"><h2>📘 Cách dùng</h2><ol class="muted"><li>Cả hai người mở cùng link game.</li><li>Người A vào tab Online Peer, bấm Tạo phòng.</li><li>Người A copy mã phòng gửi người B.</li><li>Người B nhập mã và bấm Vào phòng.</li><li>Người A bấm Bắt đầu trận.</li></ol><div class="warn"><b>Lưu ý:</b> cách PeerJS không lưu tài khoản/bạn bè lâu dài. Đây là online trực tiếp 1v1, đơn giản hơn Firebase.</div></div><div class="card"><h2>🚀 Đưa lên GitHub Pages</h2><p class="muted">Chỉ cần file index.html. Không cần npm, không cần build, không cần Firebase.</p><div class="code">repo/
├── index.html
├── README.md
└── LICENSE</div><p class="muted">Vì game dùng CDN PeerJS, người chơi vẫn cần mạng để tải thư viện PeerJS và ảnh Pokémon.</p></div></div>`;
    }

    function saveName(){S.playerName=($('nameInput').value||'Trainer').trim().slice(0,24);localStorage.setItem('peerName',S.playerName);addLog('Đã lưu tên: '+S.playerName)} window.saveName=saveName;
    function setupConn(conn){S.conn=conn;conn.on('open',()=>{S.connected=true;addLog('Đã kết nối với đối thủ.');send({type:'hello',name:S.playerName,team:S.myTeam});openTab('battle')});conn.on('data',onData);conn.on('close',()=>{S.connected=false;addLog('Đối thủ đã rời kết nối.');render()});conn.on('error',e=>{addLog('Lỗi kết nối: '+e);render()})}
    function createPeerRoom(){
      saveName();disconnectPeer(false);const id=roomId();S.host=true;S.myPeerId=id;S.peer=new Peer(id,{debug:1});
      S.peer.on('open',pid=>{S.myPeerId=pid;addLog('Đã tạo phòng: '+pid);render()});
      S.peer.on('connection',conn=>{addLog('Có người đang vào phòng...');setupConn(conn)});
      S.peer.on('error',e=>{addLog('Peer error: '+e.type+'. Hãy tạo mã khác hoặc tải lại trang.');render()});render();
    } window.createPeerRoom=createPeerRoom;
    function joinPeerRoom(){
      const id=($('joinInput')?.value||'').trim();
      if(!id)return toast('Nhập mã phòng trước.');
      const nameValue=($('nameInput')?.value||S.playerName||'Trainer').trim().slice(0,24);
      S.playerName=nameValue||'Trainer';
      localStorage.setItem('peerName',S.playerName);
      disconnectPeer(false);S.host=false;S.peer=new Peer(undefined,{debug:1});
      S.peer.on('open',()=>{S.myPeerId=S.peer.id;const conn=S.peer.connect(id,{reliable:true});setupConn(conn);addLog('Đang kết nối tới phòng '+id+'...');render()});
      S.peer.on('error',e=>{addLog('Peer error: '+e.type+'. Kiểm tra mã phòng hoặc mạng.');render()});
    } window.joinPeerRoom=joinPeerRoom;
    function disconnectPeer(logIt=true){try{if(S.conn)S.conn.close();if(S.peer)S.peer.destroy()}catch(e){}S.peer=null;S.conn=null;S.connected=false;S.myPeerId='';S.host=false;S.battleStarted=false;S.enemyTeam=[];if(logIt)addLog('Đã ngắt kết nối.');render()} window.disconnectPeer=disconnectPeer;
    function sendTeam(){send({type:'team',name:S.playerName,team:S.myTeam});addLog('Đã gửi đội hình cho đối thủ.')} window.sendTeam=sendTeam;
    function startBattle(){if(!S.host||!S.connected)return;resetBattle();S.battleStarted=true;S.myTurn=true;send({type:'start',team:S.myTeam});addLog('Trận đấu bắt đầu. Bạn đi trước.');openTab('battle')} window.startBattle=startBattle;
    function onData(d){
      if(!d||!d.type)return;
      if(d.type==='hello'){S.enemyTeam=clone(d.team||[]);addLog((d.name||'Đối thủ')+' đã kết nối.');send({type:'team',name:S.playerName,team:S.myTeam});render()}
      if(d.type==='team'){S.enemyTeam=clone(d.team||[]);addLog('Đã nhận đội hình của '+(d.name||'đối thủ')+'.');render()}
      if(d.type==='start'){resetBattle();S.enemyTeam=clone(d.team||S.enemyTeam);S.battleStarted=true;S.myTurn=false;addLog('Chủ phòng đã bắt đầu trận. Đối thủ đi trước.');openTab('battle')}
      if(d.type==='state'){S.enemyTeam=clone(d.myTeam);S.myTeam=clone(d.enemyTeam);S.myTurn=d.yourTurn;S.battleStarted=d.battleStarted;S.winner=d.winner||null;if(d.log)addLog(d.log);render()}
      if(d.type==='syncRequest'){sendSync()}
    }
    function current(){return {me:S.myTeam[S.myActive],foe:S.enemyTeam[S.enemyActive]}}
    function damage(att,def,mv){const crit=Math.random()<.12?1.65:1;const raw=mv.power+att.atk*.42-def.def*.18;const dmg=Math.max(4,Math.round(raw*crit*(.9+Math.random()*.22)));def.hp=Math.max(0,def.hp-dmg);att.energy=Math.min(att.maxEnergy,att.energy+10);return {dmg,crit:crit>1}}
    function nextAlive(team){return team.findIndex(x=>x.hp>0)}
    function useMove(i){const {me,foe}=current();if(!S.myTurn||!me||!foe)return;const mv=me.moves[i];if(me.energy<mv.cost)return;me.energy-=mv.cost;const r=damage(me,foe,mv);animate(mv.type);let text=me.name+' dùng '+mv.name+', gây '+r.dmg+' sát thương'+(r.crit?' chí mạng!':'!');let next=nextAlive(S.enemyTeam);if(foe.hp<=0){text+=' '+foe.name+' đã gục!';if(next>=0)S.enemyActive=next;else{S.winner=S.playerName;S.myTurn=false;sendState(text);addLog(text);return}}S.myTurn=false;sendState(text);addLog(text)} window.useMove=useMove;
    function chargeEnergy(){const {me}=current();if(!S.myTurn||!me)return;me.energy=Math.min(me.maxEnergy,me.energy+35);const text=me.name+' tích thêm năng lượng.';S.myTurn=false;sendState(text);addLog(text)} window.chargeEnergy=chargeEnergy;
    function sendState(text='Đồng bộ trạng thái trận đấu.'){send({type:'state',myTeam:S.myTeam,enemyTeam:S.enemyTeam,yourTurn:true,battleStarted:S.battleStarted,winner:S.winner,log:text});render()} window.sendSync=()=>{send({type:'state',myTeam:S.myTeam,enemyTeam:S.enemyTeam,yourTurn:S.myTurn,battleStarted:S.battleStarted,winner:S.winner,log:'Đã đồng bộ lại trận đấu.'});addLog('Đã gửi đồng bộ lại.')};
    function toggleTeam(index){const mon=clone(starters[index]);const exists=S.myTeam.some(x=>x.id===mon.id);if(exists)S.myTeam=S.myTeam.filter(x=>x.id!==mon.id);else{if(S.myTeam.length>=3)return toast('Đội tối đa 3 Pokémon.');S.myTeam.push(mon)}if(!S.myTeam.length)S.myTeam.push(clone(starters[0]));localStorage.setItem('peerTeam',JSON.stringify(S.myTeam));renderTeam()} window.toggleTeam=toggleTeam;
    function chooseActive(i){if(S.myTeam[i]?.hp>0){S.myActive=i;renderBattle()}} window.chooseActive=chooseActive;
    function animate(type){const fx=$('fx');if(!fx)return;fx.innerHTML='';const colors={fire:'#fb923c',water:'#38bdf8',grass:'#22c55e',electric:'#fde047',psychic:'#c084fc',normal:'#e2e8f0',poison:'#a855f7',flying:'#93c5fd',dragon:'#818cf8'};for(let i=0;i<12;i++){let p=document.createElement('div');p.className='particle';let s=rand(14,34);p.style.width=s+'px';p.style.height=s+'px';p.style.left=rand(130,230)+'px';p.style.top=rand(150,240)+'px';p.style.background='radial-gradient(circle,#fff,'+(colors[type]||'#fff')+')';p.style.setProperty('--dx',rand(260,430)+'px');p.style.setProperty('--dy',rand(-120,40)+'px');p.style.animationDelay=(i*.025)+'s';fx.appendChild(p)}setTimeout(()=>fx.innerHTML='',800)}
    render();
  </script>
</body>
</html>
  </style>
</head>
<body>
  <div class="app">
    <section class="hero">
      <div class="card">
        <h1>Pokemon Odyssey<br/>Peer Battle</h1>
        <p class="muted">Bản online không Firebase: dùng PeerJS để 2 người chơi kết nối trực tiếp bằng mã phòng. Rất hợp để đưa lên GitHub Pages vì không cần database, không cần đăng nhập.</p>
        <div class="row" style="margin-top:12px">
          <button onclick="openTab('online')">🌐 Tạo / nhập mã phòng</button>
          <button class="btn-green" onclick="openTab('battle')">⚔️ Đấu online</button>
          <button class="btn-blue" onclick="openTab('team')">📦 Chọn đội</button>
          <button class="ghost" onclick="openTab('guide')">📘 Hướng dẫn</button>
        </div>
      </div>
      <div class="card">
        <h3>Trạng thái</h3>
        <div class="list" id="status"></div>
      </div>
    </section>

    <nav class="tabs" id="tabs"></nav>

    <main>
      <section id="home" class="pane active"></section>
      <section id="online" class="pane"></section>
      <section id="battle" class="pane"></section>
      <section id="team" class="pane"></section>
      <section id="guide" class="pane"></section>
    </main>

    <footer class="footer">Pokemon Odyssey Peer Battle • Không Firebase • Không tài khoản • GitHub Pages ready</footer>
  </div>

  <script src="https://unpkg.com/peerjs@1.5.4/dist/peerjs.min.js"></script>
  <script>
    const tabs = [["home","🏠 Trang chủ"],["online","🌐 Online Peer"],["battle","⚔️ Battle"],["team","📦 Đội hình"],["guide","📘 Hướng dẫn"]];
    const starters = [
      {id:1,name:"Bulbasaur",types:["grass","poison"],hp:116,maxHp:116,energy:40,maxEnergy:100,atk:48,def:44,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/1.png",moves:[m("Leaf Cutter","grass",20,0),m("Vine Lash","grass",34,15),m("Toxic Bloom","poison",45,30),m("Solar Storm","grass",68,50)]},
      {id:4,name:"Charmander",types:["fire"],hp:104,maxHp:104,energy:45,maxEnergy:100,atk:55,def:38,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/4.png",moves:[m("Ember Burst","fire",21,0),m("Flame Dash","fire",34,15),m("Inferno Fang","fire",48,32),m("Solar Inferno","fire",70,52)]},
      {id:7,name:"Squirtle",types:["water"],hp:112,maxHp:112,energy:40,maxEnergy:100,atk:45,def:60,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/7.png",moves:[m("Bubble Jet","water",19,0),m("Aqua Slash","water",33,14),m("Tidal Crush","water",47,31),m("Ocean Breaker","water",69,52)]},
      {id:25,name:"Pikachu",types:["electric"],hp:96,maxHp:96,energy:55,maxEnergy:110,atk:58,def:35,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/25.png",moves:[m("Spark Bolt","electric",20,0),m("Volt Dash","electric",36,16),m("Thunder Cage","electric",51,34),m("Heaven Thunder","electric",74,55)]},
      {id:133,name:"Eevee",types:["normal"],hp:110,maxHp:110,energy:45,maxEnergy:100,atk:52,def:45,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/133.png",moves:[m("Quick Strike","normal",20,0),m("Double Hit","normal",35,15),m("Adaptive Rush","normal",49,32),m("Evolution Pulse","normal",72,55)]},
      {id:150,name:"Mewtwo",types:["psychic"],hp:140,maxHp:140,energy:60,maxEnergy:120,atk:70,def:55,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/150.png",moves:[m("Mind Tap","psychic",24,0),m("Psy Cut","psychic",40,18),m("Dream Nova","psychic",58,38),m("Astral Collapse","psychic",86,62)]},
      {id:6,name:"Charizard",types:["fire","flying"],hp:132,maxHp:132,energy:55,maxEnergy:115,atk:68,def:58,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/6.png",moves:[m("Flame Wing","fire",26,0),m("Air Cutter","flying",38,18),m("Dragon Heat","dragon",56,36),m("Volcano Sky","fire",82,60)]},
      {id:9,name:"Blastoise",types:["water"],hp:145,maxHp:145,energy:50,maxEnergy:110,atk:62,def:72,sprite:"https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/9.png",moves:[m("Water Cannon","water",25,0),m("Shell Guard","water",34,14),m("Hydro Crush","water",56,36),m("Ocean Fortress","water",80,60)]}
    ];
    function m(name,type,power,cost){return {name,type,power,cost}}
    const S = {
      tab:"home", peer:null, conn:null, myPeerId:"", host:false, connected:false, playerName:localStorage.getItem('peerName')||'Trainer',
      myTeam:JSON.parse(localStorage.getItem('peerTeam')||'null')||[clone(starters[0]),clone(starters[3]),clone(starters[4])],
      enemyTeam:[], myActive:0, enemyActive:0, myTurn:false, battleStarted:false, winner:null,
      log:["Chào mừng đến Peer Battle. Người A tạo mã, người B nhập mã để vào."]
    };
    const $=id=>document.getElementById(id);const cap=s=>s?s.charAt(0).toUpperCase()+s.slice(1):'';const rand=(a,b)=>Math.floor(Math.random()*(b-a+1))+a;function clone(x){return JSON.parse(JSON.stringify(x))}
    function openTab(id){S.tab=id;document.querySelectorAll('.pane').forEach(p=>p.classList.remove('active'));$(id).classList.add('active');render()} window.openTab=openTab;
    function addLog(msg){S.log.unshift('• '+msg);S.log=S.log.slice(0,80);render()} function toast(msg){alert(msg)}
    function roomId(){return 'poke-'+Math.random().toString(36).slice(2,7).toUpperCase()}
    function send(data){if(S.conn&&S.conn.open)S.conn.send(data)}
    function resetBattle(){S.enemyTeam=[];S.myActive=0;S.enemyActive=0;S.myTurn=false;S.battleStarted=false;S.winner=null;S.myTeam=S.myTeam.map(x=>{let y=clone(x);y.hp=y.maxHp;y.energy=Math.max(40,y.energy||40);return y});}

    function render(){renderShell();renderHome();renderOnline();renderBattle();renderTeam();renderGuide()}
    function renderShell(){
      $('tabs').innerHTML=tabs.map(([id,label])=>`<button class="tab ${S.tab===id?'active':''}" onclick="openTab('${id}')">${label}</button>`).join('');
      $('status').innerHTML=`
        <div class="stat"><span class="dot ${window.Peer?'ok':''}"></span>PeerJS: ${window.Peer?'đã tải':'chưa tải'}</div>
        <div class="stat"><span class="dot ${S.peer?'ok':''}"></span>Phòng của bạn: <span class="copy">${S.myPeerId||'chưa tạo'}</span></div>
        <div class="stat"><span class="dot ${S.connected?'ok':''}"></span>Kết nối: ${S.connected?'đã có đối thủ':'chưa kết nối'}</div>
        <div class="stat">Vai trò: ${S.host?'Chủ phòng':'Người tham gia / chưa chọn'}</div>
        <div class="stat">Lượt: ${S.battleStarted?(S.myTurn?'bạn':'đối thủ'):'chưa bắt đầu'}</div>`;
    }
    function renderHome(){
      $('home').innerHTML=`<div class="grid2"><div class="card"><h2>🎮 Online đơn giản hơn Firebase</h2><p class="muted">Cách này dùng PeerJS. Không lưu hồ sơ lên server, không cần Firebase Rules. Một người tạo mã phòng, người kia nhập mã. Hai trình duyệt kết nối trực tiếp với nhau.</p><div class="grid3"><div class="mini"><h3>1. Tạo mã</h3><p class="muted">Người A bấm Tạo phòng.</p></div><div class="mini"><h3>2. Gửi mã</h3><p class="muted">Copy mã phòng gửi bạn.</p></div><div class="mini"><h3>3. Đấu</h3><p class="muted">Người B nhập mã rồi vào trận.</p></div></div><div class="row" style="margin-top:12px"><button onclick="openTab('online')">Bắt đầu online</button><button class="btn-blue" onclick="openTab('team')">Chọn đội</button></div></div><div class="card"><h2>📜 Nhật ký</h2><div class="log">${S.log.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`;
    }
    function renderOnline(){
      $('online').innerHTML=`<div class="grid2"><div class="card"><h2>🌐 Tạo phòng</h2><p class="muted">Người tạo phòng bấm nút dưới, sau đó gửi mã phòng cho bạn.</p><div class="row"><input id="nameInput" placeholder="Tên của bạn" value="${S.playerName}"><button onclick="saveName()">Lưu tên</button></div><div class="row" style="margin-top:12px"><button onclick="createPeerRoom()">🏠 Tạo phòng</button><button class="btn-red" onclick="disconnectPeer()">Ngắt kết nối</button></div><div class="mini" style="margin-top:12px"><b>Mã phòng của bạn</b><h2 class="copy">${S.myPeerId||'------'}</h2><p class="muted">Gửi mã này cho bạn. Ví dụ qua Messenger, Zalo, Discord.</p></div></div><div class="card"><h2>🚪 Vào phòng</h2><p class="muted">Người tham gia nhập mã phòng của chủ phòng.</p><div class="row"><input id="joinInput" placeholder="Nhập mã phòng, ví dụ poke-ABCDE"><button class="btn-blue" onclick="joinPeerRoom()">Vào phòng</button></div><div class="good" style="margin-top:12px"><b>Không cần Firebase.</b><br>Nhưng cả hai người phải đang mở game cùng lúc. Nếu chủ phòng tắt tab, phòng cũng mất.</div></div></div>`;
    }
    function monBox(mon,i,active){return `<div class="mon ${active?'active':''}" onclick="chooseActive(${i})"><img src="${mon.sprite}"><b>${mon.name}</b><div>${mon.types.map(t=>`<span class="type">${cap(t)}</span>`).join('')}</div><div class="muted">HP ${mon.hp}/${mon.maxHp} • EN ${mon.energy}/${mon.maxEnergy}</div></div>`}
    function renderBattle(){
      const me=S.myTeam[S.myActive], foe=S.enemyTeam[S.enemyActive];
      $('battle').innerHTML=`<div class="grid2"><div class="card"><h2>⚔️ Peer PvP Battle</h2>${S.battleStarted&&me&&foe?battleHtml(me,foe):preBattleHtml()}</div><div class="card"><h2>📜 Battle log</h2><div class="log">${S.log.map(x=>`<div>${x}</div>`).join('')}</div></div></div>`;
    }
    function preBattleHtml(){return `<div class="mini"><p class="muted">Kết nối với bạn trước, rồi chủ phòng bấm bắt đầu trận.</p><div class="row"><button class="btn-green" onclick="startBattle()" ${S.connected&&S.host?'':'disabled'}>Bắt đầu trận</button><button class="btn-blue" onclick="sendTeam()" ${S.connected?'':'disabled'}>Gửi lại đội hình</button></div></div>`}
    function battleHtml(me,foe){
      return `<div class="battle-scene" id="scene"><div class="fx" id="fx"></div><div class="shadow left"></div><div class="shadow right"></div><img class="poke me" src="${me.sprite}"><img class="poke foe" src="${foe.sprite}"></div><div class="grid2" style="margin-top:12px"><div class="mini"><b>${me.name}</b><div class="bar"><span class="hp" style="width:${Math.max(0,me.hp/me.maxHp*100)}%"></span></div><small>HP ${me.hp}/${me.maxHp}</small><div class="bar"><span class="en" style="width:${Math.max(0,me.energy/me.maxEnergy*100)}%"></span></div><small>Energy ${me.energy}/${me.maxEnergy}</small></div><div class="mini"><b>${foe.name}</b><div class="bar"><span class="hp" style="width:${Math.max(0,foe.hp/foe.maxHp*100)}%"></span></div><small>HP ${foe.hp}/${foe.maxHp}</small><div class="bar"><span class="en" style="width:${Math.max(0,foe.energy/foe.maxEnergy*100)}%"></span></div><small>Energy ${foe.energy}/${foe.maxEnergy}</small></div></div><div class="moves">${me.moves.map((mv,i)=>`<button class="move" onclick="useMove(${i})" ${S.myTurn&&me.energy>=mv.cost&&me.hp>0&&foe.hp>0&&!S.winner?'':'disabled'}>${mv.name}<br><small>${cap(mv.type)} • Power ${mv.power} • Cost ${mv.cost}</small></button>`).join('')}</div><div class="row" style="margin-top:12px"><button class="btn-blue" onclick="chargeEnergy()" ${S.myTurn&&me.hp>0&&!S.winner?'':'disabled'}>⚡ Tích năng lượng</button><button class="ghost" onclick="sendSync()">Đồng bộ lại</button></div><p class="muted">${S.winner?('Người thắng: '+S.winner):(S.myTurn?'Đến lượt bạn.':'Đang chờ đối thủ.')}</p>`
    }
    function renderTeam(){
      $('team').innerHTML=`<div class="card"><h2>📦 Chọn đội hình</h2><p class="muted">Chọn tối đa 3 Pokémon để đấu online. Đội hình lưu trên trình duyệt, không cần tài khoản.</p><div class="pokemon-grid">${starters.map((mon,i)=>`<div class="mon ${S.myTeam.some(x=>x.id===mon.id)?'active':''}" onclick="toggleTeam(${i})"><img src="${mon.sprite}"><b>${mon.name}</b><div>${mon.types.map(t=>`<span class="type">${cap(t)}</span>`).join('')}</div><div class="muted">HP ${mon.maxHp} • ATK ${mon.atk}</div></div>`).join('')}</div></div>`;
    }
    function renderGuide(){
      $('guide').innerHTML=`<div class="grid2"><div class="card"><h2>📘 Cách dùng</h2><ol class="muted"><li>Cả hai người mở cùng link game.</li><li>Người A vào tab Online Peer, bấm Tạo phòng.</li><li>Người A copy mã phòng gửi người B.</li><li>Người B nhập mã và bấm Vào phòng.</li><li>Người A bấm Bắt đầu trận.</li></ol><div class="warn"><b>Lưu ý:</b> cách PeerJS không lưu tài khoản/bạn bè lâu dài. Đây là online trực tiếp 1v1, đơn giản hơn Firebase.</div></div><div class="card"><h2>🚀 Đưa lên GitHub Pages</h2><p class="muted">Chỉ cần file index.html. Không cần npm, không cần build, không cần Firebase.</p><div class="code">repo/
├── index.html
├── README.md
└── LICENSE</div><p class="muted">Vì game dùng CDN PeerJS, người chơi vẫn cần mạng để tải thư viện PeerJS và ảnh Pokémon.</p></div></div>`;
    }

    function saveName(){S.playerName=($('nameInput').value||'Trainer').trim().slice(0,24);localStorage.setItem('peerName',S.playerName);addLog('Đã lưu tên: '+S.playerName)} window.saveName=saveName;
    function setupConn(conn){S.conn=conn;conn.on('open',()=>{S.connected=true;addLog('Đã kết nối với đối thủ.');send({type:'hello',name:S.playerName,team:S.myTeam});openTab('battle')});conn.on('data',onData);conn.on('close',()=>{S.connected=false;addLog('Đối thủ đã rời kết nối.');render()});conn.on('error',e=>{addLog('Lỗi kết nối: '+e);render()})}
    function createPeerRoom(){
      saveName();disconnectPeer(false);const id=roomId();S.host=true;S.myPeerId=id;S.peer=new Peer(id,{debug:1});
      S.peer.on('open',pid=>{S.myPeerId=pid;addLog('Đã tạo phòng: '+pid);render()});
      S.peer.on('connection',conn=>{addLog('Có người đang vào phòng...');setupConn(conn)});
      S.peer.on('error',e=>{addLog('Peer error: '+e.type+'. Hãy tạo mã khác hoặc tải lại trang.');render()});render();
    } window.createPeerRoom=createPeerRoom;
    function joinPeerRoom(){
      saveName();const id=($('joinInput').value||'').trim();if(!id)return toast('Nhập mã phòng trước.');disconnectPeer(false);S.host=false;S.peer=new Peer(undefined,{debug:1});
      S.peer.on('open',()=>{S.myPeerId=S.peer.id;const conn=S.peer.connect(id,{reliable:true});setupConn(conn);addLog('Đang kết nối tới phòng '+id+'...');render()});
      S.peer.on('error',e=>{addLog('Peer error: '+e.type+'. Kiểm tra mã phòng hoặc mạng.');render()});
    } window.joinPeerRoom=joinPeerRoom;
    function disconnectPeer(logIt=true){try{if(S.conn)S.conn.close();if(S.peer)S.peer.destroy()}catch(e){}S.peer=null;S.conn=null;S.connected=false;S.myPeerId='';S.host=false;S.battleStarted=false;S.enemyTeam=[];if(logIt)addLog('Đã ngắt kết nối.');render()} window.disconnectPeer=disconnectPeer;
    function sendTeam(){send({type:'team',name:S.playerName,team:S.myTeam});addLog('Đã gửi đội hình cho đối thủ.')} window.sendTeam=sendTeam;
    function startBattle(){if(!S.host||!S.connected)return;resetBattle();S.battleStarted=true;S.myTurn=true;send({type:'start',team:S.myTeam});addLog('Trận đấu bắt đầu. Bạn đi trước.');openTab('battle')} window.startBattle=startBattle;
    function onData(d){
      if(!d||!d.type)return;
      if(d.type==='hello'){S.enemyTeam=clone(d.team||[]);addLog((d.name||'Đối thủ')+' đã kết nối.');send({type:'team',name:S.playerName,team:S.myTeam});render()}
      if(d.type==='team'){S.enemyTeam=clone(d.team||[]);addLog('Đã nhận đội hình của '+(d.name||'đối thủ')+'.');render()}
      if(d.type==='start'){resetBattle();S.enemyTeam=clone(d.team||S.enemyTeam);S.battleStarted=true;S.myTurn=false;addLog('Chủ phòng đã bắt đầu trận. Đối thủ đi trước.');openTab('battle')}
      if(d.type==='state'){S.enemyTeam=clone(d.myTeam);S.myTeam=clone(d.enemyTeam);S.myTurn=d.yourTurn;S.battleStarted=d.battleStarted;S.winner=d.winner||null;if(d.log)addLog(d.log);render()}
      if(d.type==='syncRequest'){sendSync()}
    }
    function current(){return {me:S.myTeam[S.myActive],foe:S.enemyTeam[S.enemyActive]}}
    function damage(att,def,mv){const crit=Math.random()<.12?1.65:1;const raw=mv.power+att.atk*.42-def.def*.18;const dmg=Math.max(4,Math.round(raw*crit*(.9+Math.random()*.22)));def.hp=Math.max(0,def.hp-dmg);att.energy=Math.min(att.maxEnergy,att.energy+10);return {dmg,crit:crit>1}}
    function nextAlive(team){return team.findIndex(x=>x.hp>0)}
    function useMove(i){const {me,foe}=current();if(!S.myTurn||!me||!foe)return;const mv=me.moves[i];if(me.energy<mv.cost)return;me.energy-=mv.cost;const r=damage(me,foe,mv);animate(mv.type);let text=me.name+' dùng '+mv.name+', gây '+r.dmg+' sát thương'+(r.crit?' chí mạng!':'!');let next=nextAlive(S.enemyTeam);if(foe.hp<=0){text+=' '+foe.name+' đã gục!';if(next>=0)S.enemyActive=next;else{S.winner=S.playerName;S.myTurn=false;sendState(text);addLog(text);return}}S.myTurn=false;sendState(text);addLog(text)} window.useMove=useMove;
    function chargeEnergy(){const {me}=current();if(!S.myTurn||!me)return;me.energy=Math.min(me.maxEnergy,me.energy+35);const text=me.name+' tích thêm năng lượng.';S.myTurn=false;sendState(text);addLog(text)} window.chargeEnergy=chargeEnergy;
    function sendState(text='Đồng bộ trạng thái trận đấu.'){send({type:'state',myTeam:S.myTeam,enemyTeam:S.enemyTeam,yourTurn:true,battleStarted:S.battleStarted,winner:S.winner,log:text});render()} window.sendSync=()=>{send({type:'state',myTeam:S.myTeam,enemyTeam:S.enemyTeam,yourTurn:S.myTurn,battleStarted:S.battleStarted,winner:S.winner,log:'Đã đồng bộ lại trận đấu.'});addLog('Đã gửi đồng bộ lại.')};
    function toggleTeam(index){const mon=clone(starters[index]);const exists=S.myTeam.some(x=>x.id===mon.id);if(exists)S.myTeam=S.myTeam.filter(x=>x.id!==mon.id);else{if(S.myTeam.length>=3)return toast('Đội tối đa 3 Pokémon.');S.myTeam.push(mon)}if(!S.myTeam.length)S.myTeam.push(clone(starters[0]));localStorage.setItem('peerTeam',JSON.stringify(S.myTeam));renderTeam()} window.toggleTeam=toggleTeam;
    function chooseActive(i){if(S.myTeam[i]?.hp>0){S.myActive=i;renderBattle()}} window.chooseActive=chooseActive;
    function animate(type){const fx=$('fx');if(!fx)return;fx.innerHTML='';const colors={fire:'#fb923c',water:'#38bdf8',grass:'#22c55e',electric:'#fde047',psychic:'#c084fc',normal:'#e2e8f0',poison:'#a855f7',flying:'#93c5fd',dragon:'#818cf8'};for(let i=0;i<12;i++){let p=document.createElement('div');p.className='particle';let s=rand(14,34);p.style.width=s+'px';p.style.height=s+'px';p.style.left=rand(130,230)+'px';p.style.top=rand(150,240)+'px';p.style.background='radial-gradient(circle,#fff,'+(colors[type]||'#fff')+')';p.style.setProperty('--dx',rand(260,430)+'px');p.style.setProperty('--dy',rand(-120,40)+'px');p.style.animationDelay=(i*.025)+'s';fx.appendChild(p)}setTimeout(()=>fx.innerHTML='',800)}
    render();
  </script>
</body>
</html>
