<!DOCTYPE html> 
<html lang="zh-CN"> 
<head> 
    <meta charset="UTF-8"> 
    <meta name="viewport" content="width=device-width, initial-scale=1.0, 
viewport-fit=cover"> 
    <title>《逐玉》 - 史诗级古装奇幻巨制 | 电视剧官网</title> 
    <!-- Font Awesome 6 (免费图标库) --> 
    <link rel="stylesheet" 
href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css"> 
    <!-- Google Fonts：优雅字体组合 --> 
    <link 
href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..
32,600;14..32,700&family=Cormorant+Garamond:ital,wght@0,400;0,600;1,400&display=sw
ap" rel="stylesheet"> 


  <!-- 导航栏 -->
<nav class="navbar">
    <div class="nav-container">
        <a href="#hero">首页</a>
        <a href="#synopsis">剧情简介</a>
        <a href="#cast">主演阵容</a>
        <a href="#videos">精彩内容</a>
        <a href="#info">剧集信息</a>
    </div>
</nav>

  /* 导航栏样式 */
.navbar {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background: rgba(10, 8, 20, 0.85);
    backdrop-filter: blur(10px);
    z-index: 20;
    box-shadow: 0 2px 10px rgba(0,0,0,0.5);
    padding: 0.6rem 0;
}

.nav-container {
    max-width: 1280px;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    gap: 2rem;
}

.nav-container a {
    color: var(--gold-accent);
    text-decoration: none;
    font-weight: 500;
    padding: 0.4rem 0.8rem;
    border-radius: 24px;
    transition: all 0.3s ease;
}

.nav-container a:hover {
    background: var(--gold-accent);
    color: #1e1a2f;
    transform: scale(1.05);
}

/* 给页面内容增加顶部间距，避免被导航栏遮挡 */
.main-wrapper {
    padding-top: 100px; /* 导航栏高度 + 间距 */
}

