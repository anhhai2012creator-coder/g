<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Pokemon Odyssey Peer Battle | No Firebase</title>
  <meta name="description" content="Pokemon Odyssey Peer Battle - game Pokemon online 1v1 dùng PeerJS, không cần Firebase, chạy trên GitHub Pages." />
  <meta name="theme-color" content="#2563eb" />
  <style>
    *{box-sizing:border-box}html{scroll-behavior:smooth}body{margin:0;font-family:system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;min-height:100vh;color:#f8fafc;background:radial-gradient(circle at 15% 10%,#ffffff30,transparent 20%),radial-gradient(circle at 85% 0,#facc1530,transparent 18%),linear-gradient(135deg,#020617,#1d4ed8 48%,#16a34a);overflow-x:hidden}.app{max-width:1320px;margin:0 auto;padding:18px}.hero{display:grid;grid-template-columns:1.2fr .8fr;gap:14px}.card{background:#ffffff18;border:1px solid #ffffff2d;border-radius:26px;padding:16px;box-shadow:0 20px 55px #0005;backdrop-filter:blur(18px)}h1{font-size:clamp(34px,5vw,64px);line-height:.95;margin:0 0 10px;letter-spacing:-2px}h2,h3{margin:0 0 12px}.muted{color:#dbeafe}.tabs,.row{display:flex;flex-wrap:wrap;gap:10px;align-items:center}.tabs{margin:14px 0}.tab{border:1px solid #ffffff2d;background:#ffffff18;color:white;padding:11px 14px;border-radius:16px;font-weight:900;cursor:pointer;transition:.15s}.tab:hover,.tab.active{background:#ffffff33;transform:translateY(-1px)}button,input{font:inherit}button{border:none;border-radius:15px;padding:10px 13px;font-weight:900;cursor:pointer;transition:.15s;background:linear-gradient(135deg,#fef08a,#facc15);color:#111827;box-shadow:0 10px 22px #0003}button:hover{transform:translateY(-1px)}button:disabled{opacity:.45;cursor:not-allowed;transform:none}.btn-blue{background:linear-gradient(135deg,#dbeafe,#60a5fa);color:#082f49}.btn-green{background:linear-gradient(135deg,#bbf7d0,#4ade80);color:#052e16}.btn-red{background:linear-gradient(135deg,#fecdd3,#fb7185);color:#3b0712}.btn-purple{background:linear-gradient(135deg,#ede9fe,#a78bfa);color:#2e1065}.ghost{background:#ffffff18;color:white;border:1px solid #ffffff2d;box-shadow:none}input{border:1px solid #ffffff2d;background:#00000025;color:white;border-radius:14px;padding:11px 12px;outline:none;min-width:210px}input::placeholder{color:#cbd5e1}.pane{display:none}.pane.active{display:block}.grid2{display:grid;grid-template-columns:1fr 1fr;gap:14px}.grid3{display:grid;grid-template-columns:repeat(3,1fr);gap:14px}.stat{background:#00000030;border:1px solid #ffffff24;border-radius:999px;padding:9px 12px;font-weight:900}.dot{display:inline-block;width:10px;height:10px;border-radius:50%;background:#ef4444;margin-right:6px}.dot.ok{background:#22c55e}.mini{background:#00000022;border:1px solid #ffffff24;border-radius:18px;padding:12px}.list{display:grid;gap:10px}.pokemon-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(160px,1fr));gap:10px}.mon{background:#ffffff14;border:1px solid #ffffff24;border-radius:20px;padding:12px;text-align:center;cursor:pointer;transition:.15s}.mon:hover,.mon.active{background:#ffffff30;transform:translateY(-1px)}.mon img{width:92px;height:92px;object-fit:contain;filter:drop-shadow(0 12px 12px #0005)}.type{display:inline-block;background:#0000003a;border-radius:999px;padding:3px 8px;font-size:12px;font-weight:900;margin:2px}.battle-scene{position:relative;min-height:360px;border-radius:24px;overflow:hidden;border:1px solid #ffffff2d;background:linear-gradient(180deg,#93c5fd,#22c55e 60%,#14532d)}.battle-scene::before{content:"";position:absolute;inset:0;background:radial-gradient(circle at 78% 16%,#ffffffcc 0 6%,transparent 7%),linear-gradient(transparent 62%,#00000025 63%)}.poke{position:absolute;z-index:3;width:170px;height:170px;object-fit:contain;filter:drop-shadow(0 18px 18px #0007)}.poke.me{left:50px;bottom:48px;transform:scaleX(-1)}.poke.foe{right:50px;bottom:108px}.shadow{position:absolute;width:210px;height:58px;border-radius:50%;background:radial-gradient(ellipse,#ffffff55,#00000025);bottom:34px}.shadow.left{left:38px}.shadow.right{right:38px;bottom:94px}.bar{height:13px;background:#00000045;border-radius:999px;overflow:hidden;margin:7px 0}.bar span{display:block;height:100%;border-radius:999px;transition:width:.3s}.hp{background:linear-gradient(90deg,#22c55e,#facc15,#ef4444)}.en{background:linear-gradient(90deg,#38bdf8,#a78bfa)}.moves{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-top:12px}.move{text-align:left;background:#ffffffe8;color:#0f172a}.log{height:230px;overflow:auto;background:#00000030;border:1px solid #ffffff24;border-radius:18px;padding:12px;line-height:1.45;font-size:14px}.fx{position:absolute;inset:0;pointer-events:none;z-index:5;overflow:hidden}.particle{position:absolute;border-radius:50%;animation:fly .7s ease-out forwards}@keyframes fly{0%{opacity:1;transform:translate(0,0) scale(.5)}100%{opacity:0;transform:translate(var(--dx),var(--dy)) scale(1.35) rotate(360deg)}}.footer{text-align:center;margin-top:16px;color:#dbeafe;background:#00000030;border:1px solid #ffffff24;border-radius:22px;padding:14px}.code{font-family:ui-monospace,SFMono-Regular,Menlo,monospace;background:#00000040;border:1px solid #ffffff24;border-radius:14px;padding:12px;overflow:auto;white-space:pre-wrap;color:#e0f2fe}.copy{user-select:all}.warn{background:#7f1d1d88;border:1px solid #fecdd3aa;border-radius:18px;padding:12px}.good{background:#064e3b88;border:1px solid #bbf7d0aa;border-radius:18px;padding:12px}@media(max-width:980px){.hero,.grid2,.grid3{grid-template-columns:1fr}.moves{grid-template-columns:1fr}.poke{width:125px;height:125px}.poke.me{left:15px}.poke.foe{right:15px}}
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
