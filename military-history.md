---
layout: default
title: Military History
permalink: /military-history/
---

<div class="military-history-page container">
    <!-- Page Header -->
    
    <!-- Introduction -->
    <!-- Era-Based Organization -->
    <div class="historical-timeline">
        <p>
        <!-- Era Filter -->
        <div class="era-filter-container">
            <label class="filter-label lang-en-only">Filter by Era:</label>
            <label class="filter-label lang-ko-only">시대별 필터:</label>
            <div class="era-filter-buttons">
                <button class="era-filter-btn active" data-era="all">
                    <span class="lang-en-only">All Eras</span>
                    <span class="lang-ko-only">모든 시대</span>
                </button>
                <button class="era-filter-btn" data-era="ancient">
                    <span class="lang-en-only">Ancient</span>
                    <span class="lang-ko-only">고대</span>
                </button>
                <button class="era-filter-btn" data-era="medieval">
                    <span class="lang-en-only">Medieval</span>
                    <span class="lang-ko-only">중세</span>
                </button>
                <button class="era-filter-btn" data-era="modern">
                    <span class="lang-en-only">Modern</span>
                    <span class="lang-ko-only">근대</span>
                </button>
                <button class="era-filter-btn" data-era="contemporary">
                    <span class="lang-en-only">Contemporary</span>
                    <span class="lang-ko-only">현대</span>
                </button>
            </div>
        </div>

        {% assign all_wars = site.wars | sort: 'year' %}
        {% assign eras = "ancient,medieval,modern,contemporary,future,scifi,fantasy" | split: "," %}

        {% for era in eras %}
            {% assign era_wars = all_wars | where: "era", era %}
            {% if era_wars.size > 0 %}
            <div class="era-section">
                <h3 class="era-title">
                    {% if era == "ancient" %}
                        <span class="lang-en-only">🏛️ Ancient Era (Before 500 CE)</span>
                        <span class="lang-ko-only">🏛️ 고대 (500년 이전)</span>
                    {% elsif era == "medieval" %}
                        <span class="lang-en-only">🏰 Medieval Era (500-1500)</span>
                        <span class="lang-ko-only">🏰 중세 (500-1500년)</span>
                    {% elsif era == "modern" %}
                        <span class="lang-en-only">⚔️ Modern Era (1500-1900)</span>
                        <span class="lang-ko-only">⚔️ 근대 (1500-1900년)</span>
                    {% elsif era == "contemporary" %}
                        <span class="lang-en-only">🛡️ Contemporary Era (1900-Present)</span>
                        <span class="lang-ko-only">🛡️ 현대 (1900년-현재)</span>
                    {% elsif era == "future" %}
                        <span class="lang-en-only">🔮 Future Concepts</span>
                        <span class="lang-ko-only">🔮 미래 개념</span>
                    {% elsif era == "scifi" %}
                        <span class="lang-en-only">🚀 Science Fiction</span>
                        <span class="lang-ko-only">🚀 공상과학</span>
                    {% elsif era == "fantasy" %}
                        <span class="lang-en-only">🐉 Fantasy Settings</span>
                        <span class="lang-ko-only">🐉 판타지</span>
                    {% endif %}
                    <span class="entry-count">({{ era_wars.size }} wars)</span>
                </h3>

                <div class="era-entries">
                    {% for war in era_wars %}
                    <a href="{{ war.url | relative_url }}" class="history-entry-card war-card">
                        <div class="entry-type">
                            <span class="type-badge war-badge lang-en-only">War / Conflict</span>
                            <span class="type-badge war-badge lang-ko-only">전쟁 / 분쟁</span>
                        </div>
                        <h4 class="entry-title">
                            <span class="lang-en-only">{{ war.title_en }}</span>
                            <span class="lang-ko-only">{{ war.title_ko }}</span>
                        </h4>
                        <p class="entry-summary">
                            <span class="lang-en-only">{{ war.summary_en | truncate: 120 }}</span>
                            <span class="lang-ko-only">{{ war.summary_ko | truncate: 120 }}</span>
                        </p>
                        {% if war.war_info.period_en %}
                        <div class="entry-year">
                            <span class="lang-en-only">{{ war.war_info.period_en }}</span>
                            <span class="lang-ko-only">{{ war.war_info.period_ko }}</span>
                        </div>
                        {% endif %}
                    </a>
                    {% endfor %}
                </div>
            </div>
            {% endif %}
        {% endfor %}
    </div>

    <!-- Quick Navigation -->
    <div class="quick-navigation">
        <h2 class="lang-en-only">Explore by Category</h2>
        <h2 class="lang-ko-only">카테고리별 탐색</h2>

        <div class="nav-cards">
            <a href="{{ '/fortifications/' | relative_url }}" class="nav-card fortifications-card">
                <div class="nav-icon">🏰</div>
                <h3 class="lang-en-only">Defense Structures</h3>
                <h3 class="lang-ko-only">방어 구조</h3>
                <p class="lang-en-only">Fortifications, walls, and defensive architecture</p>
                <p class="lang-ko-only">요새, 성벽 및 방어 건축</p>
                <div class="nav-count">{{ site.fortifications.size }} entries</div>
            </a>

            <a href="{{ '/strategies/' | relative_url }}" class="nav-card strategies-card">
                <div class="nav-icon">⚔️</div>
                <h3 class="lang-en-only">Strategic Systems</h3>
                <h3 class="lang-ko-only">전략 시스템</h3>
                <p class="lang-en-only">Tactical innovations and defensive strategies</p>
                <p class="lang-ko-only">전술적 혁신과 방어 전략</p>
                <div class="nav-count">{{ site.strategies.size }} entries</div>
            </a>
        </div>
    </div>
