---

title: "Building the Audience Intelligence System: Architecture & Design Principles"
toc: true
weight: 10
date: 2026-01-15 
draft: false
categories: ['audience intelligence', 'system design']
tags: ['architecture', 'technical design', 'system design', 'api design']
series: ['Audience Intelligence Implementation']

---

# **Building the Audience Intelligence System: Architecture & Design Principles**

## **Introduction: From Framework to System**

The strategy articles established the **Audience Intelligence Stack**: a conceptual framework with three layers (Strategic Intelligence, Psychographic Intelligence, Activation Intelligence) that work together to transform audience data into strategic decisions.

Now we face the implementation question: **How do you actually build this?**

This article establishes the system architecture that makes audience intelligence operational. We'll map the conceptual framework to concrete components, define clear boundaries between offline preparation and runtime execution, and establish design principles that will guide the rest of the implementation series.

The goal is not just a working system, but a **maintainable, scalable, cost-effective system** that can evolve as new data sources are added and new analytical needs emerge.

---

## **1. The Conceptual Stack Revisited**

Before diving into architecture, let's recall what the Audience Intelligence Stack provides:

**Layer 1: Strategic Intelligence**

- **Question**: Who are we really competing with?
- **Output**: Competitive landscape mapping, overlap metrics (reach, penetration, affinity), quadrant positioning
- **Use cases**: Competitive prioritization, partnership screening, market positioning

**Layer 2: Psychographic Intelligence**

- **Question**: Why do audiences make the choices they do?
- **Output**: Motivational patterns, psychographic segments, cross-category affinity themes, cultural context
- **Use cases**: Message development, brand positioning, content strategy, product development

**Layer 3: Activation Intelligence**

- **Question**: How do we effectively reach and move them?
- **Output**: Influencer recommendations, channel allocations, content strategies, campaign architectures
- **Use cases**: Influencer selection, media planning, content calendar, partnership activation

Each layer builds on the previous one. You can't activate effectively (Layer 3) without understanding motivations (Layer 2), and you can't understand motivations without knowing who you're competing for (Layer 1).

**The implementation challenge**: These layers aren't separate systems. They share data, computations, and insights. The architecture must support this integration while maintaining clear separation of concerns.

---

## **2. System Architecture: Three Tiers**

The conceptual three-layer stack maps to a three-tier technical architecture, but the mapping is not one-to-one. Instead, we organize by **when** and **how** computation happens.

```
┌─────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                         │
│                    (Jobs to Be Done)                         │
├─────────────────┬─────────────────┬─────────────────────────┤
│  Influencer     │  Competitive    │  Content        │ Market │
│  Selection      │  Intelligence   │  Strategy       │ Expand │
└────────┬────────┴────────┬────────┴────────┬────────┴────────┘
         │                 │                 │
         └─────────────────┼─────────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────┐
│                  INTELLIGENCE LAYER                          │
│                    (Runtime Logic)                           │
├──────────────────┬──────────────────┬───────────────────────┤
│  Query Planner   │  LLM Orchestrator│  API Client          │
│  ├ Parse intent  │  ├ Interpret data │  ├ Overlap metrics   │
│  ├ Select matrix │  ├ Generate      │  ├ Affinity scores   │
│  ├ Plan workflow │  │  insights      │  ├ Reach/penetration│
│  └ Route to JTBD │  └ Create reports │  └ Audience queries  │
└────────┬─────────┴────────┬───────────┴──────────┬──────────┘
         │                  │                      │
         └──────────────────┼──────────────────────┘
                            │
┌───────────────────────────▼──────────────────────────────────┐
│                      DATA LAYER                               │
│                  (Offline Preparation)                        │
├─────────────────┬──────────────────┬────────────────────────┤
│  Embeddings     │  Clusters        │  Indices      │ Taxonomy│
│  ├ Text (LLM)   │  ├ Thematic      │  ├ Vector     │ ├ Items │
│  ├ Behavioral   │  ├ Segment       │  │  similarity │ ├ Cats  │
│  ├ Hybrid       │  └ Ecosystem     │  ├ Inverted   │ └ Paths │
│  └ Per-matrix   │                  │  └ Graph      │         │
└──────────────────┴──────────────────┴────────────────────────┘
                            │
                            │
┌───────────────────────────▼──────────────────────────────────┐
│                    RAW DATA SOURCES                           │
│                                                               │
│  Twitter Matrix  │  Instagram Matrix  │  Combined Matrix     │
│  (2M users,      │  (Lookalikes)      │  (TW-IG union)       │
│   100K items)    │                    │                      │
└───────────────────────────────────────────────────────────────┘
```