/* 平滑滚动 */
html {
    scroll-behavior: smooth;
}


    <style> 
        * { 
            margin: 0; 
            padding: 0; 
            box-sizing: border-box; 
        } 
 
        /* CSS 变量定义 (动态阴霾透明度) */ 
        :root { 
            --haze-opacity: 0.65;      /* 默认阴霾强度 65% */ 
            --card-bg: rgba(10, 8, 20, 0.75); 
            --gold-accent: #d4af7a; 
            --text-light: #f3f1f0; 
            --transition-smooth: all 0.3s ease; 
        } 
 
        body { 
            font-family: 'Inter', sans-serif; 
            background-color: #0a0a14; 
            color: var(--text-light); 
            line-height: 1.5; 
            min-height: 100vh; 
            position: relative; 
            /* 默认背景图（高清雾岚山脉，符合逐玉仙侠意境）*/ 
            background-image: 
url('https://cdn.pixabay.com/photo/2020/07/23/01/29/misty-mountains-5430620_1280.jpg'); 
            background-size: cover; 
            background-position: center 30%; 
            background-attachment: fixed; 
            background-repeat: no-repeat; 
        } 
 
        /* 阴霾效果层 (动态半透明黑色覆盖，实现阴霾感) */ 
        body::before { 
            content: ""; 
            position: fixed; 
            top: 0; 
            left: 0; 
            width: 100%; 
            height: 100%; 
            background-color: rgba(0, 0, 0, var(--haze-opacity)); 
            backdrop-filter: blur(2px);   /* 轻微模糊增强阴霾氛围 */ 
            z-index: 1; 
            pointer-events: none;          /* 让所有点击穿透到内容 */ 
        } 
 
        /* 主要内容容器，高于阴霾层 */ 
        .main-wrapper { 
            position: relative; 
            z-index: 2; 
            max-width: 1280px; 
            margin: 0 auto; 
            padding: 2rem 2rem 3rem; 
        } 
 
        /* 可自定义工具栏 (背景上传 + 阴霾调节) */ 
        .toolbar { 
            position: fixed; 
            bottom: 1.5rem; 
            right: 1.5rem; 
            z-index: 10; 
            background: rgba(0, 0, 0, 0.65); 
            backdrop-filter: blur(12px); 
            border-radius: 48px; 
            padding: 0.6rem 1.2rem; 
            display: flex; 
            gap: 1rem; 
            align-items: center; 
            flex-wrap: wrap; 
            border: 1px solid rgba(212, 175, 122, 0.4); 
            box-shadow: 0 8px 20px rgba(0,0,0,0.3); 
            font-size: 0.85rem; 
        } 
 
        .toolbar button, .toolbar label { 
            background: rgba(20, 20, 30, 0.8); 
            border: none; 
            color: var(--gold-accent); 
            padding: 0.4rem 0.9rem; 
            border-radius: 32px; 
            font-size: 0.8rem; 
            font-weight: 500; 
            cursor: pointer; 
            transition: var(--transition-smooth); 
            display: inline-flex; 
            align-items: center; 
            gap: 0.5rem; 
            backdrop-filter: blur(4px); 
            font-family: 'Inter', sans-serif; 
        } 
 
        .toolbar button:hover, .toolbar label:hover { 
            background: var(--gold-accent); 
            color: #1e1a2f; 
            transform: scale(1.02); 
        } 
 
        .toolbar input[type="range"] { 
            width: 110px; 
            cursor: pointer; 
            background: rgba(212,175,122,0.3); 
            height: 3px; 
            border-radius: 3px; 
        } 
 
        .haze-slider { 
            display: flex; 
            align-items: center; 
            gap: 8px; 
            color: #e0cfb1; 
        } 
 
        /* 卡片通用样式 (半透明+毛玻璃融合) */ 
        .card { 
            background: var(--card-bg); 
            backdrop-filter: blur(8px); 
            border-radius: 32px; 
            padding: 1.8rem 2rem; 
            margin-bottom: 2rem; 
            border: 1px solid rgba(212, 175, 122, 0.25); 
            box-shadow: 0 20px 35px -12px rgba(0, 0, 0, 0.4); 
            transition: transform 0.2s ease, border-color 0.2s; 
        } 
 
        .card:hover { 
            border-color: rgba(212, 175, 122, 0.6); 
        } 
 
        /* 头部区域 */ 
        .hero { 
            text-align: center; 
            margin-bottom: 2rem; 
            padding: 1rem 0; 
        } 
 
        .hero h1 { 
            font-size: 5rem; 
            font-weight: 700; 
            font-family: 'Cormorant Garamond', serif; 
            letter-spacing: 6px; 
            background: linear-gradient(135deg, #FFF8E7, #d4af7a, #e9c891); 
            background-clip: text; 
            -webkit-background-clip: text; 
            color: transparent; 
            text-shadow: 0 2px 10px rgba(0,0,0,0.3); 
            margin-bottom: 0.5rem; 
        } 
 
        .hero .sub { 
            font-size: 1.1rem; 
            letter-spacing: 3px; 
            color: #e0cfb1; 
            border-top: 1px solid rgba(212,175,122,0.4); 
            display: inline-block; 
            padding-top: 0.5rem; 
            font-weight: 300; 
        } 
 
        .tagline { 
            margin-top: 1rem; 
            font-style: italic; 
            font-size: 1.2rem; 
            font-weight: 300; 
            color: #f3e5c9; 
        } 
 
        /* 评分与元数据 */ 
        .meta-grid { 
            display: flex; 
            flex-wrap: wrap; 
            justify-content: center; 
            gap: 2rem; 
            margin: 1.8rem 0 0; 
        } 
 
        .meta-item { 
            background: rgba(0,0,0,0.5); 
            padding: 0.5rem 1.2rem; 
            border-radius: 60px; 
            font-size: 0.9rem; 
            font-weight: 500; 
            backdrop-filter: blur(4px); 
        } 
 
        .meta-item i { 
            color: var(--gold-accent); 
            margin-right: 8px; 
        } 
 
        /* 简介区 */ 
        .synopsis p { 
            font-size: 1.05rem; 
            line-height: 1.7; 
            margin-bottom: 1rem; 
            text-align: justify; 
        } 
 
        .section-title { 
            font-size: 1.8rem; 
            font-family: 'Cormorant Garamond', serif; 
            font-weight: 600; 
            margin-bottom: 1.5rem; 
            border-left: 5px solid var(--gold-accent); 
            padding-left: 1rem; 
            letter-spacing: -0.3px; 
        } 
 
        /* 演员网格 */ 
        .cast-grid { 
            display: grid; 
            grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); 
            gap: 1.8rem; 
            margin-top: 1rem; 
        } 
 
        .cast-card { 
            background: rgba(0, 0, 0, 0.45); 
            backdrop-filter: blur(6px); 
            border-radius: 28px; 
            padding: 1.2rem; 
            text-align: center; 
            transition: all 0.25s; 
            border: 1px solid rgba(212,175,122,0.2); 
        } 
 
        .cast-card:hover { 
            transform: translateY(-6px); 
            border-color: var(--gold-accent); 
            background: rgba(0,0,0,0.6); 
        } 
 
        .avatar { 
            width: 100px; 
            height: 100px; 
            background: linear-gradient(145deg, #332c42, #1e1a2f); 
            border-radius: 50%; 
            margin: 0 auto 1rem; 
            display: flex; 
            align-items: center; 
            justify-content: center; 
            font-size: 2.8rem; 
            color: var(--gold-accent); 
            border: 2px solid rgba(212,175,122,0.7); 
            box-shadow: 0 8px 14px rgba(0,0,0,0.3); 
        } 
 
        .cast-card h4 { 
            font-size: 1.3rem; 
            font-weight: 600; 
            margin-bottom: 0.3rem; 
        } 
 
        .cast-card .role { 
            font-size: 0.9rem; 
            color: #d4c5a5; 
            font-style: italic; 
        } 
 
        .cast-card .actor-name { 
            font-size: 0.9rem; 
            margin-top: 0.5rem; 
            opacity: 0.85; 
        } 
 
        /* 角色介绍双列 */ 
        .roles-grid { 
            display: grid; 
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); 
            gap: 1.5rem; 
        } 
 
        .role-item { 
            background: rgba(20, 15, 30, 0.7); 
            border-radius: 24px; 
            padding: 1.2rem 1.5rem; 
            border-left: 4px solid var(--gold-accent); 
        } 
 
        .role-item strong { 
            font-size: 1.2rem; 
            color: var(--gold-accent); 
            display: block; 
            margin-bottom: 0.4rem; 
        } 
 
        /* 剧集信息栏 */ 
        .info-bar { 
            display: flex; 
            flex-wrap: wrap; 
            justify-content: space-between; 
            gap: 1rem; 
            background: rgba(0,0,0,0.5); 
            border-radius: 40px; 
            padding: 1rem 2rem; 
            margin-top: 0.5rem; 
        } 
 
        .info-bar span i { 
            margin-right: 8px; 
            color: var(--gold-accent); 
        } 
 
        /* 按钮装饰 */ 
        .btn-trailer { 
            display: inline-flex; 
            align-items: center; 
            gap: 12px; 
            background: linear-gradient(95deg, #d4af7a, #b28b4c); 
            border: none; 
            padding: 0.7rem 2rem; 
            border-radius: 40px; 
            font-weight: 700; 
            color: #1e1a2f; 
            margin-top: 0.5rem; 
            cursor: pointer; 
            transition: 0.2s; 
            font-size: 0.9rem; 
        } 
 
        .btn-trailer:hover { 
            transform: scale(1.02); 
            background: linear-gradient(95deg, #e6c48b, #c59d5a); 
            box-shadow: 0 6px 14px rgba(0,0,0,0.3); 
        } 
 
        footer { 
            text-align: center; 
            margin-top: 3rem; 
            padding: 1.5rem; 
            font-size: 0.75rem; 
            opacity: 0.7; 
            border-top: 1px solid rgba(212,175,122,0.2); 
        } 
 
        /* 响应式设计 */ 
        @media (max-width: 780px) { 
            .main-wrapper { 
                padding: 1.2rem; 
            } 
            .hero h1 { 
                font-size: 3rem; 
            } 
            .section-title { 
                font-size: 1.5rem; 
            } 
            .toolbar { 
                bottom: 1rem; 
                right: 1rem; 
                padding: 0.4rem 0.9rem; 
                gap: 0.6rem; 
            } 
            .card { 
                padding: 1.2rem; 
            } 
            .info-bar { 
                flex-direction: column; 
                align-items: flex-start; 
            } 
        } 
 
        /* 自定义文件上传按钮 */ 
        input#bgUpload { 
            display: none; 
        } 
        .reset-bg { 
            background: rgba(0,0,0,0.7); 
        } 
        i.fa, i.far, i.fas { 
            pointer-events: none; 
        } 
		
		.video-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 20px;
}

