---
layout: default
title_en: "Fortifications"
title_ko: "방어 구조"
permalink: /fortifications/
---

<div class="dashboard container">

    
    <div class="collection-filters">
        <div class="filter-group">
            <label class="lang-en-only">Filter by Era:</label>
            <label class="lang-ko-only">시대별 필터:</label>
            <select id="era-filter" class="filter-select">
                <option value="all" data-en="All Eras" data-ko="모든 시대">All Eras / 모든 시대</option>
                <option value="ancient" data-en="Ancient (Before 500 CE)" data-ko="고대 (500년 이전)">Ancient / 고대</option>
                <option value="medieval" data-en="Medieval (500-1500)" data-ko="중세 (500-1500)">Medieval / 중세</option>
                <option value="modern" data-en="Modern (1500-1900)" data-ko="근대 (1500-1900)">Modern / 근대</option>
                <option value="contemporary" data-en="Contemporary (1900-Present)" data-ko="현대 (1900-현재)">Contemporary / 현대</option>
                <option value="future" data-en="Future Concepts" data-ko="미래 개념">Future / 미래</option>
                <option value="scifi" data-en="Science Fiction" data-ko="공상 과학">Sci-Fi / SF</option>
                <option value="fantasy" data-en="Fantasy" data-ko="판타지">Fantasy / 판타지</option>
            </select>
        </div>

        <div class="filter-group">
            <label class="lang-en-only">War History:</label>
            <label class="lang-ko-only">전쟁 역사:</label>
            <select id="war-filter" class="filter-select">
                <option value="all" data-en="All Wars" data-ko="모든 전쟁">All Wars / 모든 전쟁</option>
                {% assign sorted_wars = site.wars | sort: 'year' %}
                {% for war in sorted_wars %}
                <option value="{{ war.url | relative_url }}" data-en="{{ war.title_en }}" data-ko="{{ war.title_ko }}">
                    <span class="lang-en-only">{{ war.title_en }}</span>
                    <span class="lang-ko-only">{{ war.title_ko }}</span>
                </option>
                {% endfor %}
            </select>
        </div>

        <div class="filter-group">
            <label class="lang-en-only">Sort by:</label>
            <label class="lang-ko-only">정렬:</label>
            <select id="sort-select" class="filter-select">
                <option value="name-asc" data-en="Name (A-Z)" data-ko="이름 (가-하)">Name (A-Z) / 이름</option>
                <option value="name-desc" data-en="Name (Z-A)" data-ko="이름 (하-가)">Name (Z-A) / 이름 역순</option>
                <option value="year-asc" data-en="Year (Oldest First)" data-ko="연도 (오래된 순)">Year (Oldest) / 연도 (오래된 순)</option>
                <option value="year-desc" data-en="Year (Newest First)" data-ko="연도 (최신 순)">Year (Newest) / 연도 (최신 순)</option>
                <option value="deterrence-desc" data-en="Deterrence (High-Low)" data-ko="억지력 (높음-낮음)">Deterrence / 억지력</option>
            </select>
        </div>

        <div class="results-count">
            <span id="count-display" class="lang-en-only">Showing all items</span>
            <span id="count-display-ko" class="lang-ko-only">모든 항목 표시</span>
        </div>
    </div>

    <section class="collection-section">
        <div class="grid-container" id="fortifications-grid">
            {% for fort in site.fortifications %}
            <a href="{{ fort.url | relative_url }}"
               class="item-card"
               data-era="{{ fort.era | default: 'ancient' }}"
               data-year="{{ fort.year | default: 0 }}"
               data-name-en="{{ fort.title_en | downcase }}"
               data-name-ko="{{ fort.title_ko }}"
               data-deterrence="{{ fort.metrics.deterrence_level | default: 0 }}">
                <div class="card-image">
                    {% if fort.thumbnail %}
                    <img src="{{ fort.thumbnail | relative_url }}" alt="{{ fort.title_en }}">
                    {% else %}
                    <div class="placeholder-image fortification-placeholder">
                        <span class="placeholder-icon">🏰</span>
                        <span class="placeholder-text lang-en-only">{{ fort.title_en }}</span>
                        <span class="placeholder-text lang-ko-only">{{ fort.title_ko }}</span>
                    </div>
                    {% endif %}
                </div>
                <div class="card-content">
                    <h3 class="card-title-en lang-en-only">{{ fort.title_en }}</h3>
                    <p class="card-title-ko lang-ko-only">{{ fort.title_ko }}</p>
                    <p class="card-summary lang-en-only">{{ fort.summary_en }}</p>
                    <p class="card-summary lang-ko-only">{{ fort.summary_ko }}</p>
                    {% if fort.metrics %}
                    <div class="card-metrics">
                        <span class="metric-badge" title="Deterrence">
                            🛡️ {{ fort.metrics.deterrence_level | default: "N/A" }}
                        </span>
                        <span class="metric-badge" title="Communication">
                            📡 {{ fort.metrics.communication_efficiency | default: "N/A" }}
                        </span>
                    </div>
                    {% endif %}
                </div>
            </a>
            {% endfor %}

            {% if site.fortifications.size == 0 %}
            <div class="empty-state">
                <p class="lang-en-only">No fortifications in the archive yet. Check back soon!</p>
                <p class="lang-ko-only">아카이브에 아직 요새가 없습니다. 곧 다시 확인하세요!</p>
            </div>
            {% endif %}
        </div>
    </section>
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    const grid = document.getElementById('fortifications-grid');
    const eraFilter = document.getElementById('era-filter');
    const warFilter = document.getElementById('war-filter');
    const sortSelect = document.getElementById('sort-select');
    const cards = Array.from(grid.querySelectorAll('.item-card'));

    // War filter navigation
    warFilter.addEventListener('change', function() {
        const selectedWar = this.value;
        if (selectedWar !== 'all') {
            window.location.href = selectedWar;
        }
    });

    function filterAndSort() {
        const selectedEra = eraFilter.value;
        const sortMethod = sortSelect.value;

        // Filter cards
        let visibleCards = cards.filter(card => {
            if (selectedEra === 'all') return true;
            return card.dataset.era === selectedEra;
        });

        // Sort cards
        visibleCards.sort((a, b) => {
            switch (sortMethod) {
                case 'name-asc':
                    return a.dataset.nameEn.localeCompare(b.dataset.nameEn);
                case 'name-desc':
                    return b.dataset.nameEn.localeCompare(a.dataset.nameEn);
                case 'year-asc':
                    return parseInt(a.dataset.year) - parseInt(b.dataset.year);
                case 'year-desc':
                    return parseInt(b.dataset.year) - parseInt(a.dataset.year);
                case 'deterrence-desc':
                    return parseInt(b.dataset.deterrence) - parseInt(a.dataset.deterrence);
                default:
                    return 0;
            }
        });

        // Hide all cards first
        cards.forEach(card => card.style.display = 'none');

        // Show and reorder visible cards
        visibleCards.forEach((card, index) => {
            card.style.display = 'flex';
            card.style.order = index;
        });

        // Update count
        const count = visibleCards.length;
        document.getElementById('count-display').textContent = `Showing ${count} of ${cards.length} items`;
        document.getElementById('count-display-ko').textContent = `${cards.length}개 중 ${count}개 항목 표시`;
    }

    eraFilter.addEventListener('change', filterAndSort);
    sortSelect.addEventListener('change', filterAndSort);

    // Initial filter
    filterAndSort();
});
</script>