### **Tier 1: Data Layer (Offline Preparation)**

**Purpose**: Precompute everything that doesn't depend on specific queries.

**Components**:

- **Embeddings**: Vector representations of items (brands, influencers, entities)
    - Text-based: Semantic meaning from descriptions and content
    - Behavioral: Co-occurrence patterns from follow matrices
    - Hybrid: Combined representations
    - Matrix-specific: Separate embeddings for TW, IG, TW-IG
- **Clusters**: Thematic groupings of items
    - Global clusters: Cross-audience patterns (e.g. "Sports Nutrition" category)
    - Segment clusters: Audience-specific patterns (e.g. "Running Ecosystem" for StrideRecover audience)
    - Multi-level: Hierarchical from broad themes to micro-niches
- **Indices**: Fast lookup structures
    - Vector similarity index: Find similar items by embedding distance
    - Inverted index: Map categories to items, items to categories
    - Graph index: Item relationships, similarity networks
- **Taxonomy**: Structured categorization
    - Item → Category mappings
    - Category hierarchies
    - Cross-category relationships

**Key principle**: The Data Layer is **query-independent**. It's computed once (or incrementally updated) and reused across all queries.

### **Tier 2: Intelligence Layer (Runtime Logic)**

**Purpose**: Orchestrate query-specific analysis using precomputed data and external APIs.

**Components**:

- **Query Planner**
    - Parses natural language or structured requests
    - Maps user intent to Jobs to Be Done patterns
    - Selects appropriate matrix (TW, IG, TW-IG) based on JTBD and context
    - Plans workflow: which API calls, which precomputed data, which LLM tasks
    - Routes to appropriate JTBD handler
- **LLM Orchestrator**
    - Interprets raw metrics into strategic insights
    - Generates narrative reports (Executive Summaries, Deep Dives, etc.)
    - Performs thematic labeling and clustering
    - Synthesizes multi-source results
    - Validates outputs against constraints
- **API Client**
    - Manages calls to Audience Intelligence API
    - Handles authentication, rate limiting, retries
    - Caches results to minimize redundant calls
    - Batches requests where possible
    - Returns structured metrics: reach, penetration, affinity, relevance

**Key principle**: The Intelligence Layer is **query-specific**. It combines precomputed data with runtime API calls to answer specific questions.

### **Tier 3: Application Layer (Jobs to Be Done)**

**Purpose**: Implement specific use cases that deliver business value.

**Components**: Each JTBD is a distinct application built on the Intelligence Layer:

- **Influencer Selection**: Find and rank influencers by audience overlap and strategic fit
- **Competitive Intelligence**: Map competitive landscape and identify threats/opportunities
- **Content Strategy**: Generate platform-specific content recommendations by segment
- **Partnership Development**: Discover and prioritize strategic collaborations
- **Market Expansion**: Identify adjacent categories with validated audience interest
- **Channel Prioritization**: Allocate media budget based on platform-specific audience behavior

**Key principle**: The Application Layer is **purpose-specific**. Each JTBD has unique logic but shares the same underlying Intelligence and Data layers.

---

## **3. Design Principles**

Five core principles guide the architecture:

### **Principle 1: Separate Offline from Runtime**

**Why it matters**: API calls and LLM invocations are expensive (financially and computationally). Precompute everything you can.

**What to precompute (Data Layer)**:

- Item embeddings (text and behavioral)
- Global thematic clusters
- Category-level patterns
- Item similarity indices
- Taxonomy structures

**What must be runtime (Intelligence Layer)**:

- Audience-specific metrics (reach, penetration, affinity for this specific audience)
- Competitive comparisons (overlap between specific brands)
- Segment-specific analysis (how segments differ for this audience)
- Personalized insights (strategic interpretation for this specific context)

**The tradeoff**:

- More offline preparation → faster runtime, lower cost, but less flexibility
- More runtime computation → more flexible, more current, but slower and more expensive