.video-item h4 {
    margin-bottom: 10px;
    font-size: 18px;
}

.video-item video {
    width: 100%;
    border-radius: 12px;
}


.info-card {
    width: 100%;
    border: 1px solid #e5e5e5;
    border-radius: 6px;
    overflow: hidden;
    font-size: 14px;
    color: #333;
}

.row {
    display: grid;
    grid-template-columns: 100px 1fr 100px 1fr;
    border-bottom: 1px dashed #ddd;
}

.row:last-child {
    border-bottom: none;
}

.label {
    background: #f5f5f5;
    padding: 10px;
    color: #666;
}

.value {
    padding: 10px;
}

    </style> 
</head> 
<body> 
 
<div class="main-wrapper"> 
    <!-- 主视觉 Hero --> 
    <div class="hero"> 
        <h1>逐·玉</h1> 
        <div class="sub">CHASING JADE</div> 
        <div class="tagline">「 命运与选择交织 · 爱与责任并存 」</div> 
        <div class="meta-grid">
            <div class="meta-item"><i class="fas fa-book"></i> 改编自：沉筱之小说</div>
            <div class="meta-item"><i class="fas fa-film"></i> 类型：古装 / 剧情 / 爱情</div>
            <div class="meta-item"><i class="fas fa-globe"></i> 制作地区：中国大陆</div>
            <div class="meta-item"><i class="fas fa-layer-group"></i> 文学IP改编作品</div>
        </div>
    </div> 
 
    <!-- 剧情简介 --> 
    <div id="synopsis" class="card synopsis"> 
    <div class="card synopsis"> 
        <div class="section-title"><i class="fas fa-feather-alt" style="margin-right: 12px;"></i> 缘
