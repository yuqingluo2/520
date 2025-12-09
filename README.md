<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>校园美食智能体</title>
    <!-- 引入字体图标（美食相关图标） -->
    <link rel="stylesheet" href="https://cdn.bootcdn.net/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- 引入扣子Chat SDK -->
    <script src="https://lf-cdn.coze.cn/obj/unpkg/flow-platform/chat-app-sdk/1.2.0-beta.19/libs/cn/index.js"></script>
    <style>
        /* 全局样式重置 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Inter", "微软雅黑", Arial, sans-serif;
        }
        /* 渐变背景+美食装饰元素 */
        body {
            height: 100vh;
            background: linear-gradient(135deg, #fdf2f8 0%, #fef7fb 50%, #f0f8fb 100%);
            position: relative;
            overflow-x: hidden;
        }
        /* 装饰性美食图标（悬浮在背景） */
        .decor-icon {
            position: absolute;
            opacity: 0.1;
            font-size: 120px;
            color: #ed8936;
            z-index: 0;
        }
        .icon-1 { top: 10%; left: 5%; transform: rotate(-15deg); }
        .icon-2 { top: 30%; right: 8%; transform: rotate(20deg); }
        .icon-3 { bottom: 15%; left: 15%; transform: rotate(-10deg); }
        .icon-4 { bottom: 25%; right: 12%; transform: rotate(15deg); }
        /* 页面主体容器 */
        .container {
            position: relative;
            z-index: 1;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
        }
        /* 标题区域样式 */
        .header {
            margin-bottom: 40px;
            animation: fadeIn 1s ease-in-out;
        }
        .header h1 {
            font-size: 3rem;
            color: #2d3748;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        .header h1 i {
            color: #ed8936;
            animation: bounce 2s infinite ease-in-out;
        }
        .header p {
            font-size: 1.2rem;
            color: #4a5568;
            max-width: 600px;
            line-height: 1.6;
        }
        /* 功能卡片区域（新增，展示智能体核心功能） */
        .feature-cards {
            display: flex;
            gap: 25px;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 60px;
            width: 100%;
            animation: fadeUp 1.2s ease-in-out;
        }
        .card {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(10px);
            border-radius: 16px;
            padding: 30px;
            width: 280px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.08);
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.5);
        }
        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.12);
            border-color: #ed8936;
        }
        .card i {
            font-size: 2.5rem;
            color: #ed8936;
            margin-bottom: 20px;
        }
        .card h3 {
            font-size: 1.3rem;
            color: #2d3748;
            margin-bottom: 12px;
        }
        .card p {
            color: #718096;
            font-size: 0.95rem;
            line-height: 1.5;
        }
        /* 悬浮按钮样式优化 */
        .coze-web-chat-container {
            position: fixed !important;
            right: 30px !important;
            bottom: 60px !important;
            z-index: 9999 !important;
            transition: all 0.3s ease !important;
        }
        .coze-web-chat-container:hover {
            transform: scale(1.05) !important;
        }
        /* 聊天框样式自定义（通过SDK配置） */
        .coze-chat-header {
            background-color: #ed8936 !important;
            color: white !important;
        }
        /* 动画效果 */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        @keyframes fadeUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        @keyframes bounce {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }
        /* 响应式适配（手机/平板） */
        @media (max-width: 768px) {
            .header h1 { font-size: 2.2rem; }
            .feature-cards { gap: 20px; }
            .card { width: 100%; max-width: 320px; }
            .coze-web-chat-container {
                right: 20px !important;
                bottom: 40px !important;
            }
        }
    </style>
</head>
<body>
    <!-- 背景装饰图标 -->
    <i class="fas fa-utensils decor-icon icon-1"></i>
    <i class="fas fa-burger decor-icon icon-2"></i>
    <i class="fas fa-pizza-slice decor-icon icon-3"></i>
    <i class="fas fa-ice-cream decor-icon icon-4"></i>

    <!-- 页面主体内容 -->
    <div class="container">
        <!-- 标题区域 -->
        <div class="header">
            <h1><i class="fas fa-utensils"></i>校园美食智能体</h1>
            <p>一站式解决食堂推荐、菜品答疑、宿舍快手菜、饮食避坑，让校园干饭更省心！</p >
        </div>

        <!-- 功能卡片区域 -->
        <div class="feature-cards">
            <div class="card">
                <i class="fas fa-clipboard-check"></i>
                <h3>食堂精准推荐</h3>
                <p>按校区、预算、口味推荐菜品+窗口，避开排队高峰</p >
            </div>
            <div class="card">
                <i class="fas fa-question-circle"></i>
                <h3>菜品在线答疑</h3>
                <p>查询成分、营业时间、隐藏吃法，解决信息差</p >
            </div>
            <div class="card">
                <i class="fas fa-fire"></i>
                <h3>宿舍快手菜</h3>
                <p>电煮锅/微波炉就能做，5步搞定美味</p >
            </div>
        </div>
    </div>

    <!-- 扣子智能体嵌入代码（已填入你的令牌和智能体ID） -->
    <script>
        new CozeWebSDK.WebChatClient({
            config: {
                bot_id: '7580561731966402596', // 你的智能体ID
            },
            componentProps: {
                title: '校园美食智能体', // 聊天框标题
                icon: 'https://lf3-cdn-tos.bytecdntp.com/cdn/expire-100-M/coze-icon/64x64.png', // 聊天框图标
                theme: {
                    primaryColor: '#ed8936', // 主题色（橙色，贴合美食场景）
                    backgroundColor: '#ffffff',
                    textColor: '#2d3748'
                }
            },
            auth: {
                type: 'token',
                token: 'pat_xzxhDcBpZpjtFo9I2IxVuWoVdm6ylxBu5IuFmcO2c6DksGODHe4h2XuQzwv85Ysq', // 你的个人令牌
                onRefreshToken: function () {
                    return 'pat_xzxhDcBpZpjtFo9I2IxVuWoVdm6ylxBu5IuFmcO2c6DksGODHe4h2XuQzwv85Ysq';
                }
            }
        });
    </script>
</body>
</html>