**Guideline**: Precompute anything that's **audience-independent** or applies to **common audience patterns**. Compute at runtime anything that's **audience-specific** or **context-dependent**.

**Example**:

python

```python
# GOOD: Precomputed
item_embedding = embedding_index.get("Nike")  # Instant lookup

# GOOD: Runtime (must be audience-specific)
reach = api.get_overlap(audience="StrideRecover", item="Nike")

# BAD: Runtime computation that could be precomputed
similar_items = compute_similarity(item="Nike", all_items)  # Expensive!
# Should be: similar_items = similarity_index.get("Nike")  # Precomputed
```

### **Principle 2: Composability Over Monoliths**

**Why it matters**: Different JTBDs require different combinations of components. Build reusable blocks, not one-size-fits-all systems.

**Composable components**:

- **Audience definers**: Parse and structure audience definitions
- **Matrix selectors**: Choose appropriate matrix (TW/IG/TW-IG) for context
- **Overlap calculators**: Get reach, penetration, affinity metrics
- **Cluster analyzers**: Identify thematic patterns in affinities
- **Report generators**: Transform data into narrative formats

**Example composition**:

python

```python
# Influencer Selection JTBD
class InfluencerSelector:
    def __init__(self):
        self.audience_definer = AudienceDefiner()
        self.matrix_selector = MatrixSelector()
        self.overlap_calculator = OverlapCalculator()
        self.report_generator = ReportGenerator()
    
    def select(self, brand, platform, budget):
        audience = self.audience_definer.define(brand=brand)
        matrix = self.matrix_selector.choose(jtbd="influencer", platform=platform)
        candidates = self.get_candidates(platform)
        overlaps = self.overlap_calculator.batch_calculate(audience, candidates, matrix)
        ranked = self.rank_by_roi(overlaps, budget)
        return self.report_generator.create("influencer_selection", ranked)

# Competitive Intelligence JTBD
class CompetitiveAnalyzer:
    def __init__(self):
        self.audience_definer = AudienceDefiner()  # Reused
        self.matrix_selector = MatrixSelector()     # Reused
        self.overlap_calculator = OverlapCalculator()  # Reused
        self.report_generator = ReportGenerator()   # Reused
    
    def analyze(self, brand, competitors):
        audience = self.audience_definer.define(brand=brand)
        matrix = self.matrix_selector.choose(jtbd="competitive")
        overlaps = self.overlap_calculator.batch_calculate(audience, competitors, matrix)
        landscape = self.classify_quadrants(overlaps)
        return self.report_generator.create("competitive_intelligence", landscape)
```

**Benefits**:

- Each component can be tested independently
- Components can be reused across JTBDs
- Easy to add new JTBDs by composing existing components
- Clear ownership and maintenance boundaries

### **Principle 3: Source-Agnostic Design**

**Why it matters**: Today you have Twitter and Instagram. Tomorrow you might add TikTok, LinkedIn, purchase data, survey data. The system must accommodate heterogeneous sources.

**Design for multiple matrices**:

- Don't hardcode "Twitter" or "Instagram" in core logic
- Parameterize matrix selection
- Support multiple matrix types: follow matrices, purchase matrices, survey matrices
- Allow matrices with different user sets and item sets

**Abstraction layer**:

python

```python
class Matrix:
    """Abstract base class for audience data matrices"""
    def __init__(self, name: str, user_count: int, item_count: int):
        self.name = name
        self.user_count = user_count
        self.item_count = item_count
    
    @abstractmethod
    def get_item_affinity(self, audience, item) -> float:
        """Return affinity score for item given audience"""
        pass
    
    @abstractmethod
    def get_top_items(self, audience, limit=100) -> List[Item]:
        """Return top items by affinity for audience"""
        pass

class FollowMatrix(Matrix):
    """Matrix based on social media follows"""
    def __init__(self, name, platform):
        super().__init__(name, ...)
        self.platform = platform  # "twitter", "instagram", etc.
    
    def get_item_affinity(self, audience, item):
        # Follow-specific logic
        pass

class PurchaseMatrix(Matrix):
    """Matrix based on purchase data (future)"""
    def __init__(self, name, retailer):
        super().__init__(name, ...)
        self.retailer = retailer
    
    def get_item_affinity(self, audience, item):
        # Purchase-specific logic
        pass

# Usage
tw_matrix = FollowMatrix("TW", platform="twitter")
ig_matrix = FollowMatrix("IG", platform="instagram")
purchase_matrix = PurchaseMatrix("Purchases", retailer="Target")

# All use same interface
affinity_tw = tw_matrix.get_item_affinity(audience, item)
affinity_purchase = purchase_matrix.get_item_affinity(audience, item)
```