起 · 逐玉之劫</div> 
        <p>
《逐玉》改编自沉筱之创作的同名小说，是一部古装题材影视作品。
故事以人物成长与命运抉择为主线，围绕复杂的人物关系与时代背景展开，
融合情感、权谋与个人理想等元素。
</p>

<p>
剧情讲述主人公在多方势力与环境变化中逐渐成长，在情感与责任之间不断抉择，
逐步揭开隐藏的真相。作品通过细腻的人物刻画与情节推进，
展现角色在时代洪流中的变化与坚持。
</p>

<p>
该作品原著连载于晋江文学城，拥有较高人气与读者基础，
影视改编在保留核心设定的同时，对剧情进行了适当调整，
以增强视觉表现与叙事节奏。
</p> 
</div>

    <!-- 主演阵容 --> 
    <div id="cast" class="card"> 
    <div class="card">
        <div class="section-title"><i class="fas fa-users"></i> 主演阵容</div> 
        <div class="cast-grid"> 
            <div class="cast-card"> 
                <div class="avatar"><img src="[images/xiezheng.jpg](https://tse4.mm.bing.net/th/id/OIP.K8cIMlSKxuKCl3ijMwi8GwHaHb?rs=1&pid=ImgDetMain&o=7&rm=3)" alt="谢征"></div> 
                <h4>谢征</h4> 
                <div class="role">武安侯将军</div> 
                <div class="actor-name">张凌赫 · 饰</div> 
            </div> 
            <div class="cast-card"> 
                <div class="avatar"><img src="images/xiezheng.jpg" alt="樊长玉"></div> 
                <h4>樊长玉</h4> 
                <div class="role">樊家屠户</div> 
                <div class="actor-name">田曦薇 · 饰</div> 
            </div> 
            <div class="cast-card"> 
                <div class="avatar"><img src="images/xiezheng.jpg" alt="俞浅浅"></div> 
                <h4>俞浅浅</h4> 
                <div class="role">溢香楼女掌柜</div> 
                <div class="actor-name">孔雪儿 · 饰</div> 
            </div> 
            <div class="cast-card"> 
                <div class="avatar"><img src="images/xiezheng.jpg" alt="公孙鄞"></div>  
                <h4>公孙鄞</h4> 
                <div class="role">河问一贤</div> 
                <div class="actor-name">李卿 · 饰</div> 
            </div> 
            <div class="cast-card"> 
                <div class="avatar"><img src="images/xiezheng.jpg" alt="齐晏"></div> 
                <h4>齐晏</h4> 
                <div class="role">皇太孙</div> 
                <div class="actor-name">邓凯 · 饰</div> 
            </div> 
            <div class="cast-card"> 
                <div class="avatar"><img src="images/xiezheng.jpg" alt="随元青"></div>  
                <h4>随元青</h4> 
                <div class="role">长信王世子</div> 
                <div class="actor-name">林沐然 · 饰</div> 
            </div> 
        </div> 
    </div> 
    </div>
 
    <div class="card"> 
    <div class="section-title">
        <i class="fas fa-video"></i> 精彩内容
    </div> 
    <div id="videos" class="card">
    <div class="video-grid">

        <!-- 预告片 -->
        <div class="video-item">
            <h4>🎬 预告片</h4>
            <video controls poster="images/trailer-cover.jpg">
                <source src="videos/trailer.mp4" type="video/mp4">
                你的浏览器不支持 video 标签
            </video>
        </div>

        <!-- 主题曲 -->
        <div class="video-item">
            <h4>🎵 主题曲</h4>
            <video controls poster="images/theme-cover.jpg">
                <source src="videos/theme.mp4" type="video/mp4">
                你的浏览器不支持 video 标签
            </video>
        </div>

    </div>
