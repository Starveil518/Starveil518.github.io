<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MC 指令大师 · 80+ 低/中/高阶交互教程</title>
    <!-- Font Awesome & Google Font -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,500;14..32,600;14..32,700;14..32,800&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        /* ----- Reset & Variables (与之前保持一致) ----- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --bg-body: #0d1117;
            --bg-card: #161b22;
            --bg-card-hover: #1c2333;
            --border-color: #30363d;
            --text-primary: #f0f6fc;
            --text-secondary: #8b949e;
            --text-muted: #484f58;
            --mc-green: #58a6ff;
            --mc-green-bright: #1f6feb;
            --accent-glow: rgba(88, 166, 255, 0.15);
            --radius: 12px;
            --transition: 0.25s cubic-bezier(0.4, 0, 0.2, 1);
            --shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
        }

        body {
            font-family: 'Inter', -apple-system, sans-serif;
            background: var(--bg-body);
            color: var(--text-primary);
            padding: 24px 20px 60px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
        }

        .container {
            max-width: 1280px;
            width: 100%;
        }

        .header {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            gap: 20px;
            padding: 16px 0 28px;
            border-bottom: 1px solid var(--border-color);
            margin-bottom: 32px;
        }

        .header h1 {
            font-size: 2.2rem;
            font-weight: 800;
            letter-spacing: -0.5px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .header h1 i {
            color: var(--mc-green);
            font-size: 2rem;
        }

        .header .stats {
            font-size: 0.85rem;
            background: var(--bg-card);
            padding: 8px 18px;
            border-radius: 40px;
            border: 1px solid var(--border-color);
            color: var(--text-secondary);
        }

        .header .stats i {
            color: var(--mc-green);
            margin-right: 6px;
        }

        .controls {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 12px 20px;
            background: var(--bg-card);
            padding: 16px 24px;
            border-radius: var(--radius);
            border: 1px solid var(--border-color);
            margin-bottom: 32px;
            box-shadow: var(--shadow);
        }

        .controls .filter-group {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            align-items: center;
        }

        .controls label {
            font-size: 0.8rem;
            font-weight: 600;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-right: 4px;
        }

        .btn-filter {
            background: transparent;
            border: 1px solid var(--border-color);
            color: var(--text-secondary);
            padding: 6px 16px;
            border-radius: 40px;
            font-size: 0.82rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            font-family: inherit;
        }

        .btn-filter:hover {
            background: var(--bg-body);
            color: var(--text-primary);
            border-color: var(--mc-green);
        }

        .btn-filter.active {
            background: var(--mc-green-bright);
            border-color: var(--mc-green-bright);
            color: #fff;
            box-shadow: 0 0 20px var(--accent-glow);
        }

        .btn-filter.version-btn {
            border-color: var(--border-color);
        }
        .btn-filter.version-btn.active-java {
            background: #da6b3e;
            border-color: #da6b3e;
            color: #fff;
        }
        .btn-filter.version-btn.active-netease {
            background: #2d8b57;
            border-color: #2d8b57;
            color: #fff;
        }

        .search-box {
            flex: 1;
            min-width: 180px;
            display: flex;
            align-items: center;
            background: var(--bg-body);
            border-radius: 40px;
            padding: 4px 16px;
            border: 1px solid var(--border-color);
            transition: var(--transition);
        }

        .search-box:focus-within {
            border-color: var(--mc-green);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }

        .search-box i {
            color: var(--text-muted);
            margin-right: 10px;
            font-size: 0.9rem;
        }

        .search-box input {
            background: transparent;
            border: none;
            padding: 10px 0;
            color: var(--text-primary);
            font-size: 0.9rem;
            width: 100%;
            outline: none;
            font-family: inherit;
        }

        .search-box input::placeholder {
            color: var(--text-muted);
        }

        .reset-btn {
            background: transparent;
            border: none;
            color: var(--text-muted);
            cursor: pointer;
            padding: 4px 8px;
            border-radius: 30px;
            transition: var(--transition);
        }
        .reset-btn:hover {
            color: var(--text-primary);
            background: var(--bg-card);
        }

        .action-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-left: auto;
        }

        .btn-action-ctrl {
            background: transparent;
            border: 1px solid var(--border-color);
            color: var(--text-secondary);
            padding: 6px 16px;
            border-radius: 40px;
            font-size: 0.78rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            font-family: inherit;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }

        .btn-action-ctrl:hover {
            background: var(--bg-body);
            color: var(--text-primary);
            border-color: var(--mc-green);
        }

        .btn-action-ctrl.random-btn {
            background: rgba(88, 166, 255, 0.08);
            border-color: rgba(88, 166, 255, 0.2);
            color: var(--mc-green);
        }
        .btn-action-ctrl.random-btn:hover {
            background: rgba(88, 166, 255, 0.18);
        }

        .command-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 16px;
            margin-top: 8px;
        }

        .command-card {
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: var(--radius);
            padding: 18px 24px;
            transition: var(--transition);
            display: flex;
            flex-direction: column;
            gap: 6px;
            position: relative;
            overflow: hidden;
        }

        .command-card:hover {
            background: var(--bg-card-hover);
            border-color: var(--mc-green);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
            transform: translateY(-2px);
        }

        .command-card.highlight-flash {
            animation: flash 1.2s ease 3;
            border-color: #f0c040;
            box-shadow: 0 0 30px rgba(240, 192, 64, 0.3);
        }

        @keyframes flash {
            0%, 100% { background: var(--bg-card); }
            50% { background: #2a2a1a; }
        }

        .command-card .top-row {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            gap: 12px;
        }

        .command-card .cmd-text {
            font-family: 'JetBrains Mono', 'Courier New', monospace;
            font-size: 1.05rem;
            font-weight: 600;
            color: #f0883e;
            background: rgba(255, 255, 255, 0.04);
            padding: 2px 14px;
            border-radius: 8px;
            border-left: 3px solid var(--mc-green);
            word-break: break-all;
        }

        .command-card .tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
        }

        .tag-level {
            font-size: 0.65rem;
            font-weight: 700;
            padding: 2px 12px;
            border-radius: 40px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .tag-low {
            background: #1f3a5f;
            color: #7cb9ff;
            border: 1px solid #2a4a7a;
        }
        .tag-mid {
            background: #3d3a1f;
            color: #f5d742;
            border: 1px solid #5a4f1a;
        }
        .tag-high {
            background: #4a1f2a;
            color: #ff7b89;
            border: 1px solid #7a2a3a;
        }

        .tag-version {
            font-size: 0.6rem;
            font-weight: 700;
            padding: 2px 10px;
            border-radius: 40px;
            text-transform: uppercase;
            background: var(--bg-body);
            color: var(--text-secondary);
            border: 1px solid var(--border-color);
        }

        .tag-version.java {
            color: #da6b3e;
            border-color: #da6b3e44;
            background: #da6b3e11;
        }
        .tag-version.netease {
            color: #2d8b57;
            border-color: #2d8b5744;
            background: #2d8b5711;
        }

        .command-card .description {
            color: var(--text-secondary);
            font-size: 0.92rem;
            line-height: 1.5;
            margin: 4px 0 2px;
            padding-left: 4px;
        }

        .command-card .description code {
            background: var(--bg-body);
            padding: 1px 8px;
            border-radius: 4px;
            font-size: 0.8rem;
            color: var(--mc-green);
        }

        .command-card .action-bar {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 10px;
            margin-top: 8px;
            border-top: 1px solid rgba(255, 255, 255, 0.04);
            padding-top: 10px;
        }

        .btn-action {
            background: transparent;
            border: 1px solid var(--border-color);
            color: var(--text-secondary);
            padding: 4px 14px;
            border-radius: 30px;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-family: inherit;
        }

        .btn-action:hover {
            background: var(--bg-body);
            color: var(--text-primary);
            border-color: var(--mc-green);
        }

        .btn-action.copy-btn {
            background: var(--bg-body);
            border-color: var(--border-color);
        }
        .btn-action.copy-btn.copied {
            background: var(--mc-green-bright);
            border-color: var(--mc-green-bright);
            color: #fff;
        }

        .btn-action.demo-btn {
            background: rgba(88, 166, 255, 0.08);
            border-color: rgba(88, 166, 255, 0.2);
            color: var(--mc-green);
        }
        .btn-action.demo-btn:hover {
            background: rgba(88, 166, 255, 0.18);
        }

        .btn-action .fa-chevron-down {
            font-size: 0.6rem;
            transition: var(--transition);
        }

        .btn-action .fa-chevron-down.open {
            transform: rotate(180deg);
        }

        .command-card .detail-box {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.4s ease, padding 0.3s ease, opacity 0.2s ease;
            opacity: 0;
            padding: 0 4px;
            background: var(--bg-body);
            border-radius: 8px;
            margin-top: 0;
            border: 1px solid transparent;
        }

        .command-card .detail-box.open {
            max-height: 600px;
            opacity: 1;
            padding: 16px 20px;
            margin-top: 12px;
            border-color: var(--border-color);
            overflow-y: auto;
        }

        .command-card .detail-box code {
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.82rem;
            color: #a5d6ff;
            display: block;
            white-space: pre-wrap;
            word-break: break-all;
            line-height: 1.8;
        }

        .command-card .detail-box .example-label {
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: var(--text-muted);
            margin-bottom: 6px;
        }

        .no-results {
            text-align: center;
            padding: 60px 20px;
            color: var(--text-secondary);
            display: none;
        }
        .no-results i {
            font-size: 3rem;
            margin-bottom: 16px;
            opacity: 0.4;
        }

        .mod-section {
            margin-top: 48px;
            background: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: var(--radius);
            padding: 24px 28px;
        }

        .mod-section h3 {
            font-size: 1.1rem;
            font-weight: 600;
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 12px;
        }

        .mod-section h3 i {
            color: var(--mc-green);
        }

        .mod-section .file-tree-sm {
            background: var(--bg-body);
            padding: 16px 20px;
            border-radius: 8px;
            font-family: 'Courier New', monospace;
            font-size: 0.8rem;
            color: var(--text-secondary);
            border: 1px solid var(--border-color);
            line-height: 2;
        }

        .mod-section .file-tree-sm .dir {
            color: var(--mc-green);
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 1.6rem;
            }
            .controls {
                padding: 14px 16px;
                flex-direction: column;
                align-items: stretch;
            }
            .controls .filter-group {
                justify-content: center;
            }
            .search-box {
                width: 100%;
            }
            .action-buttons {
                margin-left: 0;
                justify-content: center;
            }
            .command-card .top-row {
                flex-direction: column;
                align-items: flex-start;
            }
            .command-card .cmd-text {
                font-size: 0.9rem;
                width: 100%;
            }
            .command-card {
                padding: 14px 16px;
            }
        }

        @media (max-width: 480px) {
            .btn-filter {
                font-size: 0.7rem;
                padding: 4px 12px;
            }
            .command-card .action-bar {
                flex-wrap: wrap;
            }
        }

        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: var(--bg-body);
        }
        ::-webkit-scrollbar-thumb {
            background: var(--border-color);
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: var(--mc-green);
        }
    </style>
</head>
<body>
    <div class="container">

        <!-- ===== HEADER ===== -->
        <header class="header">
            <h1>
                <i class="fas fa-terminal"></i> 指令大师
                <span style="font-size:0.8rem; font-weight:400; color:var(--text-secondary); margin-left:8px;">80+ 低 · 中 · 高阶</span>
            </h1>
            <div class="stats">
                <i class="fas fa-list"></i> <span id="countDisplay">0</span> 条指令
            </div>
        </header>

        <!-- ===== CONTROLS ===== -->
        <div class="controls">
            <div class="filter-group">
                <label><i class="fas fa-tag"></i> 版本</label>
                <button class="btn-filter version-btn active-java" data-version="java" id="btnJava"><i class="fab fa-java"></i> Java</button>
                <button class="btn-filter version-btn" data-version="netease" id="btnNetease"><i class="fas fa-dragon"></i> 网易</button>
            </div>

            <div class="filter-group">
                <label><i class="fas fa-layer-group"></i> 等级</label>
                <button class="btn-filter active" data-level="all">全部</button>
                <button class="btn-filter" data-level="low"><span class="tag-level tag-low" style="border:none; background:transparent; padding:0 4px;">低阶</span></button>
                <button class="btn-filter" data-level="mid"><span class="tag-level tag-mid" style="border:none; background:transparent; padding:0 4px;">中阶</span></button>
                <button class="btn-filter" data-level="high"><span class="tag-level tag-high" style="border:none; background:transparent; padding:0 4px;">高阶</span></button>
            </div>

            <div class="search-box">
                <i class="fas fa-search"></i>
                <input type="text" id="searchInput" placeholder="搜索指令或描述...">
                <button class="reset-btn" id="clearSearch" title="清除搜索"><i class="fas fa-times-circle"></i></button>
            </div>

            <div class="action-buttons">
                <button class="btn-action-ctrl random-btn" id="randomBtn"><i class="fas fa-dice"></i> 随机</button>
                <button class="btn-action-ctrl" id="expandAllBtn"><i class="fas fa-plus-square"></i> 展开全部</button>
                <button class="btn-action-ctrl" id="collapseAllBtn"><i class="fas fa-minus-square"></i> 收起全部</button>
            </div>
        </div>

        <!-- ===== COMMAND GRID ===== -->
        <div id="commandGrid" class="command-grid"></div>
        <div class="no-results" id="noResults">
            <i class="fas fa-cube"></i>
            <p>没有找到匹配的指令，试试其他筛选条件吧。</p>
        </div>

        <!-- ===== MOD 附录 ===== -->
        <div class="mod-section">
            <h3><i class="fas fa-puzzle-piece"></i> 模组开发速览 · VS Code 结构</h3>
            <div class="file-tree-sm">
                <span class="dir">📁 你的 Fabric 模组/</span><br>
                ├── <span class="dir">📁 src/main/</span><br>
                │   ├── <span class="dir">📁 java/com/你的包/</span>  <span style="color:var(--text-muted);"># 主类 (YourMod.java)</span><br>
                │   └── <span class="dir">📁 resources/</span><br>
                │       ├── <span class="dir">📁 assets/模组ID/</span>  <span style="color:var(--text-muted);"># 贴图/模型</span><br>
                │       └── <span style="color:#f0883e;">📄 fabric.mod.json</span>  <span style="color:var(--text-muted);"># ⭐ 模组清单</span><br>
                ├── <span style="color:#f0883e;">📄 build.gradle</span>  <span style="color:var(--text-muted);"># 依赖管理</span><br>
                └── <span style="color:var(--text-muted);">📄 gradle.properties</span>
            </div>
            <div style="margin-top:12px; display:flex; flex-wrap:wrap; gap:12px;">
                <span class="btn-action" style="cursor:default; background:var(--bg-body);"><i class="fas fa-code"></i> ./gradlew genSources</span>
                <span class="btn-action" style="cursor:default; background:var(--bg-body);"><i class="fas fa-play"></i> ./gradlew runClient</span>
                <span class="btn-action" style="cursor:default; background:var(--bg-body);"><i class="fas fa-cube"></i> 网易 Add-on: behavior_pack + resource_pack</span>
            </div>
        </div>

    </div>

    <script>
        (function() {
            // ---------- 指令数据集 (80+ 条，大幅增加高阶难度) ----------
            const commands = [
                // ===== Java 低阶 (14条) =====
                { id: 1, version: 'java', level: 'low', cmd: '/gamemode creative', desc: '切换至创造模式', detail: '示例: /gamemode 1  \n/gamemode creative  (1.13+)' },
                { id: 2, version: 'java', level: 'low', cmd: '/time set day', desc: '设置时间为白天', detail: '夜晚: /time set night  \n中午: /time set noon' },
                { id: 3, version: 'java', level: 'low', cmd: '/weather clear', desc: '清除天气，变为晴天', detail: '下雨: /weather rain  \n雷暴: /weather thunder' },
                { id: 4, version: 'java', level: 'low', cmd: '/tp @p 100 64 100', desc: '传送最近的玩家到指定坐标', detail: '相对坐标: /tp ~5 ~ ~  \n面向: /tp @p ~ ~ ~ 90 0' },
                { id: 5, version: 'java', level: 'low', cmd: '/give @s diamond 64', desc: '给予自己 64 个钻石', detail: '支持NBT: /give @s diamond{Enchantments:[{id:"sharpness",lvl:5}]} 1' },
                { id: 6, version: 'java', level: 'low', cmd: '/defaultgamemode survival', desc: '设置新玩家默认游戏模式', detail: '可选: survival, creative, adventure, spectator' },
                { id: 7, version: 'java', level: 'low', cmd: '/difficulty easy', desc: '设置难度为简单', detail: '可选: peaceful, easy, normal, hard' },
                { id: 8, version: 'java', level: 'low', cmd: '/enchant @s sharpness 5', desc: '给手中物品附魔（仅限创造模式）', detail: '需要手持可附魔物品，等级需有效' },
                { id: 9, version: 'java', level: 'low', cmd: '/xp add @p 100', desc: '给最近的玩家增加100经验点', detail: '也可加等级: /xp add @p 10 levels' },
                { id: 10, version: 'java', level: 'low', cmd: '/me 正在挖矿', desc: '发送一条第三人称动作消息', detail: '显示: * 你的名字 正在挖矿' },
                { id: 11, version: 'java', level: 'low', cmd: '/tell @a 大家好', desc: '向所有玩家发送私聊消息', detail: '别名: /msg, /w' },
                { id: 12, version: 'java', level: 'low', cmd: '/seed', desc: '显示当前世界的种子', detail: '仅显示，无法修改' },
                { id: 13, version: 'java', level: 'low', cmd: '/worldborder get', desc: '查看世界边界大小', detail: '设置: /worldborder set 1000' },
                { id: 14, version: 'java', level: 'low', cmd: '/playsound minecraft:entity.enderman.teleport ambient @p ~ ~ ~ 1 1', desc: '播放音效（末影人传送）', detail: '格式: playsound <音效> <来源> <目标> <坐标> <音量> <音调>' },
                // ===== Java 中阶 (16条) =====
                { id: 15, version: 'java', level: 'mid', cmd: '/execute as @a at @s run say 你好', desc: '让所有玩家在各自位置说“你好”', detail: '核心语法: as <目标> at <目标> run <指令>  \n可嵌套: /execute as @e[type=creeper] at @s run summon lightning_bolt' },
                { id: 16, version: 'java', level: 'mid', cmd: '/effect @p speed 60 2 true', desc: '给最近的玩家 60s 速度 II (隐藏粒子)', detail: '格式: /effect <目标> <效果> <秒数> <等级> <隐藏粒子>  \n常用: haste, strength, night_vision' },
                { id: 17, version: 'java', level: 'mid', cmd: '/gamerule doDaylightCycle false', desc: '停止昼夜交替', detail: 'true 恢复  \n其他: mobGriefing, keepInventory, commandBlockOutput' },
                { id: 18, version: 'java', level: 'mid', cmd: '/scoreboard objectives add kills dummy 击杀数', desc: '创建计分板目标 (虚拟)', detail: '显示: /scoreboard objectives setdisplay sidebar kills  \n操作: /scoreboard players add @p kills 1' },
                { id: 19, version: 'java', level: 'mid', cmd: '/tag @p add 管理员', desc: '给最近的玩家添加标签“管理员”', detail: '移除: /tag @p remove 管理员  \n选择器: @a[tag=管理员]' },
                { id: 20, version: 'java', level: 'mid', cmd: '/team add red "红队"', desc: '创建队伍“红队”', detail: '加入: /team join red @p  \n可选颜色: red, blue, green' },
                { id: 21, version: 'java', level: 'mid', cmd: '/scoreboard players set @p deaths 0', desc: '设置玩家的deaths计分板为0', detail: '操作: /scoreboard players operation @p deaths += @a[limit=1] deaths' },
                { id: 22, version: 'java', level: 'mid', cmd: '/attribute @p minecraft:generic.max_health base set 40', desc: '设置玩家最大生命值为40', detail: '可修改其他属性: movement_speed, attack_damage' },
                { id: 23, version: 'java', level: 'mid', cmd: '/loot give @p minecraft:chest minecraft:chests/abandoned_mineshaft', desc: '给予玩家废弃矿井战利品', detail: '也可替换实体装备: /loot replace entity @s armor.chest ...' },
                { id: 24, version: 'java', level: 'mid', cmd: '/recipe give @p minecraft:stone', desc: '解锁石头的合成配方', detail: '全部解锁: /recipe give @p *' },
                { id: 25, version: 'java', level: 'mid', cmd: '/advancement grant @p everything', desc: '授予玩家所有进度', detail: '撤销: /advancement revoke @p everything' },
                { id: 26, version: 'java', level: 'mid', cmd: '/schedule function my:test 10s', desc: '调度函数在10秒后执行', detail: '需在数据包中定义函数' },
                { id: 27, version: 'java', level: 'mid', cmd: '/setworldspawn ~ ~ ~', desc: '设置世界出生点', detail: '新玩家将从该点附近出生' },
                { id: 28, version: 'java', level: 'mid', cmd: '/spreadplayers 0 0 10 100 false @p', desc: '将玩家随机分散在半径10-100的圆环内', detail: '常用于开局分散' },
                { id: 29, version: 'java', level: 'mid', cmd: '/team modify red color red', desc: '修改队伍颜色为红色', detail: '可选颜色: red, blue, green, yellow, aqua, white, gray, dark_gray, dark_red' },
                { id: 30, version: 'java', level: 'mid', cmd: '/bossbar add health "生命值"', desc: '创建一个Boss条', detail: '设置: /bossbar set health color red  \n/bossbar set health value 100' },
                // ===== Java 高阶 (新增 22条，大幅增加难度) =====
                { id: 31, version: 'java', level: 'high', cmd: '/execute if entity @e[type=player,limit=1] run say 有玩家在线', desc: '条件执行：如果有玩家实体则说话', detail: 'if 条件  \nunless 非条件  \n可嵌套: /execute as @a if score @s kills matches 10.. run say 击杀数≥10' },
                { id: 32, version: 'java', level: 'high', cmd: '/data get entity @s Health', desc: '获取自身的生命值 (NBT)', detail: '修改: /data merge entity @e[type=player,limit=1] {Health:20.0f}  \n获取块: /data get block ~ ~ ~' },
                { id: 33, version: 'java', level: 'high', cmd: '/execute as @a at @s store result score @s health run data get entity @s Health', desc: '将玩家的生命值存储到计分板 (health)', detail: 'store result/ success 可存储至计分板或bossbar  \n配合命令方块可实现复杂数据统计' },
                { id: 34, version: 'java', level: 'high', cmd: '/summon minecraft:zombie ~ ~1 ~ {HandItems:[{id:"diamond_sword",Count:1}],CustomName:"\\"Boss\\""}', desc: '生成手持钻石剑且命名为“Boss”的僵尸 (NBT)', detail: 'NBT 可定义装备、属性、AI等  \n常用: {NoAI:1b, Silent:1b, Health:100f}' },
                { id: 35, version: 'java', level: 'high', cmd: '/data modify block ~ ~ ~ Items append value {id:"minecraft:diamond",Count:16}', desc: '向容器 (箱子) 中追加物品 (修改NBT)', detail: '也适用于实体: /data modify entity @e[type=chest_minecart,limit=1] Items append ...' },
                { id: 36, version: 'java', level: 'high', cmd: '/data merge entity @e[type=player,limit=1] {Health:20.0f}', desc: '合并NBT数据，修改玩家生命值', detail: '可修改任意NBT，需谨慎' },
                { id: 37, version: 'java', level: 'high', cmd: '/data remove entity @s Inventory[0]', desc: '删除玩家背包第一个物品', detail: '索引从0开始' },
                { id: 38, version: 'java', level: 'high', cmd: '/execute if block ~ ~-1 ~ minecraft:grass_block run say 站在草地上', desc: '检测脚下方块是否为草方块', detail: '条件判断，可用于触发器' },
                { id: 39, version: 'java', level: 'high', cmd: '/execute unless score @p kills matches 10 run say 击杀不足', desc: '如果击杀数不匹配10则说话', detail: 'unless 表示条件为假时执行' },
                { id: 40, version: 'java', level: 'high', cmd: '/execute as @e[type=creeper] at @s run summon lightning_bolt', desc: '在每个苦力怕的位置召唤闪电', detail: '常用作陷阱或特效' },
                { id: 41, version: 'java', level: 'high', cmd: '/function custom:main', desc: '运行数据包中的 main.mcfunction', detail: '需在数据包的 functions 目录下' },
                { id: 42, version: 'java', level: 'high', cmd: '/datapack enable "vanilla"', desc: '启用数据包 (vanilla)', detail: '禁用: /datapack disable "vanilla"  \n列表: /datapack list' },
                { id: 43, version: 'java', level: 'high', cmd: '/scoreboard players operation @p kills += @a[limit=1] kills', desc: '将第一个玩家的击杀数加到自身', detail: '支持 += -= *= /= %= 等运算' },
                { id: 44, version: 'java', level: 'high', cmd: '/scoreboard objectives modify kills displayname "击杀数"', desc: '修改计分板显示名称', detail: '也可修改渲染类型: /scoreboard objectives modify kills rendertype hearts' },
                { id: 45, version: 'java', level: 'high', cmd: '/worldborder center 100 100', desc: '设置世界边界中心点', detail: '结合 set 使用' },
                { id: 46, version: 'java', level: 'high', cmd: '/worldborder warning distance 10', desc: '设置边界警告距离为10格', detail: '时间警告: /worldborder warning time 15' },
                { id: 47, version: 'java', level: 'high', cmd: '/worldborder set 5000', desc: '设置世界边界大小为5000', detail: '可指定缓动时间: /worldborder set 5000 60s' },
                { id: 48, version: 'java', level: 'high', cmd: '/loot replace entity @s armor.chest minecraft:cobblestone', desc: '将玩家胸甲替换为圆石', detail: '也可用 /loot give 给予物品' },
                { id: 49, version: 'java', level: 'high', cmd: '/loot spawn ~ ~ ~ loot minecraft:chests/end_city_treasure', desc: '在坐标处生成末地城战利品', detail: 'loot 参数丰富' },
                { id: 50, version: 'java', level: 'high', cmd: '/advancement grant @p only minecraft:story/mine_stone', desc: '授予玩家特定进度', detail: 'revoke 类似' },
                { id: 51, version: 'java', level: 'high', cmd: '/schedule function my:loop 5s 100', desc: '调度函数在5秒后执行，重复100次', detail: '无限循环可省略次数' },
                { id: 52, version: 'java', level: 'high', cmd: '/data modify entity @e[type=player,limit=1] Health set value 10.0f', desc: '修改玩家生命值为10 (使用modify)', detail: '相比 merge 更灵活，支持 append, prepend, set, remove' },
                { id: 53, version: 'java', level: 'high', cmd: '/data modify storage my:data test set value "hello"', desc: '存储数据到自定义存储空间', detail: '存储可用于跨函数传递数据' },
                { id: 54, version: 'java', level: 'high', cmd: '/execute store result score @p health run data get entity @s Health', desc: '存储生命值到计分板 (简化版)', detail: 'store result 可存储整数, success 存储成功与否' },
                { id: 55, version: 'java', level: 'high', cmd: '/execute if predicate custom:test', desc: '执行条件基于自定义预测 (predicate)', detail: 'predicate 定义在数据包 predicates 目录下' },
                { id: 56, version: 'java', level: 'high', cmd: '/team modify red collisionRule never', desc: '设置队伍碰撞规则为永不', detail: '可选: always, never, pushOtherTeams' },
                { id: 57, version: 'java', level: 'high', cmd: '/team modify red deathMessageVisibility hidden', desc: '隐藏队伍成员的死亡消息', detail: '可选: always, never, hiddenForOtherTeams, hiddenForOwnTeam' },
                { id: 58, version: 'java', level: 'high', cmd: '/debug start', desc: '开始性能调试 (生成profile文件)', detail: '/debug stop 结束' },
                { id: 59, version: 'java', level: 'high', cmd: '/tick rate 50', desc: '设置游戏刻速率为50 (每秒50刻，默认20)', detail: '用于性能测试或加速' },
                // ===== 网易版 (基岩) 低阶 (6条) =====
                { id: 101, version: 'netease', level: 'low', cmd: '/gamemode c', desc: '切换至创造模式 (网易版)', detail: '生存: /gamemode s  \n冒险: /gamemode m' },
                { id: 102, version: 'netease', level: 'low', cmd: '/locate village', desc: '定位最近的村庄', detail: '其他: /locate stronghold, /locate mansion, /locate monument' },
                { id: 103, version: 'netease', level: 'low', cmd: '/difficulty easy', desc: '设置难度为简单', detail: '可选: peaceful, easy, normal, hard' },
                { id: 104, version: 'netease', level: 'low', cmd: '/enchant @s sharpness 5', desc: '附魔手中物品', detail: '需在创造模式或拥有经验' },
                { id: 105, version: 'netease', level: 'low', cmd: '/xp 100 @p', desc: '给予最近的玩家100经验', detail: '也可加等级: /xp 10 levels @p' },
                { id: 106, version: 'netease', level: 'low', cmd: '/me 正在建筑', desc: '发送动作消息', detail: '显示: * 你的名字 正在建筑' },
                // ===== 网易版 中阶 (6条) =====
                { id: 107, version: 'netease', level: 'mid', cmd: '/effect @p speed 30 3 true', desc: '给最近的玩家 30s 速度 III', detail: '网易版支持大部分原版效果' },
                { id: 108, version: 'netease', level: 'mid', cmd: '/summon ender_dragon', desc: '生成末影龙', detail: '也可生成: /summon lightning_bolt  \n/summon creeper ~~~ minecraft:become_charged' },
                { id: 109, version: 'netease', level: 'mid', cmd: '/clone ~-5 ~ ~-5 ~5 ~5 ~5 ~10 ~ ~', desc: '复制一个区域', detail: '格式: clone <源区域> <目标位置>  \n需加载区域' },
                { id: 110, version: 'netease', level: 'mid', cmd: '/fill ~-10 ~-1 ~-10 ~10 ~10 ~10 stone', desc: '填充石砖区域', detail: '可指定方块数据值' },
                { id: 111, version: 'netease', level: 'mid', cmd: '/setblock ~ ~1 ~ diamond_block', desc: '在头顶放置钻石块', detail: '常用建造或快速修改' },
                { id: 112, version: 'netease', level: 'mid', cmd: '/testfor @p[tag=admin]', desc: '检测最近的玩家是否有“admin”标签', detail: '用于条件触发 (需配合命令方块)' },
                // ===== 网易版 高阶 (新增 8条，增加难度) =====
                { id: 113, version: 'netease', level: 'high', cmd: '/kill @e[type=slime]', desc: '清除所有史莱姆', detail: '选择器支持 type, name, tag, family 等  \n/kill @e[family=monster] 清除所有怪物' },
                { id: 114, version: 'netease', level: 'high', cmd: '/function custom:main', desc: '运行函数 (需行为包)', detail: '网易Add-on支持函数文件 (.mcfunction)  \n需放置在 behavior_pack/functions/ 下' },
                { id: 115, version: 'netease', level: 'high', cmd: '/structure save house ~-5 ~-5 ~-5 ~5 ~5 ~5', desc: '保存区域为结构“house”', detail: '加载: /structure load house ~ ~ ~  \n删除: /structure delete house' },
                { id: 116, version: 'netease', level: 'high', cmd: '/tickingarea add circle ~ ~ ~ 3 管理区', desc: '添加一个常加载区域', detail: '防止实体消失，常用于红石机器' },
                { id: 117, version: 'netease', level: 'high', cmd: '/replaceitem entity @p slot.hotbar 0 diamond_sword', desc: '将玩家快捷栏第一个格子替换为钻石剑', detail: 'slot.armor.head 等可用于装备' },
                { id: 118, version: 'netease', level: 'high', cmd: '/clear @p diamond', desc: '清除玩家背包中的钻石', detail: '可指定数量: /clear @p diamond 64' },
                { id: 119, version: 'netease', level: 'high', cmd: '/playsound random.explode @a ~ ~ ~ 1 1', desc: '播放爆炸音效给所有玩家', detail: '音量、音调可调' },
                { id: 120, version: 'netease', level: 'high', cmd: '/title @p title 欢迎', desc: '显示大标题给最近的玩家', detail: 'subtitle 副标题, actionbar 操作栏' },
            ];

            // ---------- DOM 引用 ----------
            const grid = document.getElementById('commandGrid');
            const countDisplay = document.getElementById('countDisplay');
            const noResults = document.getElementById('noResults');

            let currentVersion = 'java';
            let currentLevel = 'all';
            let searchTerm = '';

            const btnJava = document.getElementById('btnJava');
            const btnNetease = document.getElementById('btnNetease');
            const levelBtns = document.querySelectorAll('[data-level]');
            const searchInput = document.getElementById('searchInput');
            const clearSearch = document.getElementById('clearSearch');
            const randomBtn = document.getElementById('randomBtn');
            const expandAllBtn = document.getElementById('expandAllBtn');
            const collapseAllBtn = document.getElementById('collapseAllBtn');

            // ---------- 渲染函数 ----------
            function render() {
                const filtered = commands.filter(cmd => {
                    if (cmd.version !== currentVersion) return false;
                    if (currentLevel !== 'all' && cmd.level !== currentLevel) return false;
                    if (searchTerm.trim() !== '') {
                        const term = searchTerm.trim().toLowerCase();
                        const inCmd = cmd.cmd.toLowerCase().includes(term);
                        const inDesc = cmd.desc.toLowerCase().includes(term);
                        const inDetail = cmd.detail ? cmd.detail.toLowerCase().includes(term) : false;
                        if (!inCmd && !inDesc && !inDetail) return false;
                    }
                    return true;
                });

                countDisplay.textContent = filtered.length;

                if (filtered.length === 0) {
                    grid.innerHTML = '';
                    noResults.style.display = 'block';
                    return;
                }
                noResults.style.display = 'none';

                let html = '';
                filtered.forEach(cmd => {
                    const levelLabel = cmd.level === 'low' ? '低阶' : cmd.level === 'mid' ? '中阶' : '高阶';
                    const levelClass = cmd.level === 'low' ? 'tag-low' : cmd.level === 'mid' ? 'tag-mid' : 'tag-high';
                    const versionLabel = cmd.version === 'java' ? 'Java' : '网易';
                    const versionClass = cmd.version === 'java' ? 'java' : 'netease';
                    const detailSafe = cmd.detail ? cmd.detail.replace(/\n/g, '<br>').replace(/  /g, '&nbsp;&nbsp;') : '';

                    html += `
                    <div class="command-card" data-id="${cmd.id}">
                        <div class="top-row">
                            <span class="cmd-text">${cmd.cmd}</span>
                            <div class="tags">
                                <span class="tag-level ${levelClass}">${levelLabel}</span>
                                <span class="tag-version ${versionClass}"><i class="${cmd.version === 'java' ? 'fab fa-java' : 'fas fa-dragon'}"></i> ${versionLabel}</span>
                            </div>
                        </div>
                        <div class="description">${cmd.desc}</div>
                        <div class="action-bar">
                            <button class="btn-action copy-btn" data-cmd="${cmd.cmd.replace(/"/g, '&quot;')}"><i class="fas fa-copy"></i> 复制</button>
                            <button class="btn-action demo-btn" data-demo="${cmd.cmd}"><i class="fas fa-play"></i> 演示</button>
                            <button class="btn-action toggle-detail"><i class="fas fa-chevron-down"></i> 详情</button>
                        </div>
                        <div class="detail-box">
                            <div class="example-label"><i class="fas fa-code"></i> 用法 / 示例</div>
                            <code>${detailSafe}</code>
                        </div>
                    </div>
                    `;
                });

                grid.innerHTML = html;

                // 绑定事件
                grid.querySelectorAll('.copy-btn').forEach(btn => {
                    btn.addEventListener('click', function(e) {
                        e.stopPropagation();
                        const cmdText = this.getAttribute('data-cmd');
                        if (!cmdText) return;
                        if (navigator.clipboard) {
                            navigator.clipboard.writeText(cmdText).then(() => {
                                this.classList.add('copied');
                                this.innerHTML = '<i class="fas fa-check"></i> 已复制';
                                setTimeout(() => {
                                    this.classList.remove('copied');
                                    this.innerHTML = '<i class="fas fa-copy"></i> 复制';
                                }, 2000);
                            }).catch(() => fallbackCopy(this, cmdText));
                        } else {
                            fallbackCopy(this, cmdText);
                        }
                    });
                });

                grid.querySelectorAll('.demo-btn').forEach(btn => {
                    btn.addEventListener('click', function(e) {
                        e.stopPropagation();
                        const demo = this.getAttribute('data-demo');
                        if (demo) {
                            alert(`🎮 模拟执行指令：\n${demo}\n\n（在游戏中按 T 输入即可执行）`);
                        }
                    });
                });

                grid.querySelectorAll('.toggle-detail').forEach(btn => {
                    btn.addEventListener('click', function(e) {
                        e.stopPropagation();
                        const card = this.closest('.command-card');
                        const detailBox = card.querySelector('.detail-box');
                        const icon = this.querySelector('.fa-chevron-down');
                        if (detailBox) {
                            detailBox.classList.toggle('open');
                            if (icon) icon.classList.toggle('open');
                            if (detailBox.classList.contains('open')) {
                                this.innerHTML = '<i class="fas fa-chevron-down open"></i> 收起';
                            } else {
                                this.innerHTML = '<i class="fas fa-chevron-down"></i> 详情';
                            }
                        }
                    });
                });
            }

            function fallbackCopy(btn, text) {
                const textarea = document.createElement('textarea');
                textarea.value = text;
                document.body.appendChild(textarea);
                textarea.select();
                try {
                    document.execCommand('copy');
                    btn.classList.add('copied');
                    btn.innerHTML = '<i class="fas fa-check"></i> 已复制';
                    setTimeout(() => {
                        btn.classList.remove('copied');
                        btn.innerHTML = '<i class="fas fa-copy"></i> 复制';
                    }, 2000);
                } catch (err) {
                    alert('复制失败，请手动复制: ' + text);
                }
                document.body.removeChild(textarea);
            }

            // 辅助功能
            function randomCommand() {
                const cards = document.querySelectorAll('.command-card');
                if (cards.length === 0) return;
                const randomIndex = Math.floor(Math.random() * cards.length);
                const card = cards[randomIndex];
                card.scrollIntoView({ behavior: 'smooth', block: 'center' });
                card.classList.add('highlight-flash');
                setTimeout(() => {
                    card.classList.remove('highlight-flash');
                }, 4000);
            }

            function expandAll() {
                document.querySelectorAll('.command-card .detail-box').forEach(box => {
                    box.classList.add('open');
                });
                document.querySelectorAll('.toggle-detail').forEach(btn => {
                    btn.innerHTML = '<i class="fas fa-chevron-down open"></i> 收起';
                });
            }

            function collapseAll() {
                document.querySelectorAll('.command-card .detail-box').forEach(box => {
                    box.classList.remove('open');
                });
                document.querySelectorAll('.toggle-detail').forEach(btn => {
                    btn.innerHTML = '<i class="fas fa-chevron-down"></i> 详情';
                });
            }

            // 事件绑定
            btnJava.addEventListener('click', function() {
                currentVersion = 'java';
                this.classList.add('active-java');
                this.classList.remove('active-netease');
                btnNetease.classList.remove('active-java', 'active-netease');
                render();
            });

            btnNetease.addEventListener('click', function() {
                currentVersion = 'netease';
                this.classList.add('active-netease');
                this.classList.remove('active-java');
                btnJava.classList.remove('active-netease', 'active-java');
                render();
            });

            levelBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    levelBtns.forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    currentLevel = this.getAttribute('data-level');
                    render();
                });
            });

            searchInput.addEventListener('input', function() {
                searchTerm = this.value;
                render();
            });

            clearSearch.addEventListener('click', function() {
                searchInput.value = '';
                searchTerm = '';
                render();
            });

            randomBtn.addEventListener('click', randomCommand);
            expandAllBtn.addEventListener('click', expandAll);
            collapseAllBtn.addEventListener('click', collapseAll);

            // 初始化
            btnJava.classList.add('active-java');
            document.querySelector('[data-level="all"]').classList.add('active');
            render();

            console.log(`✅ MC 指令大师已启动！ 共 ${commands.length} 条指令，高阶占比显著提升。`);
        })();
    </script>

</body>
</html>