**Matrix combination strategies**:

- **Combinable sources** (e.g. Twitter + Instagram follows): Create union matrix (TW-IG)
- **Non-combinable sources** (e.g. follows + purchases): Keep separate, synthesize insights via LLM
- **Partial overlap** (e.g. Twitter users + different Instagram users): Use lookalike matching or keep separate

**Key insight**: Not all data sources can or should be combined into a single matrix. The system must support **multiple simultaneous views** of the audience.

### **Principle 4: Cost-Aware Architecture**

**Why it matters**: Two types of costs dominate:

1. **Audience Intelligence API calls**: Potentially expensive at scale
2. **LLM API calls**: Token costs add up quickly

**Cost optimization strategies**:

**API call optimization**:

python

```python
class CachedAPIClient:
    def __init__(self, api_client, cache_ttl=3600):
        self.api = api_client
        self.cache = TTLCache(maxsize=10000, ttl=cache_ttl)
    
    def get_overlap(self, audience, item, matrix):
        cache_key = f"{hash(audience)}:{item}:{matrix}"
        
        if cache_key in self.cache:
            return self.cache[cache_key]
        
        result = self.api.get_overlap(audience, item, matrix)
        self.cache[cache_key] = result
        return result
    
    def batch_get_overlap(self, audience, items, matrix):
        """Batch multiple items in single API call"""
        # API supports batch requests - use them
        return self.api.batch_get_overlap(audience, items, matrix)
```

**LLM cost optimization**:

python

```python
class TieredLLMClient:
    def __init__(self):
        self.small_model = LLMClient("gpt-4o-mini")  # Cheap, fast
        self.large_model = LLMClient("claude-sonnet-4")  # Expensive, powerful
    
    def classify_quadrant(self, reach, penetration):
        """Simple task: use small model"""
        return self.small_model.classify(reach, penetration)
    
    def generate_report(self, data, template):
        """Complex synthesis: use large model"""
        return self.large_model.generate(data, template)
    
    def label_cluster(self, items):
        """Medium task: try small, fallback to large"""
        try:
            return self.small_model.label(items)
        except QualityError:
            return self.large_model.label(items)
```

**Precomputation amortizes costs**:

- Compute embeddings once, reuse indefinitely: $0.001/item initially, then $0/query
- Compute clusters once, reuse across audiences: $0.01/cluster initially, then $0/query
- Runtime API calls: $0.01-0.10 per query (ongoing cost)

**Rule of thumb**: If a computation will be reused ≥10 times, precompute it.

### **Principle 5: Validate Everything**

**Why it matters**: LLMs hallucinate. APIs return unexpected results. Data has quality issues. The system must validate at multiple levels.

**Validation layers**:

**API response validation**:

python

```python
class ValidatedAPIClient:
    def get_overlap(self, audience, item, matrix):
        result = self.api.get_overlap(audience, item, matrix)
        
        # Sanity checks
        assert 0 <= result.reach <= 1, f"Invalid reach: {result.reach}"
        assert 0 <= result.penetration <= 1, f"Invalid penetration: {result.penetration}"
        assert result.affinity >= 0, f"Invalid affinity: {result.affinity}"
        
        # Statistical significance check
        if result.sample_size < 100:
            result.warning = "Low sample size, low confidence"
        
        return result
```

**LLM output validation**:

python

```python
class ValidatedLLMClient:
    def classify_quadrant(self, reach, penetration):
        result = self.llm.classify(reach, penetration)
        
        # Validate against known rules
        expected = self.rule_based_classify(reach, penetration)
        
        if result != expected:
            # LLM disagrees with rules - investigate
            self.log_disagreement(result, expected, reach, penetration)
            return expected  # Trust rules over LLM for simple cases
        
        return result
    
    def generate_report(self, data, template):
        report = self.llm.generate(data, template)
        
        # Validate report structure
        assert self.has_required_sections(report, template)
        
        # Validate no hallucinated metrics
        assert not self.contains_ungrounded_claims(report, data)
        
        return report
```

