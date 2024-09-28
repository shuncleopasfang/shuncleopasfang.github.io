---
layout: page
title: Articles
permalink: /articles/
---

<style>
        .article-list {
            width: 100%;
            max-width: 800px;
            margin: 0 auto;
            padding: 0 20px;
            box-sizing: border-box;
        }
        .article-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding: 10px 0;
            border-bottom: 1px solid #eee;
        }
        .article-info {
            flex-grow: 1;
            padding-right: 20px;
        }
        .article-date {
            font-size: 0.9em;
            color: #666;
        }
        .article-title {
            font-size: 1.0em;
            text-decoration: none;
            color: #333;
            word-wrap: break-word;
        }
        
        .article-image-container {
            width: 60px;
            height: 60px;
            flex-shrink: 0;
            overflow: hidden;
            border-radius: 50%;
        }

        .article-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.3s ease;
        }

        .article-image:hover {
            transform: scale(1.1);
        }
    </style>
</head>
<body>
    <div class="article-list">
        <div class="article-item">
            <div class="article-info">
                <span class="article-date">Jan 19, 2024</span><br>
                <a href="https://shuncleopasfang.blogspot.com/2023/11/taiwan-travelogue.html" class="article-title">從天黑走到天亮——方順的台灣日記</a>
            </div>
            <div class="article-image-container">
                <img src="/assets/images/ko_wen-je_&_juntaro_ogata.jpeg" alt="ko_wen-je_&_juntaro_ogata" class="article-image">
            </div>
        </div>
        
        <!-- 其他文章項目... -->
    </div>

    <script>
    document.addEventListener('DOMContentLoaded', () => {
        const images = document.querySelectorAll('.article-image');
        
        images.forEach(img => {
            img.addEventListener('mouseenter', () => {
                img.style.transform = 'scale(1.1)';
            });
            
            img.addEventListener('mouseleave', () => {
                img.style.transform = 'scale(1)';
            });
        });
    });
    </script>