</div>

<style>
/* Military History Page Styles */
.military-history-page {
    padding: 2rem 0;
}

.page-header {
    text-align: center;
    padding: 3rem 0 2rem;
    background: linear-gradient(180deg, #1a252f 0%, #0f1419 100%);
    margin-bottom: 3rem;
    border-radius: 12px;
}

.page-header h1 {
    font-size: 3rem;
    color: #3498db;
    text-transform: uppercase;
    letter-spacing: 3px;
    margin-bottom: 1rem;
}

.page-subtitle {
    color: #95a5a6;
    font-size: 1.2rem;
    max-width: 800px;
    margin: 0 auto;
}

/* Archive Statistics */
.archive-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem;
    margin-bottom: 3rem;
}

.stat-card {
    background: linear-gradient(135deg, #1a252f 0%, #2c3e50 100%);
    padding: 2rem;
    border-radius: 12px;
    text-align: center;
    border: 2px solid #34495e;
    transition: all 0.3s ease;
}

.stat-card:hover {
    border-color: #3498db;
    transform: translateY(-5px);
    box-shadow: 0 8px 16px rgba(52, 152, 219, 0.3);
}

.stat-number {
    font-size: 3rem;
    font-weight: 700;
    color: #3498db;
    margin-bottom: 0.5rem;
}

.stat-label {
    color: #95a5a6;
    font-size: 1rem;
    text-transform: uppercase;
    letter-spacing: 1px;
}

/* Introduction */
.archive-introduction {
    background: linear-gradient(135deg, #34495e15, #2c3e5015);
    padding: 2rem;
    border-radius: 12px;
    margin-bottom: 3rem;
    border-left: 4px solid #3498db;
}

.archive-introduction h2 {
    color: #3498db;
    font-size: 2rem;
    margin-bottom: 1rem;
}

.archive-introduction p {
    color: #bdc3c7;
    font-size: 1.1rem;
    line-height: 1.8;
}

/* Historical Timeline */
.historical-timeline {
    margin-bottom: 3rem;
}

.historical-timeline > h2 {
    color: #3498db;
    font-size: 2.5rem;
    margin-bottom: 2rem;
    text-align: center;
    text-transform: uppercase;
    letter-spacing: 2px;
}

/* Era Filter */
.era-filter-container {
    background: linear-gradient(135deg, #34495e15, #2c3e5015);
    padding: 1.5rem 2rem;
    border-radius: 12px;
    margin-bottom: 2.5rem;
    border: 2px solid #34495e;
}

.filter-label {
    display: block;
    color: #3498db;
    font-size: 1.1rem;
    font-weight: 600;
    margin-bottom: 1rem;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.era-filter-buttons {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem;
}

.era-filter-btn {
    background: linear-gradient(135deg, #1a252f 0%, #2c3e50 100%);
    border: 2px solid #34495e;
    border-radius: 25px;
    padding: 0.75rem 1.5rem;
    color: #95a5a6;
    font-size: 0.95rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    cursor: pointer;
    transition: all 0.3s ease;
}

.era-filter-btn:hover {
    border-color: #3498db;
    color: #3498db;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(52, 152, 219, 0.3);
}

.era-filter-btn.active {
    background: linear-gradient(135deg, #3498db, #2980b9);
    border-color: #3498db;
    color: #fff;
    box-shadow: 0 4px 12px rgba(52, 152, 219, 0.4);
}

.era-section {
    margin-bottom: 3rem;
    transition: opacity 0.3s ease, max-height 0.3s ease;
}

.era-section.hidden {
    display: none;
}

.era-title {
    color: #5dade2;
    font-size: 1.8rem;
    margin-bottom: 1.5rem;
    padding-bottom: 0.5rem;
    border-bottom: 2px solid #34495e;
}

.entry-count {
    color: #95a5a6;
    font-size: 1rem;
    font-weight: normal;
    margin-left: 0.5rem;
}

.era-entries {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1.5rem;
}

.history-entry-card {
    background: linear-gradient(135deg, #1a252f 0%, #2c3e50 100%);
    border-radius: 8px;
    padding: 1.5rem;
    text-decoration: none;
    color: inherit;
    border: 2px solid #34495e;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
}

.history-entry-card:hover {
    transform: translateY(-5px);
    border-color: #3498db;
    box-shadow: 0 8px 16px rgba(52, 152, 219, 0.3);
}

.entry-type {
    margin-bottom: 0.75rem;
}

.type-badge {
    display: inline-block;
    padding: 0.25rem 0.75rem;
    border-radius: 15px;
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.fortification-badge {
    background: linear-gradient(135deg, #3498db, #2980b9);
    color: #fff;
}

.strategy-badge {
    background: linear-gradient(135deg, #9b59b6, #8e44ad);
    color: #fff;
}

.war-badge {
    background: linear-gradient(135deg, #e74c3c, #c0392b);
    color: #fff;
}

.entry-title {
    color: #3498db;
    font-size: 1.3rem;
    margin-bottom: 0.75rem;
}

.entry-summary {
    color: #bdc3c7;
    font-size: 0.9rem;
    line-height: 1.5;
    flex-grow: 1;
    margin-bottom: 0.75rem;
}

.entry-year {
    color: #95a5a6;
    font-size: 0.85rem;
    font-style: italic;
    border-top: 1px solid #34495e;
    padding-top: 0.5rem;
    margin-top: 0.5rem;
}

/* Quick Navigation */
.quick-navigation {
    margin-top: 4rem;
}

.quick-navigation > h2 {
    color: #3498db;
    font-size: 2rem;
    margin-bottom: 2rem;
    text-align: center;
    text-transform: uppercase;
    letter-spacing: 2px;
}

.nav-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
}

.nav-card {
    background: linear-gradient(135deg, #1a252f 0%, #2c3e50 100%);
    border-radius: 12px;
    padding: 2.5rem;
    text-decoration: none;
    color: inherit;
    border: 2px solid #34495e;
    transition: all 0.3s ease;
    text-align: center;
}

.nav-card:hover {
    transform: translateY(-8px);
    border-color: #3498db;
    box-shadow: 0 12px 24px rgba(52, 152, 219, 0.4);
}

.nav-icon {
    font-size: 4rem;
    margin-bottom: 1rem;
}

.nav-card h3 {
    color: #3498db;
    font-size: 1.5rem;
    margin-bottom: 0.75rem;
}

.nav-card p {
    color: #bdc3c7;
    font-size: 1rem;
    margin-bottom: 1rem;
}

.nav-count {
    color: #95a5a6;
    font-size: 0.9rem;
    font-style: italic;
}

/* Responsive Design */
@media (max-width: 768px) {
    .page-header h1 {
        font-size: 2rem;
    }

    .page-subtitle {
        font-size: 1rem;
    }

    .era-entries {
        grid-template-columns: 1fr;
    }

    .nav-cards {
        grid-template-columns: 1fr;
    }

    .era-filter-buttons {
        gap: 0.5rem;
    }

    .era-filter-btn {
        padding: 0.5rem 1rem;
        font-size: 0.85rem;
    }
}
</style>

<script>
// Era Filter Functionality
document.addEventListener('DOMContentLoaded', function() {
    const filterButtons = document.querySelectorAll('.era-filter-btn');
    const eraSections = document.querySelectorAll('.era-section');

    // Add click event to each filter button
    filterButtons.forEach(button => {
        button.addEventListener('click', function() {
            const selectedEra = this.dataset.era;

            // Update active button state
            filterButtons.forEach(btn => btn.classList.remove('active'));
            this.classList.add('active');

            // Show/hide era sections based on filter
            eraSections.forEach(section => {
                const sectionEra = section.querySelector('.era-title').textContent.toLowerCase();

                if (selectedEra === 'all') {
                    section.classList.remove('hidden');
                } else {
                    // Match the era with the section
                    if (selectedEra === 'ancient' && sectionEra.includes('ancient') || sectionEra.includes('고대')) {
                        section.classList.remove('hidden');
                    } else if (selectedEra === 'medieval' && (sectionEra.includes('medieval') || sectionEra.includes('중세'))) {
                        section.classList.remove('hidden');
                    } else if (selectedEra === 'modern' && (sectionEra.includes('modern') || sectionEra.includes('근대'))) {
                        section.classList.remove('hidden');
                    } else if (selectedEra === 'contemporary' && (sectionEra.includes('contemporary') || sectionEra.includes('현대'))) {
                        section.classList.remove('hidden');
                    } else if (selectedEra === 'future' && (sectionEra.includes('future') || sectionEra.includes('미래'))) {
                        section.classList.remove('hidden');
                    } else if (selectedEra === 'scifi' && (sectionEra.includes('science fiction') || sectionEra.includes('공상과학'))) {
                        section.classList.remove('hidden');
                    } else if (selectedEra === 'fantasy' && (sectionEra.includes('fantasy') || sectionEra.includes('판타지'))) {
                        section.classList.remove('hidden');
                    } else {
                        section.classList.add('hidden');
                    }
                }
            });

            // Scroll to timeline section smoothly
            document.querySelector('.historical-timeline').scrollIntoView({
                behavior: 'smooth',
                block: 'start'
            });
        });
    });
});
</script>