**Data quality validation**:

python

````python
class DataQualityChecker:
    def validate_audience(self, audience):
        """Check audience definition is valid"""
        assert audience.size > 100, "Audience too small for reliable analysis"
        assert audience.has_sufficient_metadata(), "Insufficient audience data"
        return True
    
    def validate_item(self, item):
        """Check item has sufficient data"""
        assert item.has_description or item.has_tweets, "Item lacks content"
        assert item.follower_count > 50, "Item has too few followers"
        return True
```

**Progressive validation**:
1. **Input validation**: Reject invalid inputs early
2. **Intermediate validation**: Check API responses and intermediate results
3. **Output validation**: Verify final outputs meet quality standards
4. **Human-in-the-loop**: Flag low-confidence results for human review

---

## **4. Offline vs. Runtime: The Decision Framework**

The most critical architectural decision for each component: **offline or runtime?**

### **Decision Tree**
```
Is this computation audience-specific?
│
├─ NO: Can it be precomputed?
│  │
│  ├─ YES: OFFLINE (Data Layer)
│  │  Examples: Item embeddings, global clusters, similarity indices
│  │
│  └─ NO: Why not?
│     ├─ Data changes frequently → Consider incremental updates
│     ├─ Computation too expensive → Approximate or sample
│     └─ Uncertain usage → Start offline, monitor usage
│
└─ YES: Does it apply to common audience patterns?
   │
   ├─ YES: Can we precompute for segments?
   │  │
   │  ├─ YES: HYBRID (Precompute segments, query at runtime)
   │  │  Examples: Segment-level clusters, persona-level patterns
   │  │
   │  └─ NO: RUNTIME (Intelligence Layer)
   │     Examples: Audience-specific overlap, competitive positioning
   │
   └─ NO: RUNTIME (Intelligence Layer)
      Examples: Custom audience definitions, ad-hoc comparisons
````

### **Examples Classified**

|Computation|Audience-Specific?|Common Pattern?|Decision|Rationale|
|---|---|---|---|---|
|**Item text embedding**|No|N/A|OFFLINE|Same for all audiences, stable|
|**Item behavioral embedding**|No (per matrix)|N/A|OFFLINE (per matrix)|Matrix-specific but audience-independent|
|**Global thematic clusters**|No|N/A|OFFLINE|Universal patterns across audiences|
|**Category-level affinities**|Yes|Yes|HYBRID|Precompute for major segments, runtime for custom|
|**Brand overlap metrics**|Yes|No|RUNTIME|Specific to each brand pair and audience|
|**Segment identification**|Yes|Yes|HYBRID|Precompute common segments, runtime for custom|
|**Competitive quadrant classification**|Yes|No|RUNTIME|Depends on specific competitive set|
|**Influencer ranking**|Yes|No|RUNTIME|Depends on campaign context and budget|

### **Hybrid Pattern: Precomputed Segments**

Many computations are audience-specific but follow common patterns. **Solution**: Precompute for common segments, interpolate or compute at runtime for custom audiences.

python

````python
class SegmentedDataLayer:
    def __init__(self):
        # Precomputed for common segments
        self.segment_clusters = {
            "GenZ_Female_Urban": precomputed_clusters,
            "Millennial_Male_Fitness": precomputed_clusters,
            "GenX_Parent_Wellness": precomputed_clusters,
            # ... 20-50 common segments
        }
    
    def get_clusters(self, audience):
        # Check if audience matches a precomputed segment
        segment = self.match_segment(audience)
        
        if segment and segment in self.segment_clusters:
            return self.segment_clusters[segment]
        
        else:
            # Custom audience: compute at runtime
            return self.compute_clusters_runtime(audience)
    
    def match_segment(self, audience):
        """Fuzzy matching to precomputed segments"""
        # If audience is close enough to a precomputed segment, use it
        for segment, definition in self.segment_definitions.items():
            if self.similarity(audience, definition) > 0.9:
                return segment
        return None
