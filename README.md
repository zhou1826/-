
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
  <title>🎵 歌手小百科 · 智能助手+游戏</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@400;500;600;700&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { font-family: 'Quicksand', sans-serif; background: linear-gradient(145deg, #fff9f0 0%, #ffe6f0 100%); color: #5e4b3c; padding: 1.5rem; min-height: 100vh; }
    .container { max-width: 1400px; margin: 0 auto; }
    .header { background: rgba(255,255,255,0.75); backdrop-filter: blur(8px); border-radius: 80px; padding: 0.6rem 1.8rem; display: flex; flex-wrap: wrap; justify-content: space-between; align-items: center; margin-bottom: 1.5rem; border: 2px solid #ffe0b5; }
    .logo h1 { font-size: 1.5rem; font-weight: 700; color: #ff8c94; }
    .lang-switch { display: flex; gap: 12px; }
    .lang-btn { background: #fff5e8; border: none; padding: 6px 18px; border-radius: 60px; font-weight: 600; cursor: pointer; font-size: 0.8rem; color: #cc8b65; transition: all 0.2s; }
    .lang-btn.active { background: #ffb7b2; color: white; }
    .search-wrapper { position: relative; margin: 1rem 0 1.2rem; }
    .search-area { background: white; border-radius: 100px; display: flex; align-items: center; padding: 0.3rem 0.3rem 0.3rem 1.8rem; border: 2px solid #ffe0c4; }
    .search-area i { color: #ffaa99; font-size: 1.2rem; margin-right: 8px; }
    .search-area input { flex: 1; border: none; padding: 0.9rem 1rem; font-size: 1rem; background: transparent; outline: none; font-family: 'Quicksand', sans-serif; }
    .search-area button { background: #ffb7b2; border: none; color: white; padding: 0.6rem 1.8rem; border-radius: 60px; font-weight: 700; cursor: pointer; transition: 0.2s; }
    .search-area button:hover { background: #ff9a8b; }
    .suggestions-box { position: absolute; top: 100%; left: 0; right: 0; background: white; border-radius: 28px; margin-top: 8px; box-shadow: 0 15px 30px rgba(0,0,0,0.1); border: 2px solid #ffe0c4; z-index: 100; max-height: 280px; overflow-y: auto; display: none; }
    .suggestions-box.show { display: block; }
    .suggestion-item, .history-item { padding: 10px 20px; cursor: pointer; display: flex; align-items: center; gap: 10px; border-bottom: 1px solid #fff0e6; }
    .suggestion-item:hover, .history-item:hover { background: #fff5e8; }
    .history-header { padding: 8px 20px; font-size: 0.7rem; color: #cc8b65; font-weight: 600; border-bottom: 1px solid #ffe0c4; display: flex; justify-content: space-between; }
    .clear-history { cursor: pointer; color: #ff8c94; }

    .filter-section { margin-bottom: 1.2rem; }
    .filter-row { display: flex; flex-wrap: wrap; align-items: center; gap: 12px; background: rgba(255,250,240,0.6); padding: 8px 16px; border-radius: 60px; margin-bottom: 8px; }
    .filter-label { font-weight: 700; color: #b35e3e; font-size: 0.8rem; }
    .filter-chips { display: flex; flex-wrap: wrap; gap: 8px; }
    .chip { background: white; border: 1px solid #ffe0c4; padding: 4px 14px; border-radius: 40px; font-size: 0.75rem; font-weight: 500; cursor: pointer; color: #5e4b3c; transition: all 0.15s; }
    .chip.active { background: #ffb7b2; color: white; border-color: #ffb7b2; }
    .tag-cloud { display: flex; flex-wrap: wrap; gap: 8px; margin: 10px 0 5px; }
    .cloud-tag { background: #fff2e9; padding: 4px 12px; border-radius: 30px; font-size: 0.75rem; color: #b35e3e; cursor: pointer; border: 1px solid #ffe0d0; }
    .cloud-tag.active { background: #ffb7b2; color: white; }
    .sort-row { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; }
    .sort-btn { background: transparent; border: 1px solid #ffd9c6; padding: 4px 14px; border-radius: 40px; font-size: 0.75rem; font-weight: 600; cursor: pointer; color: #8b5e4b; transition: 0.15s; }
    .sort-btn.active { background: #ffd9c6; color: #5e2e1c; }

    /* 游戏卡片 */
    .game-card { background: rgba(255,255,255,0.7); backdrop-filter: blur(4px); border-radius: 28px; padding: 16px 20px; margin: 16px 0 8px; border: 2px dashed #ffb7b2; display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; }
    .game-title { font-weight: 700; color: #c06a4a; }
    .game-btn { background: #ffd9c6; border: none; padding: 8px 18px; border-radius: 40px; font-weight: 600; cursor: pointer; color: #5e4b3c; margin-left: 10px; }
    .random-btn { background: #ffe0b5; margin-left: 8px; }

    .result-info { display: flex; justify-content: space-between; margin-bottom: 1.5rem; background: rgba(255,250,240,0.8); padding: 8px 18px; border-radius: 60px; }
    .reset-btn { background: #ffefdb; border: none; padding: 6px 18px; border-radius: 40px; cursor: pointer; font-weight: 600; color: #5e4b3c; }
    .singers-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(310px, 1fr)); gap: 1.8rem; }
    .singer-card { background: #ffffff; backdrop-filter: blur(4px); border-radius: 2rem; overflow: hidden; cursor: pointer; border: 2px solid #ffe2ce; transition: 0.2s; }
    .singer-card:hover { transform: translateY(-5px); box-shadow: 0 20px 30px rgba(0,0,0,0.1); }
    .card-inner { padding: 1.4rem; }
    .card-top { display: flex; align-items: center; gap: 14px; margin-bottom: 1rem; border-bottom: 2px dotted #ffe0d0; padding-bottom: 0.7rem; }
    .avatar { width: 56px; height: 56px; background: #ffe3d6; border-radius: 40px; display: flex; align-items: center; justify-content: center; font-size: 2rem; color: #ff9a8b; }
    .singer-name { font-size: 1.4rem; font-weight: 700; color: #c06a4a; }
    .debut-badge { background: #ffefdb; padding: 4px 12px; border-radius: 40px; font-size: 0.7rem; display: inline-block; margin-top: 6px; }
    .reps { display: flex; flex-wrap: wrap; gap: 8px; margin: 12px 0; }
    .rep-tag { background: #fff2e6; color: #d48c6b; font-size: 0.7rem; padding: 4px 12px; border-radius: 30px; }
    .card-footer { margin-top: 12px; font-size: 0.7rem; text-align: right; color: #ffaa99; }

    .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(255,210,190,0.7); backdrop-filter: blur(5px); align-items: center; justify-content: center; z-index: 1000; }
    .modal-content { background: #fffff5; max-width: 580px; width: 90%; border-radius: 2rem; padding: 1.8rem; position: relative; max-height: 85vh; overflow-y: auto; border: 3px solid #ffd9c6; }
    .close-modal { position: absolute; top: 1rem; right: 1.2rem; font-size: 1.8rem; cursor: pointer; color: #c06a4a; }
    .modal h2 { font-size: 1.8rem; color: #c27757; margin-bottom: 0.8rem; }
    .modal-detail p { margin: 12px 0; line-height: 1.5; font-size: 0.9rem; }
    .modal-detail .label { font-weight: 800; background: #fff0e6; padding: 4px 12px; border-radius: 40px; display: inline-block; margin-right: 8px; }

    /* AI 助手 */
    .ai-assistant { position: fixed; bottom: 20px; right: 20px; z-index: 1001; font-family: 'Quicksand', sans-serif; }
    .ai-toggle { width: 60px; height: 60px; border-radius: 30px; background: #ffb7b2; border: none; color: white; font-size: 28px; cursor: pointer; box-shadow: 0 8px 20px rgba(255,140,148,0.3); transition: 0.2s; display: flex; align-items: center; justify-content: center; }
    .ai-toggle:hover { background: #ff9a8b; transform: scale(1.05); }
    .ai-chat-panel { position: absolute; bottom: 80px; right: 0; width: 320px; background: white; border-radius: 28px; box-shadow: 0 20px 40px rgba(0,0,0,0.15); border: 2px solid #ffe0c4; overflow: hidden; display: none; flex-direction: column; }
    .ai-chat-panel.open { display: flex; }
    .ai-header { background: #ffb7b2; color: white; padding: 16px 20px; font-weight: 700; display: flex; justify-content: space-between; align-items: center; }
    .ai-header i { cursor: pointer; }
    .ai-messages { height: 300px; overflow-y: auto; padding: 16px; background: #fffaf5; display: flex; flex-direction: column; gap: 12px; }
    .ai-message { display: flex; gap: 8px; max-width: 85%; }
    .ai-message.user { align-self: flex-end; flex-direction: row-reverse; }
    .ai-message .bubble { background: #ffe3d6; padding: 10px 14px; border-radius: 18px; font-size: 0.85rem; color: #5e4b3c; }
    .ai-message.user .bubble { background: #ffb7b2; color: white; }
    .ai-avatar { width: 32px; height: 32px; background: #ffd9c6; border-radius: 20px; display: flex; align-items: center; justify-content: center; color: #c06a4a; }
    .ai-input-area { display: flex; padding: 12px 16px; border-top: 1px solid #ffe0c4; background: white; }
    .ai-input-area input { flex: 1; border: 1px solid #ffe0c4; border-radius: 40px; padding: 10px 16px; font-size: 0.9rem; outline: none; font-family: 'Quicksand', sans-serif; }
    .ai-input-area button { background: #ffb7b2; border: none; color: white; width: 44px; border-radius: 30px; margin-left: 8px; cursor: pointer; }

    @media (max-width: 700px) { body { padding: 1rem; } .header { flex-direction: column; align-items: stretch; border-radius: 40px; gap: 10px; } }
  </style>
</head>
<body>
<div class="container">
  <div class="header">
    <div class="logo"><h1 id="pageTitle">🎤 歌手小百科</h1></div>
    <div class="lang-switch">
      <button class="lang-btn active" data-lang="zh">中文</button>
      <button class="lang-btn" data-lang="ja">日本語</button>
      <button class="lang-btn" data-lang="en">English</button>
    </div>
  </div>

  <div class="search-wrapper">
    <div class="search-area">
      <i class="fas fa-music"></i>
      <input type="text" id="searchInput" placeholder="搜歌手 / 英文名 / 风格 / 代表作" autocomplete="off">
      <button id="searchBtn"><span id="searchBtnText">搜索</span></button>
      <button class="random-btn" id="randomSingerBtn" title="随机发现一位歌手">🎲</button>
    </div>
    <div id="suggestionsBox" class="suggestions-box"></div>
  </div>

  <!-- 游戏栏 -->
  <div class="game-card" id="gameArea">
    <div><span class="game-title">🎮 猜代表作</span> <span id="gameQuestion">加载中...</span></div>
    <div>
      <input type="text" id="gameAnswerInput" placeholder="输入歌手名" style="padding:6px 12px; border-radius:40px; border:1px solid #ffd9c6; outline:none;">
      <button class="game-btn" id="gameSubmitBtn">提交</button>
      <button class="game-btn" id="gameNextBtn">下一题</button>
    </div>
  </div>

  <!-- 筛选区 -->
  <div class="filter-section">
    <div class="filter-row">
      <span class="filter-label" id="filterEraLabel">📅 年代</span>
      <div class="filter-chips" id="eraFilters"></div>
    </div>
    <div class="filter-row">
      <span class="filter-label" id="filterRegionLabel">🌍 地区</span>
      <div class="filter-chips" id="regionFilters"></div>
    </div>
    <div class="tag-cloud" id="genreTagCloud"></div>
    <div class="sort-row">
      <span class="filter-label" id="sortLabel">🔽 排序</span>
      <button class="sort-btn" data-sort="yearAsc" id="sortYearAsc">出道年份 ↑</button>
      <button class="sort-btn" data-sort="yearDesc" id="sortYearDesc">出道年份 ↓</button>
      <button class="sort-btn" data-sort="nameAsc" id="sortNameAsc">A → Z</button>
      <button class="sort-btn" data-sort="nameDesc" id="sortNameDesc">Z → A</button>
      <button class="sort-btn active" data-sort="hot" id="sortHot">🔥 热度</button>
    </div>
  </div>

  <div class="result-info">
    <span id="resultCount">加载中...</span>
    <button class="reset-btn" id="resetBtn">🔄 重置</button>
  </div>

  <div id="singersGrid" class="singers-grid"></div>
</div>

<!-- 模态框 -->
<div id="singerModal" class="modal">
  <div class="modal-content">
    <span class="close-modal">&times;</span>
    <div id="modalBody"></div>
  </div>
</div>

<!-- AI 助手 -->
<div class="ai-assistant">
  <button class="ai-toggle" id="aiToggle">💬</button>
  <div class="ai-chat-panel" id="aiChatPanel">
    <div class="ai-header"><span>🤖 小音 AI</span><i class="fas fa-times" id="aiClose"></i></div>
    <div class="ai-messages" id="aiMessages">
      <div class="ai-message"><div class="ai-avatar"><i class="fas fa-robot"></i></div><div class="bubble">你好！我是小音，可以问我关于歌手的问题哦～</div></div>
    </div>
    <div class="ai-input-area">
      <input type="text" id="aiInput" placeholder="问点什么吧..." />
      <button id="aiSend"><i class="fas fa-paper-plane"></i></button>
    </div>
  </div>
</div>

<script>
(function(){
  "use strict";

  // ---------- 歌手数据库 (含陈洁丽、李佳薇、廖俊涛) ----------
  const singersDB = [
    { name: "林子祥", enName: "George Lam", debutYear: "1976", debutDetail: "1976年发行首张专辑《George Lam》", genre: ["粤语流行", "摇滚"], reps: ["男儿当自强", "数字人生", "分分钟需要你"], bio: "香港乐坛殿堂级歌手，以高音和硬汉形象著称。", bio_en: "Hong Kong music legend, known for high-pitched voice and tough guy image.", bio_ja: "香港の伝説的歌手。高音とハードなイメージで知られる。", region: "香港", gender: "男", hot: 88 },
    { name: "胡歌", enName: "Hu Ge", debutYear: "2015", debutDetail: "2015年演唱《风起时》跨界乐坛", genre: ["流行", "影视"], reps: ["风起时", "一念之间", "逍遥叹"], bio: "著名演员，同时演唱多部影视主题曲，嗓音深情。", bio_en: "Famous actor, also sings many TV drama theme songs with emotional voice.", bio_ja: "有名俳優。多くのドラマ主題歌を担当。", region: "内地", gender: "男", hot: 75 },
    { name: "林志炫", enName: "Terry Lin", debutYear: "1991", debutDetail: "1991年以组合优客李林出道", genre: ["流行", "美声"], reps: ["单身情歌", "蒙娜丽莎的眼泪", "离人"], bio: "拥有清亮高亢的嗓音，被誉为歌坛绅士。", bio_en: "Known for clear and high-pitched voice, called 'Gentleman of Music'.", bio_ja: "澄んだ高声を持つ「音楽界の紳士」。", region: "台湾", gender: "男", hot: 82 },
    { name: "林忆莲", enName: "Sandy Lam", debutYear: "1985", debutDetail: "1985年发行首张专辑《林忆莲》", genre: ["流行", "抒情", "R&B"], reps: ["至少还有你", "伤痕", "为你我受冷风吹"], bio: "华语乐坛天后级歌手，情感细腻，唱功卓越。", bio_en: "Diva of Mandopop, delicate emotions and superb singing skills.", bio_ja: "マンダポップの歌姫。繊細な感情表現と卓越した歌唱力。", region: "香港", gender: "女", hot: 95 },
    { name: "林志颖", enName: "Jimmy Lin", debutYear: "1992", debutDetail: "1992年发行首张专辑《不是每个恋曲都有美好回忆》", genre: ["流行", "青春"], reps: ["十七岁的雨季", "芹菜", "稻草人"], bio: "亚洲小旋风，歌手、演员、赛车手。", bio_en: "Asian Little Tornado, singer, actor, race car driver.", bio_ja: "「アジアの小さな旋風」。歌手、俳優、レーサー。", region: "台湾", gender: "男", hot: 84 },
    { name: "BY2", enName: "BY2", debutYear: "2008", debutDetail: "2008年发行首张专辑《16未成年》", genre: ["流行", "舞曲"], reps: ["爱丫爱丫", "我知道", "有点甜"], bio: "新加坡双胞胎女子组合，青春舞曲代表。", bio_en: "Singaporean twin sister duo, youthful dance pop.", bio_ja: "シンガポールの双子姉妹デュオ。", region: "海外", gender: "女", hot: 78 },
    { name: "张学友", enName: "Jacky Cheung", debutYear: "1985", debutDetail: "1985年发行首张专辑《Smile》", genre: ["流行", "粤语"], reps: ["吻别", "一千个伤心的理由", "遥远的她"], bio: "华语歌神，四大天王之一。", bio_en: "God of Songs, one of the Four Heavenly Kings.", bio_ja: "中国ポップスの歌神。", region: "香港", gender: "男", hot: 99 },
    { name: "刘德华", enName: "Andy Lau", debutYear: "1985", debutDetail: "1985年发行首张专辑《只知道此刻爱你》", genre: ["流行", "粤语"], reps: ["忘情水", "一起走过的日子", "中国人"], bio: "四大天王之一，影视歌三栖巨星。", bio_en: "One of the Four Heavenly Kings, superstar in film and music.", bio_ja: "四大天王の一人。", region: "香港", gender: "男", hot: 98 },
    { name: "郭富城", enName: "Aaron Kwok", debutYear: "1990", debutDetail: "1990年发行首张专辑《对你爱不完》", genre: ["流行", "舞曲"], reps: ["对你爱不完", "狂野之城", "Para Para Sakura"], bio: "四大天王之一，动感舞曲代表。", bio_en: "One of the Four Heavenly Kings, known for dance music.", bio_ja: "四大天王の一人。ダンスミュージックで知られる。", region: "香港", gender: "男", hot: 92 },
    { name: "张信哲", enName: "Jeff Chang", debutYear: "1989", debutDetail: "1989年发行首张专辑《说谎》", genre: ["流行", "情歌"], reps: ["爱如潮水", "过火", "白月光"], bio: "情歌王子，嗓音清澈温柔。", bio_en: "Prince of love songs, clear and tender voice.", bio_ja: "ラブソングの王子様。", region: "台湾", gender: "男", hot: 89 },
    { name: "邓丽君", enName: "Teresa Teng", debutYear: "1967", debutDetail: "1967年发行首张专辑《邓丽君之歌》", genre: ["流行", "抒情"], reps: ["甜蜜蜜", "月亮代表我的心", "我只在乎你"], bio: "永恒的歌后，20世纪最富盛名的华语女歌手。", bio_en: "Eternal diva, most famous Chinese female singer of 20th century.", bio_ja: "永遠の歌姫。", region: "台湾", gender: "女", hot: 100 },
    { name: "许嵩", enName: "Xu Song", debutYear: "2009", debutDetail: "2009年发行《自定义》", genre: ["中国风", "R&B"], reps: ["有何不可", "灰色头像", "雅俗共赏"], bio: "QQ音乐三巨头之一，音乐诗人。", bio_en: "One of the Big Three of QQ Music, music poet.", bio_ja: "QQ音楽ビッグ3の一人。", region: "内地", gender: "男", hot: 91 },
    { name: "汪苏泷", enName: "Silence Wang", debutYear: "2010", debutDetail: "2010年发行《慢慢懂》", genre: ["流行", "R&B"], reps: ["有点甜", "不分手的恋爱", "万有引力"], bio: "全能制作人，OST大户。", bio_en: "All-round producer, known for OST hits.", bio_ja: "万能プロデューサー。", region: "内地", gender: "男", hot: 87 },
    { name: "徐良", enName: "Xu Liang", debutYear: "2010", debutDetail: "2010年凭《犯贱》爆红", genre: ["流行"], reps: ["犯贱", "客官不可以", "七秒钟的记忆"], bio: "QQ音乐三巨头之一，网络音乐代表。", bio_en: "One of the Big Three, online music representative.", bio_ja: "QQ音楽ビッグ3の一人。", region: "内地", gender: "男", hot: 80 },
    { name: "周杰伦", enName: "Jay Chou", debutYear: "2000", debutDetail: "2000年《Jay》出道", genre: ["R&B", "中国风", "嘻哈"], reps: ["七里香", "青花瓷", "双截棍"], bio: "华语流行天王，金曲奖纪录保持者。", bio_en: "King of Mandopop, Golden Melody record holder.", bio_ja: "マンダポップの王様。", region: "台湾", gender: "男", hot: 100 },
    { name: "林俊杰", enName: "JJ Lin", debutYear: "2003", debutDetail: "2003年《乐行者》", genre: ["流行", "R&B"], reps: ["江南", "修炼爱情", "不为谁而作的歌"], bio: "行走的CD，金曲歌王。", bio_en: "Walking CD, Golden Melody Best Male Singer.", bio_ja: "歩くCD。", region: "海外", gender: "男", hot: 97 },
    { name: "陈奕迅", enName: "Eason Chan", debutYear: "1995", debutDetail: "1995新秀冠军", genre: ["粤语流行", "抒情"], reps: ["十年", "富士山下", "浮夸"], bio: "香港乐坛殿堂级歌手，情感表达极致。", bio_en: "Hong Kong music legend, master of emotion.", bio_ja: "香港の殿堂級歌手。", region: "香港", gender: "男", hot: 98 },
    { name: "薛之谦", enName: "Joker Xue", debutYear: "2005", debutDetail: "2005我型我秀出道", genre: ["抒情流行"], reps: ["演员", "丑八怪", "认真的雪"], bio: "深情伤感情歌王子。", bio_en: "Prince of sad love songs.", bio_ja: "切ないラブソングの王子。", region: "内地", gender: "男", hot: 93 },
    { name: "邓紫棋", enName: "G.E.M.", debutYear: "2008", debutDetail: "2008年《G.E.M.》", genre: ["流行", "摇滚"], reps: ["光年之外", "泡沫", "句号"], bio: "创作型铁肺天后。", bio_en: "Singer-songwriter with powerful vocals.", bio_ja: "創作系鉄肺歌姫。", region: "香港", gender: "女", hot: 96 },
    { name: "周深", enName: "Zhou Shen", debutYear: "2014", debutDetail: "2014好声音出道", genre: ["流行", "国风", "美声"], reps: ["大鱼", "光亮", "化身孤岛的鲸"], bio: "天籁之音，海妖之嗓。", bio_en: "Heavenly voice, known as the 'Siren'.", bio_ja: "天に昇る歌声。", region: "内地", gender: "男", hot: 94 },
    { name: "李荣浩", enName: "Li Ronghao", debutYear: "2013", debutDetail: "2013《模特》", genre: ["蓝调", "流行"], reps: ["模特", "李白", "年少有为"], bio: "全能音乐人，一人包办所有乐器。", bio_en: "All-round musician, plays all instruments himself.", bio_ja: "万能音楽家。", region: "内地", gender: "男", hot: 90 },
    { name: "张杰", enName: "Jason Zhang", debutYear: "2004", debutDetail: "2004我型我秀冠军", genre: ["流行", "摇滚"], reps: ["逆战", "天下", "最美的太阳"], bio: "华语LIVE王，高音亮。", bio_en: "Live king of Mandopop, known for high notes.", bio_ja: "ライブの王者。", region: "内地", gender: "男", hot: 92 },
    { name: "王力宏", enName: "Leehom Wang", debutYear: "1995", debutDetail: "1995《情敌贝多芬》", genre: ["R&B", "中国风"], reps: ["唯一", "大城小爱", "花田错"], bio: "伯克利博士，开创Chinked-out曲风。", bio_en: "Doctor from Berklee, creator of Chinked-out style.", bio_ja: "バークリー音楽院博士。", region: "台湾", gender: "男", hot: 95 },
    { name: "蔡依林", enName: "Jolin Tsai", debutYear: "1999", debutDetail: "1999《1019》", genre: ["舞曲", "电子"], reps: ["日不落", "舞娘", "Play我呸"], bio: "亚洲舞后，金曲奖大满贯。", bio_en: "Queen of dance in Asia, Golden Melody Grand Slam.", bio_ja: "アジアのダンスクイーン。", region: "台湾", gender: "女", hot: 97 },
    { name: "孙燕姿", enName: "Stefanie Sun", debutYear: "2000", debutDetail: "2000同名专辑", genre: ["抒情", "流行"], reps: ["天黑黑", "遇见", "逆光"], bio: "独特嗓音，华语小天后。", bio_en: "Unique voice, little diva of Mandopop.", bio_ja: "唯一無二の声。", region: "海外", gender: "女", hot: 96 },
    { name: "张靓颖", enName: "Jane Zhang", debutYear: "2005", debutDetail: "2005超女", genre: ["流行", "灵魂"], reps: ["画心", "终于等到你", "如果这就是爱情"], bio: "海豚音公主，OST女王。", bio_en: "Princess of dolphin whistle, queen of OST.", bio_ja: "ドルフィンホイッスルの女王。", region: "内地", gender: "女", hot: 91 },
    { name: "林宥嘉", enName: "Yoga Lin", debutYear: "2007", debutDetail: "2007星光大道冠军", genre: ["迷幻摇滚", "抒情"], reps: ["说谎", "残酷月光", "天真有邪"], bio: "迷幻唱腔，音乐美学独特。", bio_en: "Psychedelic voice, unique musical aesthetics.", bio_ja: "サイケデリックな歌声。", region: "台湾", gender: "男", hot: 88 },
    { name: "陶喆", enName: "David Tao", debutYear: "1997", debutDetail: "1997《David Tao》", genre: ["R&B", "灵魂"], reps: ["爱很简单", "小镇姑娘", "黑色柳丁"], bio: "华语R&B教父。", bio_en: "Godfather of Chinese R&B.", bio_ja: "中国R&Bのゴッドファーザー。", region: "台湾", gender: "男", hot: 92 },
    { name: "方大同", enName: "Khalil Fong", debutYear: "2005", debutDetail: "2005《Soulboy》", genre: ["R&B", "灵魂", "爵士"], reps: ["爱爱爱", "特别的人", "三人游"], bio: "灵魂乐才子，节奏蓝调指标。", bio_en: "Soul music talent, icon of R&B.", bio_ja: "ソウルミュージックの才子。", region: "海外", gender: "男", hot: 89 },
    { name: "毛不易", enName: "Mao Buyi", debutYear: "2017", debutDetail: "2017明日之子冠军", genre: ["民谣", "抒情"], reps: ["消愁", "平凡的一天", "像我这样的人"], bio: "平凡巨星，歌词直击人心。", bio_en: "Ordinary superstar, lyrics that hit the heart.", bio_ja: "平凡なスーパースター。", region: "内地", gender: "男", hot: 90 },
    { name: "单依纯", enName: "Shan Yichun", debutYear: "2020", debutDetail: "2020好声音冠军", genre: ["R&B", "灵魂"], reps: ["永不失联的爱", "给电影人的情书"], bio: "新生代唱将，声音细腻。", bio_en: "New generation powerhouse, delicate voice.", bio_ja: "新生代の実力派。", region: "内地", gender: "女", hot: 85 },
    { name: "刘宇宁", enName: "Liu Yuning", debutYear: "2018", debutDetail: "摩登兄弟主唱", genre: ["流行", "摇滚"], reps: ["让酒", "天问", "寻一个你"], bio: "OST大户，嗓音沙哑磁性。", bio_en: "OST king, husky magnetic voice.", bio_ja: "OSTの王様。", region: "内地", gender: "男", hot: 88 },
    { name: "黄子弘凡", enName: "Huang Zihongfan", debutYear: "2018", debutDetail: "声入人心出道", genre: ["美声流行"], reps: ["青火", "歌行", "Waking"], bio: "新生代美声偶像，伯克利才子。", bio_en: "New generation bel canto idol, Berklee talent.", bio_ja: "新生代のベルカントアイドル。", region: "内地", gender: "男", hot: 80 },
    { name: "希林娜依·高", enName: "Curley G", debutYear: "2017", debutDetail: "2017好声音", genre: ["流行", "摇滚"], reps: ["颗粒季", "阿莫希林", "Mirror"], bio: "烟嗓极具辨识度，前硬糖少女303队长。", bio_en: "Recognizable smoky voice, former leader of BonBon Girls 303.", bio_ja: "特徴的なハスキーボイス。", region: "内地", gender: "女", hot: 86 },
    { name: "黄霄雲", enName: "Huang Xiaoyun", debutYear: "2015", debutDetail: "2015好声音", genre: ["流行", "高音"], reps: ["星辰大海", "左手指月"], bio: "技术流唱将，魔王级新人。", bio_en: "Technical powerhouse, demon-level newcomer.", bio_ja: "テクニック重視の実力派。", region: "内地", gender: "女", hot: 84 },
    { name: "刘柏辛", enName: "Lexie Liu", debutYear: "2018", debutDetail: "2018《2029》", genre: ["电子", "嘻哈"], reps: ["Manta", "佳人"], bio: "前卫音乐人，国际范创作型歌手。", bio_en: "Avant-garde musician, international style.", bio_ja: "アバンギャルドな音楽家。", region: "内地", gender: "女", hot: 83 },
    { name: "王源", enName: "Wang Yuan", debutYear: "2013", debutDetail: "TFBOYS成员", genre: ["流行", "民谣"], reps: ["骄傲", "世界上没有真正的感同身受"], bio: "原创音乐人，伯克利在读。", bio_en: "Singer-songwriter, studying at Berklee.", bio_ja: "シンガーソングライター。", region: "内地", gender: "男", hot: 88 },
    { name: "王俊凯", enName: "Wang Junkai", debutYear: "2013", debutDetail: "TFBOYS出道", genre: ["流行"], reps: ["生长", "Ain't Got No Love"], bio: "全能艺人，北京电影学院毕业。", bio_en: "All-round entertainer, graduated from Beijing Film Academy.", bio_ja: "万能エンターテイナー。", region: "内地", gender: "男", hot: 87 },
    { name: "易烊千玺", enName: "Jackson Yee", debutYear: "2013", debutDetail: "TFBOYS出道", genre: ["流行", "实验"], reps: ["My Boo", "粉雾海"], bio: "演员歌手双栖，音乐风格前卫。", bio_en: "Actor and singer, avant-garde music style.", bio_ja: "俳優兼歌手。", region: "内地", gender: "男", hot: 89 },
    { name: "张艺兴", enName: "Lay Zhang", debutYear: "2012", debutDetail: "EXO出道", genre: ["流行", "电子", "M-Pop"], reps: ["莲", "Sheep", "梦不落雨林"], bio: "唱跳制作人，M-Pop开创者。", bio_en: "Singer-dancer-producer, creator of M-Pop.", bio_ja: "歌って踊れるプロデューサー。", region: "内地", gender: "男", hot: 94 },
    { name: "五月天", enName: "Mayday", debutYear: "1999", debutDetail: "1999第一张专辑", genre: ["摇滚", "流行"], reps: ["倔强", "突然好想你", "恋爱ing"], bio: "华语摇滚天团，青春信仰。", bio_en: "Mandopop rock band, faith of youth.", bio_ja: "マンダポップロックバンド。", region: "台湾", gender: "组合", hot: 99 },
    { name: "苏打绿", enName: "Sodagreen", debutYear: "2005", debutDetail: "2005同名专辑", genre: ["独立", "古典摇滚"], reps: ["小情歌", "你在烦恼什么", "冬未了"], bio: "文艺乐团，韦瓦第计划。", bio_en: "Literary band, Vivaldi Project.", bio_ja: "文学的なバンド。", region: "台湾", gender: "组合", hot: 93 },
    { name: "告五人", enName: "Accusefive", debutYear: "2017", debutDetail: "2017成团", genre: ["独立", "流行摇滚"], reps: ["爱人错过", "带我去找夜生活", "披星戴月的想你"], bio: "新生代人气乐团，双主唱。", bio_en: "Popular new-generation band, dual lead vocals.", bio_ja: "人気の新世代バンド。", region: "台湾", gender: "组合", hot: 90 },
    { name: "草东没有派对", enName: "No Party For Cao Dong", debutYear: "2016", debutDetail: "2016《丑奴儿》", genre: ["独立摇滚", "另类"], reps: ["山海", "丑", "烂泥"], bio: "金曲奖最佳乐团，情绪摇滚代表。", bio_en: "Golden Melody Best Band, representative of emo rock.", bio_ja: "金曲賞最優秀バンド。", region: "台湾", gender: "组合", hot: 91 },
    { name: "凤凰传奇", enName: "Phoenix Legend", debutYear: "2004", debutDetail: "2004年成立", genre: ["民族流行", "电音"], reps: ["最炫民族风", "月亮之上", "山河图"], bio: "国民组合，广场舞神曲缔造者。", bio_en: "National duo, creators of square dance hits.", bio_ja: "国民的デュオ。", region: "内地", gender: "组合", hot: 95 },
    { name: "时代少年团", enName: "Teens in Times", debutYear: "2019", debutDetail: "2019成团", genre: ["流行", "舞曲"], reps: ["爆米花", "哪吒", "无尽的冒险"], bio: "Z世代顶流偶像团体。", bio_en: "Top idol group of Gen Z.", bio_ja: "Z世代のトップアイドルグループ。", region: "内地", gender: "组合", hot: 92 },
    { name: "筷子兄弟", enName: "Chopstick Brothers", debutYear: "2007", debutDetail: "2007组合成立", genre: ["流行", "网络"], reps: ["老男孩", "小苹果", "父亲"], bio: "现象级神曲《小苹果》创作者。", bio_en: "Creators of viral hit 'Little Apple'.", bio_ja: "バイラルヒット「小苹果」の生みの親。", region: "内地", gender: "组合", hot: 88 },
    { name: "小虎队", enName: "Little Tigers", debutYear: "1988", debutDetail: "1988组合成立", genre: ["流行", "青春"], reps: ["青苹果乐园", "爱", "红蜻蜓"], bio: "华语乐坛第一支偶像团体。", bio_en: "The first idol group in Chinese pop music.", bio_ja: "中国ポップス初のアイドルグループ。", region: "台湾", gender: "组合", hot: 94 },
    { name: "韩红", enName: "Han Hong", debutYear: "1995", debutDetail: "1995年出道", genre: ["流行", "民族"], reps: ["天路", "青藏高原", "天亮了"], bio: "国家一级演员，慈善家。", bio_en: "National First-Class Actress, philanthropist.", bio_ja: "国家一级演员。", region: "内地", gender: "女", hot: 93 },
    { name: "刘欢", enName: "Liu Huan", debutYear: "1986", debutDetail: "1986年出道", genre: ["流行", "影视音乐"], reps: ["好汉歌", "千万次的问", "弯弯的月亮"], bio: "中国流行音乐家，对外经贸大学教授。", bio_en: "Chinese pop musician, professor at UIBE.", bio_ja: "中国ポップス音楽家。", region: "内地", gender: "男", hot: 92 },
    { name: "孙楠", enName: "Sun Nan", debutYear: "1989", debutDetail: "1989年出道", genre: ["流行"], reps: ["你快回来", "不见不散", "红旗飘飘"], bio: "实力派唱将，高音嘹亮。", bio_en: "Powerhouse vocalist, known for high notes.", bio_ja: "実力派歌手。", region: "内地", gender: "男", hot: 90 },
    { name: "韩磊", enName: "Han Lei", debutYear: "1991", debutDetail: "1991年出道", genre: ["流行", "民族"], reps: ["向天再借五百年", "走四方", "等待"], bio: "影视歌曲之王，歌王称号。", bio_en: "King of TV drama songs, winner of 'I Am a Singer'.", bio_ja: "ドラマソングの王様。", region: "内地", gender: "男", hot: 89 },
    { name: "谭维维", enName: "Tan Weiwei", debutYear: "2006", debutDetail: "2006超女", genre: ["摇滚", "民族"], reps: ["如果有来生", "乌兰巴托的夜", "华阴老腔"], bio: "摇滚女皇，民族摇滚先锋。", bio_en: "Rock queen, pioneer of ethnic rock.", bio_ja: "ロックの女王。", region: "内地", gender: "女", hot: 88 },
    { name: "袁娅维", enName: "Tia Ray", debutYear: "2012", debutDetail: "2012好声音", genre: ["Soul", "R&B"], reps: ["说散就散", "阿楚姑娘", "Love Can Fly"], bio: "灵魂歌者，中国灵魂乐第一人。", bio_en: "Soul singer, pioneer of Chinese soul music.", bio_ja: "ソウルシンガー。", region: "内地", gender: "女", hot: 87 },
    { name: "刀郎", enName: "Dao Lang", debutYear: "2004", debutDetail: "2004年《2002年的第一场雪》", genre: ["民谣", "民族"], reps: ["2002年的第一场雪", "冲动的惩罚", "西海情歌"], bio: "西域歌王，沧桑嗓音。", bio_en: "King of Western Region, weathered voice.", bio_ja: "西域の歌王。", region: "内地", gender: "男", hot: 90 },
    { name: "郑润泽", enName: "Zheng Runze", debutYear: "2018", debutDetail: "2018《明日之子》", genre: ["流行", "抒情"], reps: ["于是", "如果呢", "小胡同"], bio: "Z世代情歌王子，播放量超10亿。", bio_en: "Gen Z love song prince, over 1 billion streams.", bio_ja: "Z世代のラブソング王子。", region: "内地", gender: "男", hot: 84 },
    { name: "颜人中", enName: "Yan Renzhong", debutYear: "2018", debutDetail: "2018翻唱走红", genre: ["流行", "R&B"], reps: ["晚安", "嗜好", "夏夜最后的烟火"], bio: "慵懒磁性嗓音，宝藏男孩。", bio_en: "Lazy magnetic voice, treasure boy.", bio_ja: "怠惰で磁性のある声。", region: "台湾", gender: "男", hot: 85 },
    { name: "程响", enName: "Cheng Xiang", debutYear: "2011", debutDetail: "2011年《不再联系》", genre: ["流行", "抒情"], reps: ["不再联系", "四季予你", "世界这么大还是遇见你"], bio: "温暖治愈系女声。", bio_en: "Warm and healing female voice.", bio_ja: "温かく癒やしのボーカル。", region: "内地", gender: "女", hot: 83 },
    { name: "赵磊", enName: "Zhao Lei", debutYear: "2016", debutDetail: "2016《燃烧吧少年》", genre: ["流行", "抒情"], reps: ["呼吸", "永恒", "Lover"], bio: "X玖少年团成员，温柔嗓音。", bio_en: "Member of X-NINE, gentle voice.", bio_ja: "X玖少年团メンバー。", region: "内地", gender: "男", hot: 81 },
    { name: "廖俊涛", enName: "Liao Juntao", debutYear: "2017", debutDetail: "2017年《明日之子》出道", genre: ["流行", "民谣"], reps: ["谁", "无言", "你说的对"], bio: "创作才子，歌曲《谁》感动无数人。", bio_en: "Talented songwriter, his song 'Who' moved many.", bio_ja: "才能あるシンガーソングライター。", region: "内地", gender: "男", hot: 82 },
    { name: "陈粒", enName: "Chen Li", debutYear: "2014", debutDetail: "2014《如也》", genre: ["独立民谣", "艺术流行"], reps: ["奇妙能力歌", "易燃易爆炸", "小半"], bio: "独立音乐领军人物，个性鲜明。", bio_en: "Leader of indie music, distinctive personality.", bio_ja: "インディーズ音楽のリーダー。", region: "内地", gender: "女", hot: 89 },
    { name: "吴青峰", enName: "Wu Qingfeng", debutYear: "2005", debutDetail: "苏打绿主唱", genre: ["独立", "流行"], reps: ["小情歌", "太空人", "无与伦比的美丽"], bio: "细腻声线，诗意歌词。", bio_en: "Delicate voice, poetic lyrics.", bio_ja: "繊細な声、詩的な歌詞。", region: "台湾", gender: "男", hot: 91 },
    { name: "田馥甄", enName: "Hebe Tien", debutYear: "2010", debutDetail: "SHE单飞", genre: ["独立流行", "抒情"], reps: ["小幸运", "魔鬼中的天使", "寂寞寂寞就好"], bio: "文艺女神，嗓音空灵。", bio_en: "Goddess of art, ethereal voice.", bio_ja: "アートの女神。", region: "台湾", gender: "女", hot: 94 },
    { name: "杨丞琳", enName: "Rainie Yang", debutYear: "2000", debutDetail: "4 in Love组合", genre: ["流行", "抒情"], reps: ["暧昧", "年轮说", "雨爱"], bio: "全能艺人，演技歌艺俱佳。", bio_en: "All-round entertainer, good at acting and singing.", bio_ja: "万能エンターテイナー。", region: "台湾", gender: "女", hot: 89 },
    { name: "梁静茹", enName: "Fish Leong", debutYear: "1999", debutDetail: "1999《一夜长大》", genre: ["抒情", "情歌"], reps: ["勇气", "宁夏", "会呼吸的痛"], bio: "情歌天后，疗愈系嗓音。", bio_en: "Queen of love songs, healing voice.", bio_ja: "ラブソングの女王。", region: "海外", gender: "女", hot: 96 },
    { name: "汪峰", enName: "Wang Feng", debutYear: "1994", debutDetail: "鲍家街43号", genre: ["摇滚"], reps: ["春天里", "北京北京", "怒放的生命"], bio: "摇滚半壁江山，创作力旺盛。", bio_en: "Half of Chinese rock, prolific songwriter.", bio_ja: "中国ロックの半分。", region: "内地", gender: "男", hot: 92 },
    { name: "那英", enName: "Na Ying", debutYear: "1988", debutDetail: "1988出道", genre: ["流行"], reps: ["征服", "白天不懂夜的黑", "默"], bio: "天后级唱将，乐坛常青树。", bio_en: "Diva-level singer, evergreen in music industry.", bio_ja: "ディーヴァレベルの歌手。", region: "内地", gender: "女", hot: 94 },
    { name: "李健", enName: "Li Jian", debutYear: "2001", debutDetail: "水木年华成员", genre: ["民谣", "古典"], reps: ["传奇", "贝加尔湖畔", "风吹麦浪"], bio: "音乐诗人，儒雅声线。", bio_en: "Music poet, elegant voice.", bio_ja: "音楽の詩人。", region: "内地", gender: "男", hot: 91 },
    { name: "胡彦斌", enName: "Hu Yanbin", debutYear: "2002", debutDetail: "2002《文武双全》", genre: ["R&B", "流行"], reps: ["男人KTV", "红颜", "你要的全拿走"], bio: "音乐魔法师，编曲鬼才。", bio_en: "Music magician, arrangement genius.", bio_ja: "音楽マジシャン。", region: "内地", gender: "男", hot: 88 },
    { name: "GAI周延", enName: "GAI", debutYear: "2017", debutDetail: "2017《中国有嘻哈》冠军", genre: ["嘻哈", "中国风"], reps: ["沧海一声笑", "虎山行", "兰花草"], bio: "说唱江湖气，中国风嘻哈代表。", bio_en: "Rap with Jianghu spirit, representative of Chinese-style hip-hop.", bio_ja: "江湖の精神を持つラップ。", region: "内地", gender: "男", hot: 87 },
    { name: "陈楚生", enName: "Chen Chusheng", debutYear: "2007", debutDetail: "2007快男冠军", genre: ["民谣", "流行"], reps: ["有没有人告诉你", "思念一个荒废的名字"], bio: "灵魂吉他手，淡然声线。", bio_en: "Soul guitarist, calm voice.", bio_ja: "ソウルギタリスト。", region: "内地", gender: "男", hot: 85 },
    { name: "戴佩妮", enName: "Penny Tai", debutYear: "2000", debutDetail: "2000《Penny》", genre: ["流行", "民谣"], reps: ["怎样", "你要的爱", "街角的祝福"], bio: "创作才女，金曲歌后。", bio_en: "Talented songwriter, Golden Melody Best Female Singer.", bio_ja: "才能あるソングライター。", region: "海外", gender: "女", hot: 88 },
    { name: "徐佳莹", enName: "Lala Hsu", debutYear: "2008", debutDetail: "2008星光大道冠军", genre: ["流行", "创作"], reps: ["身骑白马", "失落沙洲", "寻人启事"], bio: "唱作俱佳，金曲歌后。", bio_en: "Great singer-songwriter, Golden Melody Best Female Singer.", bio_ja: "優れたシンガーソングライター。", region: "台湾", gender: "女", hot: 90 },
    { name: "陈洁丽", enName: "Jerry Chan", debutYear: "2003", debutDetail: "2003年发行首张个人专辑《心曲》", genre: ["粤语流行", "发烧人声"], reps: ["一水隔天涯", "小雨中的回忆", "绿色的旋律"], bio: "Hi-Fi天后，嗓音清丽甜美，字正腔圆。", bio_en: "Hi-Fi queen with a sweet, clear voice.", bio_ja: "Hi-Fi界の歌姫。透き通る甘い歌声。", region: "内地", gender: "女", hot: 85 },
    { name: "李佳薇", enName: "Jess Lee", debutYear: "2010", debutDetail: "2010年《超级星光大道》冠军出道", genre: ["流行", "抒情", "高音"], reps: ["煎熬", "像天堂的悬崖", "大火"], bio: "铁肺女王，以《煎熬》震撼乐坛。", bio_en: "Powerhouse vocalist known for 'Suffering'.", bio_ja: "鉄肺の女王。「煎熬」で楽壇を震撼させた。", region: "海外", gender: "女", hot: 89 },
    {name: "赵英俊", enName: "Zhao Yingjun", debutYear: "2004", debutDetail: "2004年参加选秀节目《我型我秀》出道", genre: ["流行", "摇滚", "影视原声"], reps: ["刺激2005", "大王叫我来巡山", "送你一朵小红花"], bio: "创作鬼才、潇洒哥，影视歌曲爆款制造机，以《刺激2005》开启网络歌曲新时代。", bio_en: "Creative genius known as 'Xiaosa Ge', hitmaker of film & TV songs.", bio_ja: "創作の鬼才、通称「潇洒哥」。映画・ドラマ主題歌のヒットメーカー。", region: "国内", gender: "男", hot: 100},
	{name: "刘惜君", enName: "Sara Liu", debutYear: "2004", debutDetail: "2004年凭借单曲《贝壳风铃》崭露头角，2009年获《快乐女声》全国五强出道", genre: ["华语流行", "独立摇滚", "影视原声"],reps: ["我很快乐", "怎么唱情歌", "大风吹"], bio: "温婉深情的女歌手，以高辨识度嗓音和影视金曲闻名，近年凭《大风吹》再度翻红。",bio_en: "Warm and soulful female singer known for her distinctive voice and film soundtracks.", bio_ja: "温かく感情豊かな女性歌手。特徴的な声質と映画主題歌で知られる。", region: "国内", gender: "女", hot: 101}
  ];

  // 翻译字典 (含风格映射)
  const translations = {
    zh: { pageTitle: "🎤 歌手小百科", placeholder: "搜歌手 / 英文名 / 风格 / 代表作", searchBtn: "搜索", resultPrefix: "位小可爱歌手", reset: "重置", cardFooter: "戳我查看完整百科", modalDebut: "出道", modalGenre: "音乐风格", modalReps: "代表作", modalBio: "艺人小传", filterEra: "📅 年代", filterRegion: "🌍 地区", all: "全部", sortLabel: "🔽 排序", sortYearAsc: "出道年份 ↑", sortYearDesc: "出道年份 ↓", sortNameAsc: "A → Z", sortNameDesc: "Z → A", sortHot: "🔥 热度", genreMap: { "流行":"流行","抒情":"抒情","R&B":"R&B","摇滚":"摇滚","民谣":"民谣","舞曲":"舞曲","中国风":"中国风","灵魂":"灵魂","民族":"民族","粤语流行":"粤语流行","嘻哈":"嘻哈","电子":"电子","美声":"美声","独立":"独立","蓝调":"蓝调","爵士":"爵士","创作":"创作","实验":"实验","影视":"影视","发烧人声":"发烧人声","高音":"高音" } },
    ja: { pageTitle: "🎵 歌手小百科", placeholder: "歌手名・英語・ジャンルで検索", searchBtn: "検索", resultPrefix: "人のアーティスト", reset: "リセット", cardFooter: "クリックで詳細", modalDebut: "デビュー", modalGenre: "ジャンル", modalReps: "代表曲", modalBio: "プロフィール", filterEra: "📅 年代", filterRegion: "🌍 地域", all: "全て", sortLabel: "🔽 並び替え", sortYearAsc: "デビュー年 ↑", sortYearDesc: "デビュー年 ↓", sortNameAsc: "A → Z", sortNameDesc: "Z → A", sortHot: "🔥 人気", genreMap: { "流行":"ポップ","抒情":"バラード","R&B":"R&B","摇滚":"ロック","民谣":"フォーク","舞曲":"ダンス","中国风":"中華風","灵魂":"ソウル","民族":"民族","粤语流行":"広東ポップ","嘻哈":"ヒップホップ","电子":"エレクトロ","美声":"ベルカント","独立":"インディー","蓝调":"ブルース","爵士":"ジャズ","创作":"創作","实验":"実験","影视":"映画・ドラマ","发烧人声":"オーディオファイル","高音":"高音" } },
    en: { pageTitle: "🎶 Singerpedia", placeholder: "Search by name / English / genre", searchBtn: "Search", resultPrefix: "sweet singers", reset: "Reset", cardFooter: "Click for full bio", modalDebut: "Debut", modalGenre: "Genre", modalReps: "Hits", modalBio: "Biography", filterEra: "📅 Era", filterRegion: "🌍 Region", all: "All", sortLabel: "🔽 Sort", sortYearAsc: "Debut ↑", sortYearDesc: "Debut ↓", sortNameAsc: "A → Z", sortNameDesc: "Z → A", sortHot: "🔥 Hot", genreMap: { "流行":"Pop","抒情":"Ballad","R&B":"R&B","摇滚":"Rock","民谣":"Folk","舞曲":"Dance","中国风":"Chinese Style","灵魂":"Soul","民族":"Ethnic","粤语流行":"Cantopop","嘻哈":"Hip-hop","电子":"Electronic","美声":"Bel Canto","独立":"Indie","蓝调":"Blues","爵士":"Jazz","创作":"Singer-songwriter","实验":"Experimental","影视":"Film/TV","发烧人声":"Audiophile","高音":"High Note" } }
  };

  let currentLang = "zh";
  let currentDisplayList = [...singersDB];
  let activeFilters = { era: null, region: null, genre: null };
  let currentSort = 'hot';
  let searchHistory = JSON.parse(localStorage.getItem('musicSearchHistory')) || [];

  // 辅助函数
  function getEra(y) { const year = parseInt(y); if(year<1970) return '1960s'; if(year<1980) return '1970s'; if(year<1990) return '1980s'; if(year<2000) return '1990s'; if(year<2010) return '2000s'; if(year<2020) return '2010s'; return '2020s'; }
  function getBio(s) { if(currentLang==='zh') return s.bio; if(currentLang==='en') return s.bio_en||s.bio; return s.bio_ja||s.bio_en||s.bio; }

  function applyFiltersAndSort(list) {
    let filtered = list.filter(s => {
      if(activeFilters.era && getEra(s.debutYear) !== activeFilters.era) return false;
      if(activeFilters.region && s.region !== activeFilters.region) return false;
      if(activeFilters.genre && !s.genre.includes(activeFilters.genre)) return false;
      return true;
    });
    if(currentSort==='yearAsc') filtered.sort((a,b)=>parseInt(a.debutYear)-parseInt(b.debutYear));
    else if(currentSort==='yearDesc') filtered.sort((a,b)=>parseInt(b.debutYear)-parseInt(a.debutYear));
    else if(currentSort==='nameAsc') filtered.sort((a,b)=>a.name.localeCompare(b.name,'zh'));
    else if(currentSort==='nameDesc') filtered.sort((a,b)=>b.name.localeCompare(a.name,'zh'));
    else if(currentSort==='hot') filtered.sort((a,b)=>(b.hot||0)-(a.hot||0));
    return filtered;
  }

  function renderSingers(singers) {
    const grid = document.getElementById("singersGrid");
    const t = translations[currentLang];
    document.getElementById("resultCount").innerText = `${singers.length} ${t.resultPrefix}`;
    if(!singers.length) { grid.innerHTML = '<div style="grid-column:1/-1; text-align:center; padding:3rem;">✨ 没有找到小可爱歌手，换个词试试吧～</div>'; return; }
    grid.innerHTML = singers.map(s => {
      const displayName = (currentLang!=='zh' && s.enName) ? s.enName : s.name;
      return `<div class="singer-card" data-name="${s.name}"><div class="card-inner"><div class="card-top"><div class="avatar"><i class="fas fa-star"></i></div><div><div class="singer-name">${displayName}</div><div class="debut-badge">🎤 ${s.debutYear}</div></div></div><div class="reps">${s.reps.slice(0,3).map(r=>`<span class="rep-tag">${r}</span>`).join('')}</div><div class="card-footer">${t.cardFooter}</div></div></div>`;
    }).join('');
    document.querySelectorAll('.singer-card').forEach(card => card.addEventListener('click', ()=>{
      const singer = singersDB.find(s=>s.name===card.dataset.name);
      if(singer) showModal(singer);
    }));
  }

  function showModal(singer) {
    const t = translations[currentLang];
    const modal = document.getElementById("singerModal");
    modal.style.display = "flex";
    document.getElementById("modalBody").innerHTML = `<h2>🎤 ${singer.name} ${singer.enName?`(${singer.enName})`:''}</h2><div class="modal-detail"><p><span class="label">${t.modalDebut}</span> ${singer.debutYear} · ${singer.debutDetail}</p><p><span class="label">${t.modalGenre}</span> ${singer.genre.map(g=>t.genreMap[g]||g).join(' / ')}</p><p><span class="label">${t.modalReps}</span> ${singer.reps.join(' · ')}</p><p><span class="label">📖 ${t.modalBio}</span><br>${getBio(singer)}</p><p style="margin-top:12px; font-size:0.8rem; color:#cc9a80;">✨ 小百科 · 持续更新 ✨</p></div>`;
  }

  function renderFilters() {
    const t = translations[currentLang];
    const eraContainer = document.getElementById('eraFilters');
    const regionContainer = document.getElementById('regionFilters');
    const eras = ['1960s','1970s','1980s','1990s','2000s','2010s','2020s'];
    eraContainer.innerHTML = `<span class="chip ${!activeFilters.era?'active':''}" data-era="">${t.all}</span>` + eras.map(e=>`<span class="chip ${activeFilters.era===e?'active':''}" data-era="${e}">${e}</span>`).join('');
    const regions = [...new Set(singersDB.map(s=>s.region))];
    regionContainer.innerHTML = `<span class="chip ${!activeFilters.region?'active':''}" data-region="">${t.all}</span>` + regions.map(r=>`<span class="chip ${activeFilters.region===r?'active':''}" data-region="${r}">${r}</span>`).join('');
    const genreCount = {}; singersDB.forEach(s=>s.genre.forEach(g=>genreCount[g]=(genreCount[g]||0)+1));
    const sortedGenres = Object.entries(genreCount).sort((a,b)=>b[1]-a[1]).slice(0,12);
    document.getElementById('genreTagCloud').innerHTML = sortedGenres.map(([g])=>`<span class="cloud-tag ${activeFilters.genre===g?'active':''}" data-genre="${g}">${t.genreMap[g]||g}</span>`).join('');
    document.querySelectorAll('[data-era]').forEach(el=>el.addEventListener('click',()=>{ activeFilters.era = el.dataset.era || null; updateDisplay(); }));
    document.querySelectorAll('[data-region]').forEach(el=>el.addEventListener('click',()=>{ activeFilters.region = el.dataset.region || null; updateDisplay(); }));
    document.querySelectorAll('[data-genre]').forEach(el=>el.addEventListener('click',()=>{ const g=el.dataset.genre; activeFilters.genre = activeFilters.genre===g?null:g; updateDisplay(); }));
  }

  function updateDisplay() {
    const filtered = applyFiltersAndSort(currentDisplayList);
    renderSingers(filtered);
    renderFilters();
  }

  function resetAllFilters() {
    activeFilters = { era: null, region: null, genre: null };
    currentSort = 'hot';
    document.querySelectorAll('.sort-btn').forEach(b=>b.classList.remove('active'));
    document.querySelector('.sort-btn[data-sort="hot"]').classList.add('active');
    document.getElementById('searchInput').value = '';
    currentDisplayList = [...singersDB];
    updateDisplay();
  }

  function performSearch(keyword) {
    if(!keyword.trim()) currentDisplayList = [...singersDB];
    else {
      const kw = keyword.trim().toLowerCase();
      currentDisplayList = singersDB.filter(s=> s.name.toLowerCase().includes(kw) || (s.enName&&s.enName.toLowerCase().includes(kw)) || s.genre.some(g=>g.toLowerCase().includes(kw)) || s.reps.some(r=>r.toLowerCase().includes(kw)) );
    }
    if(keyword.trim()) { searchHistory = searchHistory.filter(k=>k!==keyword.trim()); searchHistory.unshift(keyword.trim()); if(searchHistory.length>8) searchHistory.pop(); localStorage.setItem('musicSearchHistory', JSON.stringify(searchHistory)); }
    updateDisplay();
  }

  function applyLanguage() {
    const t = translations[currentLang];
    document.getElementById("pageTitle").innerHTML = t.pageTitle;
    document.getElementById("searchInput").placeholder = t.placeholder;
    document.getElementById("searchBtnText").innerText = t.searchBtn;
    document.getElementById("resetBtn").innerHTML = `🔄 ${t.reset}`;
    document.getElementById("filterEraLabel").innerText = t.filterEra;
    document.getElementById("filterRegionLabel").innerText = t.filterRegion;
    document.getElementById("sortLabel").innerText = t.sortLabel;
    document.getElementById("sortYearAsc").innerHTML = t.sortYearAsc;
    document.getElementById("sortYearDesc").innerHTML = t.sortYearDesc;
    document.getElementById("sortNameAsc").innerHTML = t.sortNameAsc;
    document.getElementById("sortNameDesc").innerHTML = t.sortNameDesc;
    document.getElementById("sortHot").innerHTML = t.sortHot;
    updateDisplay();
  }

  // ---------- 猜代表作游戏 ----------
  let currentGameSinger = null;
  function newGameQuestion() {
    const eligible = singersDB.filter(s => s.reps && s.reps.length > 0);
    currentGameSinger = eligible[Math.floor(Math.random() * eligible.length)];
    const rep = currentGameSinger.reps[Math.floor(Math.random() * currentGameSinger.reps.length)];
    document.getElementById("gameQuestion").innerText = `代表作：《${rep}》 是哪位歌手的？`;
    document.getElementById("gameAnswerInput").value = '';
  }
  function checkGameAnswer() {
    const answer = document.getElementById("gameAnswerInput").value.trim();
    if (!currentGameSinger) return;
    const isCorrect = answer === currentGameSinger.name || (currentGameSinger.enName && answer.toLowerCase() === currentGameSinger.enName.toLowerCase());
    if (isCorrect) {
      alert(`✅ 回答正确！就是 ${currentGameSinger.name}！`);
      showModal(currentGameSinger);
      newGameQuestion();
    } else {
      alert(`❌ 不对哦，再试试看～ 提示：${currentGameSinger.name.charAt(0)}**`);
    }
  }

  // ---------- AI 助手 (增强) ----------
  function findSingerByName(q) {
    const lower = q.toLowerCase();
    return singersDB.find(s=>s.name.toLowerCase()===lower || (s.enName&&s.enName.toLowerCase()===lower)) || singersDB.find(s=>s.name.toLowerCase().includes(lower)||(s.enName&&s.enName.toLowerCase().includes(lower)));
  }
  async function getAIResponse(msg) {
    const t = translations[currentLang];
    const lower = msg.toLowerCase();
    for(let p of [/介绍[一下]?[：:]?\s*([^，。？\s]+)/, /([^，。？\s]+)是谁/, /([^，。？\s]+)的[代表作|歌]/]) {
      const m = msg.match(p); if(m) { const singer = findSingerByName(m[1]); if(singer) return `${singer.name}${singer.enName?'('+singer.enName+')':''}，${singer.debutYear}年出道。\n风格：${singer.genre.map(g=>t.genreMap[g]||g).join('、')}\n代表作：${singer.reps.slice(0,3).join('、')}\n简介：${getBio(singer)}`; }
    }
    if(lower.includes('推荐')||lower.includes('随便')) { const r = singersDB[Math.floor(Math.random()*singersDB.length)]; return `为你推荐 ${r.name}，代表作《${r.reps[0]}》`; }
    if(lower.includes('多少')&&lower.includes('歌手')) return `当前收录 ${singersDB.length} 位歌手。`;
    return `可以问我具体歌手信息，比如“周杰伦是谁”，或者说“推荐歌手”～`;
  }

  // 初始化
  document.addEventListener('DOMContentLoaded', ()=>{
    applyLanguage();
    newGameQuestion();
    document.getElementById('randomSingerBtn').addEventListener('click', ()=>{
      const r = singersDB[Math.floor(Math.random()*singersDB.length)];
      showModal(r);
    });
    document.getElementById('gameSubmitBtn').addEventListener('click', checkGameAnswer);
    document.getElementById('gameNextBtn').addEventListener('click', newGameQuestion);
    document.getElementById('gameAnswerInput').addEventListener('keypress', e=>{ if(e.key==='Enter') checkGameAnswer(); });

    const searchInput = document.getElementById('searchInput');
    const suggestionsBox = document.getElementById('suggestionsBox');
    function renderSuggestions(kw) {
      if(!kw.trim()) {
        if(searchHistory.length) {
          suggestionsBox.innerHTML = `<div class="history-header">最近搜索 <span class="clear-history" id="clearHistoryBtn">清空</span></div>` + searchHistory.map(h=>`<div class="history-item" data-value="${h}"><i class="fas fa-history"></i> ${h}</div>`).join('');
          suggestionsBox.classList.add('show');
          document.querySelectorAll('.history-item').forEach(el=>el.addEventListener('click', ()=>{ searchInput.value=el.dataset.value; performSearch(el.dataset.value); suggestionsBox.classList.remove('show'); }));
          document.getElementById('clearHistoryBtn').onclick = ()=>{ searchHistory=[]; localStorage.setItem('musicSearchHistory','[]'); renderSuggestions(''); };
        } else suggestionsBox.classList.remove('show');
        return;
      }
      const kwLower = kw.trim().toLowerCase();
      const matches = singersDB.filter(s=>s.name.toLowerCase().includes(kwLower)||(s.enName&&s.enName.toLowerCase().includes(kwLower))).sort((a,b)=>a.name.toLowerCase().startsWith(kwLower)?-1:1).slice(0,8);
      if(!matches.length) { suggestionsBox.classList.remove('show'); return; }
      suggestionsBox.innerHTML = matches.map(s=>`<div class="suggestion-item" data-value="${s.name}"><i class="fas fa-search"></i> ${s.name} ${s.enName?'('+s.enName+')':''}</div>`).join('');
      suggestionsBox.classList.add('show');
      document.querySelectorAll('.suggestion-item').forEach(el=>el.addEventListener('click', ()=>{ searchInput.value=el.dataset.value; performSearch(el.dataset.value); suggestionsBox.classList.remove('show'); }));
    }
    searchInput.addEventListener('input', e=>renderSuggestions(e.target.value));
    searchInput.addEventListener('focus', ()=>renderSuggestions(searchInput.value));
    document.addEventListener('click', e=>{ if(!e.target.closest('.search-wrapper')) suggestionsBox.classList.remove('show'); });
    document.getElementById('searchBtn').addEventListener('click', ()=>{ performSearch(searchInput.value); suggestionsBox.classList.remove('show'); });
    document.getElementById('resetBtn').addEventListener('click', resetAllFilters);
    searchInput.addEventListener('keypress', e=>{ if(e.key==='Enter') { performSearch(searchInput.value); suggestionsBox.classList.remove('show'); }});
    document.querySelectorAll('.lang-btn').forEach(b=>b.addEventListener('click', ()=>{
      document.querySelectorAll('.lang-btn').forEach(bb=>bb.classList.remove('active')); b.classList.add('active');
      currentLang = b.dataset.lang; applyLanguage();
    }));
    document.querySelectorAll('.sort-btn').forEach(b=>b.addEventListener('click', ()=>{
      document.querySelectorAll('.sort-btn').forEach(bb=>bb.classList.remove('active')); b.classList.add('active');
      currentSort = b.dataset.sort; updateDisplay();
    }));
    const modal = document.getElementById('singerModal');
    document.querySelector('.close-modal').addEventListener('click', ()=>modal.style.display='none');
    window.addEventListener('click', e=>{ if(e.target===modal) modal.style.display='none'; });

    // AI 助手
    const aiToggle=document.getElementById('aiToggle'), aiPanel=document.getElementById('aiChatPanel'), aiClose=document.getElementById('aiClose'), aiMessages=document.getElementById('aiMessages'), aiInput=document.getElementById('aiInput'), aiSend=document.getElementById('aiSend');
    aiToggle.addEventListener('click', ()=>aiPanel.classList.toggle('open'));
    aiClose.addEventListener('click', ()=>aiPanel.classList.remove('open'));
    function addAIMessage(text, isUser=false) {
      const div = document.createElement('div'); div.className = `ai-message ${isUser?'user':''}`;
      div.innerHTML = isUser ? `<div class="bubble">${text}</div>` : `<div class="ai-avatar"><i class="fas fa-robot"></i></div><div class="bubble">${text}</div>`;
      aiMessages.appendChild(div); aiMessages.scrollTop = aiMessages.scrollHeight;
    }
    async function handleAISend() {
      const text = aiInput.value.trim(); if(!text) return;
      addAIMessage(text, true); aiInput.value = '';
      const reply = await getAIResponse(text); addAIMessage(reply);
    }
    aiSend.addEventListener('click', handleAISend);
    aiInput.addEventListener('keypress', e=>{ if(e.key==='Enter') handleAISend(); });
    document.addEventListener('click', e=>{ if(!e.target.closest('.ai-assistant') && aiPanel.classList.contains('open')) aiPanel.classList.remove('open'); });
  });
})();
</script>
</body>
</html>