<style>
.collection-filters {
    background: white;
    padding: 1.5rem;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    margin-top: 2rem;
    margin-bottom: 2rem;
    display: flex;
    flex-wrap: wrap;
    gap: 1.5rem;
    align-items: center;
}

.filter-group {
    display: flex;
    align-items: center;
    gap: 0.1rem;
}

.filter-group label {
    font-weight: 600;
    color: #2c3e50;
}

.filter-select {
    padding: 0.5rem 1rem;
    border: 2px solid #ecf0f1;
    border-radius: 8px;
    font-size: 1rem;
    cursor: pointer;
    background: white;
    color: #2c3e50;
    transition: border-color 0.3s ease;
}

.filter-select:hover {
    border-color: #3498db;
}

.filter-select:focus {
    outline: none;
    border-color: #3498db;
}

.results-count {
    margin-left: auto;
    color: #7f8c8d;
    font-size: 0.95rem;
}

.placeholder-image {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 1rem;
}

.placeholder-icon {
    font-size: 4rem;
    margin-bottom: 0.5rem;
}

.placeholder-text {
    font-size: 1.2rem;
    font-weight: 700;
    text-align: center;
}

.card-metrics {
    display: flex;
    gap: 0.5rem;
    margin-top: 0.75rem;
}

.metric-badge {
    background: #ecf0f1;
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    font-size: 0.85rem;
    font-weight: 600;
    color: #34495e;
}

@media (max-width: 768px) {
    .collection-filters {
        flex-direction: column;
        align-items: stretch;
    }

    .filter-group {
        flex-direction: column;
        align-items: stretch;
    }

    .filter-select {
        width: 100%;
    }

    .results-count {
        margin-left: 0;
        text-align: center;
    }
}
</style>
