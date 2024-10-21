---
layout: page
title: 
permalink: /articles/
---

<style>
    .article-list {
        width: 100%;
        max-width: 800px;
        margin: 0 auto;
    }
    .article-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 10px;
        padding: 5px 0;
    }
    .article-info {
        flex-grow: 1;
        padding-right: 10px;
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
        margin-right: 10px; /* Increased right margin */
    }
    .article-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 50%;
        transition: transform 0.3s ease;
    }
    .article-image:hover {
        transform: scale(1.1);
    }
</style>

<div class="article-list">
  <div class="article-item">
    <div class="article-info">
      <span class="article-date">Jan 19, 2024</span><br>
      <a href="https://shuncleopasfang.blogspot.com/2023/11/taiwan-travelogue.html" class="article-title">從天黑走到天亮——方順的台灣日記</a>
    </div>
    <div class="article-image-container">
      <img src="/assets/images/articles/ko_wen-je_&_juntaro_ogata.jpeg" alt="ko_wen-je_&_juntaro_ogata" class="article-image">
    </div>
  </div>
  
  <div class="article-item">
    <div class="article-info">
      <span class="article-date">Aug 10, 2023</span><br>
      <a href="https://shuncleopasfang.blogspot.com/2023/09/aid-education-record-2.html" class="article-title">第二年支教始末记</a>
    </div>
    <div class="article-image-container">
      <img src="/assets/images/articles/aid_education_2.jpg" alt="aid_education_2" class="article-image">
    </div>
  </div>

  <div class="article-item">
    <div class="article-info">
      <span class="article-date">Apr 22, 2023</span><br>
      <a href="https://shuncleopasfang.blogspot.com/2023/05/huangshan-tour.html" class="article-title">黄山游日志</a>
    </div>
    <div class="article-image-container">
      <img src="/assets/images/articles/huangshan_tour.jpg" alt="huangshan_tour" class="article-image">
    </div>
  </div>

  <div class="article-item">
    <div class="article-info">
      <span class="article-date">Jul 17, 2022</span><br>
      <a href="https://shuncleopasfang.blogspot.com/2022/06/aid-education-record.html" class="article-title">支教记闻</a>
    </div>
    <div class="article-image-container">
      <img src="/assets/images/articles/aid_education_1.jpg" alt="aid_education_1" class="article-image">
    </div>
  </div>

  <div class="article-item">
    <div class="article-info">
      <span class="article-date">Jan 2, 2022</span><br>
      <a href="https://shuncleopasfang.blogspot.com/2022/01/50km-Trailwalker-of-Hefei-2022.html" class="article-title">2022合肥50km百里毅行记闻</a>
    </div>
    <div class="article-image-container">
      <img src="/assets/images/articles/50km_trailwalker.jpg" alt="50km_trailwalker" class="article-image">
    </div>
  </div>

  <div class="article-item">
    <div class="article-info">
      <span class="article-date">Dec 9, 2021</span><br>
      <a href="https://shuncleopasfang.blogspot.com/2021/12/hefei-marathon-2021.html" class="article-title">2021合肥马拉松半马心路历程</a>
    </div>
    <div class="article-image-container">
      <img src="/assets/images/articles/hefei_marathon_2021.jpeg" alt="hefei_marathon_2021" class="article-image">
    </div>
  </div>
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