```

**Benefits**:
- Common cases (90% of queries) are fast and cheap (precomputed)
- Rare cases (10% of queries) still work (runtime computation)
- System gracefully handles both

---

## **5. Component Interactions: Information Flow**

Let's trace a complete workflow to see how components interact.

### **Example: Influencer Selection for StrideRecover**

**User request**: "Find Instagram influencers for our recovery footwear brand targeting serious marathon runners. Budget: $50K."

**Step-by-step flow**:
```
┌─────────────────────────────────────────────────┐
│ 1. APPLICATION LAYER: Influencer Selection JTBD │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 2. INTELLIGENCE LAYER: Query Planner            │
│    - Parse intent: Influencer Selection          │
│    - Extract constraints:                        │
│      • Brand: recovery footwear                  │
│      • Target: serious marathon runners          │
│      • Platform: Instagram                       │
│      • Budget: $50K                              │
│    - Select matrix: IG (campaign platform)       │
│    - Plan workflow: Define audience → Get        │
│      candidates → Calculate overlaps → Rank      │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 3. INTELLIGENCE LAYER: API Client               │
│    - Define audience:                            │
│      audience = api.define_audience({            │
│        "brand": "StrideRecover",                 │
│        "segment": "Dedicated_Athletes"           │
│      })                                          │
│    - Result: audience_id = "aud_12345"           │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 4. DATA LAYER: Precomputed Clusters             │
│    - Query: Get Instagram influencers in         │
│      "Running Ecosystem" cluster                 │
│    - Returns: 50 candidate influencers           │
│      [@RunCoachKatie, @MarathonMindset, ...]     │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 5. INTELLIGENCE LAYER: API Client (batch)       │
│    - Parallel API calls:                         │
│      overlaps = api.batch_get_overlap(           │
│        audience="aud_12345",                     │
│        items=candidates,                         │
│        matrix="IG"                               │
│      )                                           │
│    - Returns: reach, penetration, affinity for   │
│      each candidate                              │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 6. DATA LAYER: Influencer Metadata              │
│    - Enrich with precomputed data:               │
│      • Follower counts                           │
│      • Engagement rates                          │
│      • Content themes (from text embeddings)     │
│      • Estimated costs                           │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 7. INTELLIGENCE LAYER: LLM Orchestrator         │
│    - Rank influencers:                           │
│      ranked = llm.rank_influencers(              │
│        overlaps,                                 │
│        budget=$50K,                              │
│        criteria=["overlap", "affinity",          │
│                  "cost_efficiency", "authentic"] │
│      )                                           │
│    - Strategic interpretation:                   │
│      • "RunCoachKatie has 38% reach, 45x         │
│         affinity → perfect fit"                  │
│      • "FitLifeJenna has 0.8% reach → avoid"     │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 8. INTELLIGENCE LAYER: LLM Orchestrator         │
│    - Generate report:                            │
│      report = llm.generate_report(               │
│        template="influencer_selection",          │
│        data=ranked,                              │
│        top_n=5                                   │
│      )                                           │
│    - Output: Structured report with:             │
│      • Top 5 recommended influencers             │
│      • Rationale for each                        │
│      • Estimated ROI                             │
│      • Campaign activation guidance              │
└──────────────────┬──────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────────────┐
│ 9. APPLICATION LAYER: Return to user            │
│    - Display report in UI                        │
│    - Enable drill-down into each influencer      │
│    - Allow refinement and re-ranking             │
└──────────────────────────────────────────────────┘
````

**Key observations**:

1. **Data Layer was queried twice**: Once for candidate influencers (precomputed cluster), once for metadata (precomputed profiles)
2. **API was called once**: Batch call for all candidates (cost-efficient)
3. **LLM was called twice**: Once for ranking logic, once for report generation
4. **No redundant computation**: Everything that could be precomputed was
5. **Clear separation**: Each layer has distinct responsibility

---

## **6. The Matrix Question: A Preview**

One of the most important architectural decisions is **which matrix to use for which query**.

You have three matrices:

- **TW**: Twitter follows only
- **IG**: Instagram follows (via lookalikes)
- **TW-IG**: Combined (Twitter follows OR Instagram follows of lookalikes)

**The question**: Should TW-IG be the default? Or should matrix selection be query-specific?

**Preview of Part 4 answer**: It depends on the JTBD.

**Quick heuristic**:

