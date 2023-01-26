---
title: "이것이 코딩 테스트다"
layout: archive
permalink: /Algorithm
author_profile: true
sidebar:
    nav: "docs"
---
<!-- permalink 대소문자 구별 중요! 카테고리 이름 완벽히 똑같이 적어야 함. 다르면 사이트 이상하게 나옴 -->
<!-- site.categories는 딕셔너리 형태 key:카테고리, value:포스트 내용 -->
{% assign posts = site.categories.Algorithm %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}