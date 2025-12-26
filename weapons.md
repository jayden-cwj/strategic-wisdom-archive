---
layout: default
title: "Weapons Arsenal"
permalink: /weapons/
---

<div class="dashboard container">
    <div class="dashboard-header">
        <h1 lang="en">Weapons Arsenal</h1>
        <h1 lang="ko" style="display:none;">무기 목록</h1>
        <p class="subtitle" lang="en">Comprehensive archive of historical military weapons</p>
        <p class="subtitle" lang="ko" style="display:none;">역사적 군사 무기의 종합 아카이브</p>
    </div>

    <section class="collection-section">
        <h2 lang="en">All Weapons</h2>
        <h2 lang="ko" style="display:none;">모든 무기</h2>
        <div class="grid-container">
            {% for weapon in site.weapons %}
            <a href="{{ weapon.url | relative_url }}" class="item-card">
                <div class="card-image">
                    {% if weapon.thumbnail %}
                    <img src="{{ weapon.thumbnail | relative_url }}" alt="{{ weapon.title_en }}">
                    {% else %}
                    <svg width="400" height="300" xmlns="http://www.w3.org/2000/svg">
                        <rect width="400" height="300" fill="#2c3e50"/>
                        <text x="200" y="150" font-family="Arial" font-size="24" fill="#ecf0f1" text-anchor="middle" font-weight="bold">{{ weapon.title_en }}</text>
                    </svg>
                    {% endif %}
                </div>
                <div class="card-content">
                    <h3 class="card-title-en">{{ weapon.title_en }}</h3>
                    <p class="card-title-ko">{{ weapon.title_ko }}</p>
                    <p class="card-summary" lang="en">{{ weapon.summary_en }}</p>
                    <p class="card-summary" lang="ko" style="display:none;">{{ weapon.summary_ko }}</p>
                </div>
            </a>
            {% endfor %}
        </div>
    </section>
</div>