|JTBD|Default Matrix|Rationale|
|---|---|---|
|**Influencer Selection**|Platform-specific (TW or IG)|Activate where influencer has audience|
|**Competitive Intelligence**|TW-IG|Broadest view of competitive landscape|
|**Content Strategy**|Both separately|Platform-specific behaviors matter|
|**Partnership Development**|TW-IG|Initial screening, then platform-specific|

**Why this matters architecturally**:

The system must support:

- **Multiple simultaneous matrices**: Can't just have one "audience matrix"
- **Query-time matrix selection**: Different queries need different matrices
- **Cross-matrix comparisons**: "How does audience differ on Twitter vs. Instagram?"

**Architectural implication**:

python

```python
class MatrixSelector:
    """Encapsulates matrix selection logic"""
    
    def choose(self, jtbd: str, context: dict) -> str:
        """Return matrix name: 'TW', 'IG', or 'TW-IG'"""
        
        if jtbd == "influencer_selection":
            platform = context.get("campaign_platform")
            return "TW" if platform == "twitter" else "IG"
        
        elif jtbd == "competitive_intelligence":
            return "TW-IG"  # Broad view
        
        elif jtbd == "content_strategy":
            return "BOTH_SEPARATE"  # Special case: compare platforms
        
        elif jtbd == "partnership_development":
            stage = context.get("stage")
            return "TW-IG" if stage == "screening" else context.get("platform")
        
        else:
            return "TW-IG"  # Safe default
```

This will be explored in detail in Part 4, but the architecture must anticipate it now.

---

## **7. Practical Constraints & Tradeoffs**

Every architectural decision involves tradeoffs. Here are the key ones:

### **Tradeoff 1: Precomputation vs. Flexibility**

**More precomputation**:

