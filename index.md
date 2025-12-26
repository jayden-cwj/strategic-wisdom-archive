---
layout: default
title: "Global Arsenal Archive - Dashboard"
---

<div class="dashboard container">
    <div class="dashboard-header">
        <h1>Global Arsenal Archive</h1>
        <p class="subtitle">A data-driven platform archiving global military history and weapon specifications</p>
    </div>

    <!-- Weapons Section -->
    <section class="collection-section">
        <h2>Weapons Arsenal</h2>
        <div class="grid-container">
            {% for weapon in site.weapons %}
            <a href="{{ weapon.url | relative_url }}" class="item-card">
                <div class="card-image">
                    <img src="{{ weapon.url | relative_url }}{{ weapon.thumbnail }}" alt="{{ weapon.title_en }}">
                </div>
                <div class="card-content">
                    <h3 class="card-title-en">{{ weapon.title_en }}</h3>
                    <p class="card-title-ko">{{ weapon.title_ko }}</p>
                    <p class="card-summary">{{ weapon.summary_en }}</p>
                </div>
            </a>
            {% endfor %}
        </div>
    </section>

    <!-- Wars Section -->
    <section class="collection-section">
        <h2>Historical Conflicts</h2>
        <div class="grid-container">
            {% for war in site.wars %}
            <a href="{{ war.url | relative_url }}" class="item-card">
                <div class="card-image">
                    <img src="{{ war.url | relative_url }}{{ war.thumbnail }}" alt="{{ war.title_en }}">
                </div>
                <div class="card-content">
                    <h3 class="card-title-en">{{ war.title_en }}</h3>
                    <p class="card-title-ko">{{ war.title_ko }}</p>
                    <p class="card-summary">{{ war.summary_en }}</p>
                </div>
            </a>
            {% endfor %}
        </div>
    </section>
</div>
