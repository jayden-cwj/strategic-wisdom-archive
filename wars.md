---
layout: default
title: "Historical Conflicts"
permalink: /wars/
---

<div class="dashboard container">
    <div class="dashboard-header">
        <h1 lang="en">Historical Conflicts</h1>
        <h1 lang="ko" style="display:none;">역사적 전쟁</h1>
        <p class="subtitle" lang="en">Comprehensive archive of major military conflicts throughout history</p>
        <p class="subtitle" lang="ko" style="display:none;">역사상 주요 군사 분쟁의 종합 아카이브</p>
    </div>

    <section class="collection-section">
        <h2 lang="en">All Wars</h2>
        <h2 lang="ko" style="display:none;">모든 전쟁</h2>
        <div class="grid-container">
            {% for war in site.wars %}
            <a href="{{ war.url | relative_url }}" class="item-card">
                <div class="card-image">
                    {% if war.thumbnail %}
                    <img src="{{ war.thumbnail | relative_url }}" alt="{{ war.title_en }}">
                    {% else %}
                    <svg width="400" height="300" xmlns="http://www.w3.org/2000/svg">
                        <rect width="400" height="300" fill="#1a252f"/>
                        <text x="200" y="150" font-family="Arial" font-size="24" fill="#ecf0f1" text-anchor="middle" font-weight="bold">{{ war.title_en }}</text>
                    </svg>
                    {% endif %}
                </div>
                <div class="card-content">
                    <h3 class="card-title-en">{{ war.title_en }}</h3>
                    <p class="card-title-ko">{{ war.title_ko }}</p>
                    <p class="card-summary" lang="en">{{ war.summary_en }}</p>
                    <p class="card-summary" lang="ko" style="display:none;">{{ war.summary_ko }}</p>
                </div>
            </a>
            {% endfor %}
        </div>
    </section>
</div>