</div>
</div>

    <!-- 剧集亮点 / 播出详情 --> 
    <div id="info" class="info-card"> 
    <div class="info-card">
    <div class="row">
        <div class="label">中文名</div>
        <div class="value">逐玉</div>
        <div class="label">制片人</div>
        <div class="value">叶丹（总制片人）、吕婷艳</div>
    </div>

    <div class="row">
        <div class="label">外文名</div>
        <div class="value">Pursuit of Jade</div>
        <div class="label">导演</div>
        <div class="value">富拓</div>
    </div>

    <div class="row">
        <div class="label">作品类型</div>
        <div class="value">古装、爱情</div>
        <div class="label">监制</div>
        <div class="value">王晓晖、王柯</div>
    </div>

    <div class="row">
        <div class="label">语言</div>
        <div class="value">普通话</div>
        <div class="label">出品公司</div>
        <div class="value">爱奇艺、腾讯视频、浩瀚娱乐</div>
    </div>

    <div class="row">
        <div class="label">主演</div>
        <div class="value">张凌赫、田曦薇、任豪、孔雪儿、邓凯</div>
        <div class="label">拍摄地点</div>
        <div class="value">浙江、重庆</div>
    </div>

    <div class="row">
        <div class="label">首播时间</div>
        <div class="value">2026年3月6日</div>
        <div class="label">播放平台</div>
        <div class="value">腾讯视频、爱奇艺、Netflix</div>
    </div>

    <div class="row">
        <div class="label">集数</div>
        <div class="value">40集</div>
        <div class="label">单集时长</div>
        <div class="value">45分钟</div>
    </div>
    </div>
    
</div> 
 
    <footer> 
        <i class="fas fa-copyright"></i> 2026 逐玉剧组 · 官方网站 
    </footer> 
</div> 
</body> 
</html> 
