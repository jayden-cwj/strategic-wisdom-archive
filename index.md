---
layout: default
title: "Global Arsenal Archive - Dashboard"
---

<div class="dashboard container">
    <div class="dashboard-header">
        <h1 lang="en">Global Arsenal Archive</h1>
        <h1 lang="ko" style="display:none;">글로벌 무기 아카이브</h1>
        <p class="subtitle" lang="en">A data-driven platform archiving global military history and weapon specifications</p>
        <p class="subtitle" lang="ko" style="display:none;">전 세계 군사 역사와 무기 사양을 아카이브하는 데이터 기반 플랫폼</p>
    </div>

    <!-- Weapons Section -->
    <section class="collection-section">
        <h2 lang="en">Weapons Arsenal</h2>
        <h2 lang="ko" style="display:none;">무기 목록</h2>
        <div class="grid-container">
            {% for weapon in site.weapons %}
            <a href="{{ weapon.url | relative_url }}" class="item-card">
                <div class="card-image">
                    <img src="{{ weapon.thumbnail | relative_url }}" alt="{{ weapon.title_en }}">
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

    <!-- Wars Section -->
    <section class="collection-section">
        <h2 lang="en">Historical Conflicts</h2>
        <h2 lang="ko" style="display:none;">역사적 전쟁</h2>
        <div class="grid-container">
            {% for war in site.wars %}
            <a href="{{ war.url | relative_url }}" class="item-card">
                <div class="card-image">
                    <img src="{{ war.thumbnail | relative_url }}" alt="{{ war.title_en }}">
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