- ✅ Faster runtime
- ✅ Lower cost per query
- ✅ Consistent results
- ❌ Less flexible (can't handle arbitrary queries)
- ❌ Stale data (must be refreshed)
- ❌ Higher storage costs

**More runtime computation**:

- ✅ Maximum flexibility
- ✅ Always current
- ✅ Handles arbitrary queries
- ❌ Slower
- ❌ Higher cost per query
- ❌ Inconsistent results (API variability)

**Recommendation**: Start with aggressive precomputation. Add runtime computation only when flexibility is proven necessary.

### **Tradeoff 2: Single Matrix vs. Multi-Matrix**

**Single combined matrix (TW-IG only)**:

- ✅ Simpler architecture
- ✅ Easier to communicate
- ✅ Single source of truth
- ❌ Loss of platform-specific insights
- ❌ Lookalike noise affects all results
- ❌ Can't answer "how do they differ by platform?"

**Multi-matrix (TW, IG, TW-IG all available)**:

- ✅ Platform-specific insights preserved
- ✅ Can compare across platforms
- ✅ Can choose appropriate matrix per query
- ❌ More complex architecture
- ❌ More API costs (maintain 3 matrices)
- ❌ More storage (3x embeddings, clusters)

**Recommendation**: Support all three matrices. The flexibility is worth the complexity for high-value use cases.

### **Tradeoff 3: Global Clusters vs. Audience-Specific Clusters**

**Global clusters (offline)**:

- ✅ Precomputed, fast, consistent
- ✅ Work across all audiences
- ✅ Easy to maintain
- ❌ May not capture audience-specific patterns
- ❌ One-size-fits-all

**Audience-specific clusters (runtime)**:

- ✅ Perfectly tailored to each audience
- ✅ Reveal unique patterns
- ❌ Must compute for each audience
- ❌ Expensive
- ❌ Inconsistent across audiences

**Recommendation**: Hybrid approach

- Maintain global clusters (offline)
- For high-value audiences, compute custom clusters (cache results)
- Use global clusters as fallback for ad-hoc queries

### **Tradeoff 4: LLM Model Selection**

**Always use large, expensive models (e.g. Claude Sonnet 4)**:

- ✅ Best quality outputs
- ✅ Handles complex synthesis
- ❌ High cost ($0.03-0.10 per query)
- ❌ Slower response times

**Always use small, cheap models (e.g. GPT-4o-mini)**:

- ✅ Low cost ($0.001-0.01 per query)
- ✅ Fast response times
- ❌ Lower quality for complex tasks
- ❌ More hallucinations

**Tiered approach (recommended)**:

- Small models for simple tasks: classification, labeling, formatting
- Large models for complex tasks: strategic synthesis, report generation
- Fallback logic: try small, escalate to large if quality insufficient

---

## **8. Evolution & Extensibility**

The system must evolve as new needs emerge and new data sources are added.

### **Adding New Data Sources**

**Scenario**: You want to add TikTok follow data.

**What changes**:

1. **Data Layer**: Compute TikTok-specific embeddings and clusters
2. **Intelligence Layer**: Add TikTok matrix option to Matrix Selector
3. **Application Layer**: Update JTBDs to handle TikTok (where relevant)

**What doesn't change**:

- Core architecture (three tiers)
- JTBD patterns (influencer selection logic is the same)
- Report generation (same templates)

**Source-agnostic design pays off**: Adding TikTok is incremental, not a rewrite.

### **Adding New JTBDs**

**Scenario**: You want to add "Brand Health Monitoring" JTBD.

**What changes**:

1. **Application Layer**: New JTBD handler
2. **Intelligence Layer**: May need new query patterns
3. **Data Layer**: May need new precomputed indices

**What doesn't change**:

- Existing JTBDs continue working
- Shared components (API Client, LLM Orchestrator) are reused

**Composable design pays off**: New JTBDs are combinations of existing components.

### **Improving Precomputation**

**Scenario**: You discover a new clustering algorithm that produces better segments.

**What changes**:

1. **Data Layer**: Recompute clusters with new algorithm
2. **Version clusters**: Maintain both old and new versions during transition

**What doesn't change**:

- Intelligence Layer (queries clusters by interface, doesn't care about algorithm)
- Application Layer (oblivious to clustering changes)

**Abstraction pays off**: Implementation improvements don't break the system.

---

## **9. Implementation Checklist**

When building this system, implement in this order:

**Phase 1: Data Layer (Offline)**

- [ ]  Item text embeddings (LLM-based)
- [ ]  Item behavioral embeddings (matrix-based, per matrix)
- [ ]  Global thematic clusters
- [ ]  Category taxonomy integration
- [ ]  Vector similarity index (FAISS/Annoy)
- [ ]  Inverted indices (category → items)

**Phase 2: Intelligence Layer (Runtime)**

- [ ]  API Client wrapper (authentication, retries, caching)
- [ ]  Query Planner (parse intent, plan workflow)
- [ ]  Matrix Selector (choose TW/IG/TW-IG based on context)
- [ ]  LLM Orchestrator (tiered model selection)
- [ ]  Validation layer (API responses, LLM outputs)

**Phase 3: Application Layer (JTBDs)**

- [ ]  Influencer Selection
- [ ]  Competitive Intelligence
- [ ]  Content Strategy
- [ ]  Partnership Development
- [ ]  (Add more JTBDs incrementally)

**Phase 4: Production Readiness**

- [ ]  Monitoring and logging
- [ ]  Error handling and alerting
- [ ]  Cost tracking and budgeting
- [ ]  Performance optimization
- [ ]  Documentation

**Phase 5: Evolution**

- [ ]  Add new matrices (TikTok, LinkedIn)
- [ ]  Improve clustering algorithms
- [ ]  Add new JTBDs based on usage
- [ ]  Continuous refinement

---

## **10. Summary: Architecture Principles**

The Audience Intelligence System is built on five core principles:

1. **Separate offline from runtime**: Precompute everything that's audience-independent
2. **Composability over monoliths**: Build reusable blocks, not one-size-fits-all systems
3. **Source-agnostic design**: Prepare for heterogeneous data sources from the start
4. **Cost-aware architecture**: Optimize for both API and LLM costs
5. **Validate everything**: LLMs and APIs need multiple layers of validation

The three-tier architecture maps cleanly to these principles:

- **Data Layer**: Offline preparation (embeddings, clusters, indices)
- **Intelligence Layer**: Runtime orchestration (query planning, API calls, LLM synthesis)
- **Application Layer**: Purpose-specific JTBDs (influencer selection, competitive intelligence)

Matrix selection is context-dependent, not one-size-fits-all. Part 4 will detail when to use TW, IG, or TW-IG.