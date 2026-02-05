# Choosing the Right Channels for Customer Acquisition

_How to prioritize marketing channels and platforms using audience behavior patterns and platform-specific affinities_

---

## The Business Problem

Your marketing team presents the annual budget allocation:

**CMO:** "We should go big on TikTok. That's where everyone is."  
**Performance Marketing Lead:** "Instagram has been our best performer. Double down there."  
**Head of Content:** "LinkedIn is showing great engagement for our thought leadership."  
**VP Sales:** "Our competitor just launched a podcast. Should we?"

**Current allocation:**

- Instagram: 35% of budget
- LinkedIn: 25%
- Google Ads: 20%
- Facebook: 10%
- TikTok: 5%
- Podcast sponsorships: 5%

**The problem:** This allocation is based on:

- Where marketing team _thinks_ audience is
- What's worked historically (without knowing why)
- Competitor moves (assumes they know what they're doing)
- Platform popularity (general trends, not your audience specifically)

After a year, results are disappointing:

{{< callout "warning" >}} **Post-mortem reveals:**

**Instagram (35% of budget):**

- High impressions, low conversions
- Engagement is likes/saves, not purchases
- Audience uses Instagram for lifestyle inspiration, not product discovery

**TikTok (5% of budget):**

- Poor performance across all metrics
- Content falls flat, feels inauthentic
- Turns out: Only 8% of target audience actively uses TikTok

**Podcast sponsorships (5% of budget):**

- One show performed incredibly well (15x ROI)
- Other four shows delivered near-zero conversions
- No systematic way to pick the right shows

**LinkedIn (25% of budget):**

- Great engagement, minimal revenue impact
- Audience engages with thought leadership but doesn't convert
- Wrong intent: learning mode, not buying mode {{< /callout >}}

**Total CAC:** $127 (target was $45)  
**Channel efficiency variance:** Best channel 12x better than worst  
**Wasted spend:** ~$340K on wrong channels

**The core issue:** Channel selection based on assumptions, not audience intelligence.

---

## The Data Approach

### The Core Principle

{{< callout "highlight" >}} **Different audiences use different platforms for different reasons.**

Your target customer might be "on Instagram," but that doesn't mean Instagram is the right acquisition channel for your product:

- They use Instagram for entertainment → Won't convert on product ads
- They use LinkedIn for professional learning → Won't buy consumer products there
- They use podcasts for deep focus time → Highly receptive to sponsorship messages

**The right channel is where your audience is + in the right mindset + with the right intent.** {{< /callout >}}

### The Framework: Channel Prioritization Matrix

**Step 1: Measure platform presence and engagement**

For each potential channel, calculate:

|Metric|Formula|What It Reveals|
|---|---|---|
|**Platform Reach**|% of your audience on platform|How many can you reach|
|**Platform Affinity**|Engagement vs. general population|How intensely they use it|
|**Content Engagement**|Affinity for content types on platform|What they consume there|
|**Purchase Intent**|Affinity for shopping/discovery behavior|Will they buy through this channel|

**Step 2: Map channel-specific behavior patterns**

mermaid

````mermaid
graph TB
    A[Platform Affinity Data] --> B{Usage Intent}
    B --> C[Entertainment/Distraction]
    B --> D[Learning/Information]
    B --> E[Discovery/Shopping]
    B --> F[Community/Connection]
    
    C --> C1[Awareness Only]
    D --> D1[Consideration Stage]
    E --> E1[Conversion Optimized]
    F --> F1[Retention/Loyalty]
    
    style A fill:#EFF6FF
    style E fill:#D1FAE5
    style E1 fill:#D1FAE5
```

**Step 3: Calculate channel prioritization score**
```
Channel Score = (Reach × Affinity × Intent Match × Content Fit) ÷ Competition
````

Where:

- **Reach:** % of target audience on platform (0-1)
- **Affinity:** Platform engagement vs. general pop (multiplier)
- **Intent Match:** Platform usage aligns with buying journey (0-1)
- **Content Fit:** Your content type aligns with platform norms (0-1)
- **Competition:** Ad saturation, noise level (0.5-2x modifier)

**Step 4: Match channel to funnel stage**

|Channel Type|Best For|When to Use|
|---|---|---|
|**High Reach, Low Intent**|Awareness|Early funnel, brand building|
|**Moderate Reach, High Intent**|Conversion|Direct response, acquisition|
|**Low Reach, High Affinity**|Retention|Community, loyalty programs|
|**High Intent, Purchase Behavior**|Growth|Scaling proven acquisition|

---

## Worked Example: PeakForm Fitness App Channel Strategy

### Scenario Setup

<div style="border-left:5px solid #4F46E5; background-color:#F3F4F6; padding:1em; margin-bottom:1em; border-radius:8px;">

**PeakForm**

- Strength training and workout tracking app
- Target: Serious lifters aged 25-45
- Current users: 280,000 active
- Price: $12/month subscription
- CAC target: $35
- Challenge: Customer acquisition costs too high, unclear which channels to prioritize

</div>

**Current channel mix (based on "where fitness brands advertise"):**

- Instagram: 40% ($280K/year)
- Facebook: 20% ($140K)
- YouTube: 15% ($105K)
- TikTok: 10% ($70K)
- Podcast ads: 10% ($70K)
- Google Ads: 5% ($35K)

**Results after 1 year:**

- Total spend: $700K
- New customers: 8,200
- Average CAC: $85 (143% over target)
- Huge variance: Best channel $22 CAC, worst $340 CAC

**Question:** Which channels should PeakForm prioritize based on actual audience behavior?

### Step 1: Platform Presence Analysis

**Measuring PeakForm's 280,000 user audience across platforms:**

|Platform|% Audience Using|General Population %|Affinity|Interpretation|
|---|---|---|---|---|
|**Instagram**|68%|52%|1.31x|Present, but only moderate affinity|
|**YouTube**|72%|54%|1.33x|Present, moderate affinity|
|**TikTok**|18%|38%|0.47x|**Actively avoid** (below general pop)|
|**Facebook**|42%|48%|0.88x|Below average usage|
|**Reddit**|48%|22%|2.18x|Strong over-index|
|**Podcast apps**|56%|32%|1.75x|Strong over-index|
|**Twitter/X**|38%|28%|1.36x|Moderate over-index|
|**LinkedIn**|52%|44%|1.18x|Slight over-index|

{{< callout "note" >}} **Initial surprise:**

- TikTok has 0.47x affinity (audience actively avoids it)
- Currently spending $70K/year on TikTok
- Reddit has 2.18x affinity but $0 budget
- Podcasts have 1.75x affinity with moderate budget

**Platform presence ≠ platform opportunity.** Need deeper analysis of _how_ they use each platform. {{< /callout >}}

### Step 2: Platform-Specific Behavior Analysis

#### Instagram (68% reach, 1.31x affinity)

**What PeakForm audience does on Instagram:**

|Activity/Content Type|Affinity|Reach|Interpretation|
|---|---|---|---|
|Follow fitness influencers|8.2x|44%|High engagement with fitness content|
|Fitness transformation content|12.4x|38%|Inspirational consumption|
|Workout videos (watch)|6.8x|52%|Passive consumption|
|Workout videos (save for later)|14.2x|28%|Intent to use|
|**Product discovery/shopping**|**2.1x**|**24%**|**Low purchase intent**|
|Fitness memes|9.4x|36%|Entertainment|

**Purchase behavior signals:**

|Signal|Affinity|Interpretation|
|---|---|---|
|Click shopping tags|1.8x|Low|
|Save product posts|2.4x|Low|
|Engage with fitness brand ads|3.2x|Moderate|

{{< callout "warning" >}} **Instagram analysis:**

**Strengths:**

- High reach (68% of audience)
- Strong engagement with fitness content
- Saving workout content (14.2x) shows intent to use later

**Weaknesses:**

- **Low purchase intent** (2.1x for shopping)
- Used for inspiration and entertainment, not discovery
- Ad engagement moderate (3.2x), not strong

**Recommended use:** Awareness and inspiration, NOT direct response acquisition

**Budget implication:** Reduce from 40% to 15% of budget. Use for brand building and retargeting, not cold acquisition. {{< /callout >}}

#### YouTube (72% reach, 1.33x affinity)

**What PeakForm audience does on YouTube:**

|Activity/Content Type|Affinity|Reach|Interpretation|
|---|---|---|---|
|Workout tutorial videos|18.4x|58%|High intent, educational|
|Form check videos|22.8x|42%|Learning proper technique|
|Program review videos|16.2x|36%|Research before purchase|
|Fitness documentaries|8.4x|34%|Casual interest|
|Exercise science content|19.6x|48%|Deep learning|

**Purchase journey signals:**

|Signal|Affinity|Reach|Interpretation|
|---|---|---|---|
|Watch app review videos|24.2x|32%|Researching solutions|
|Search "best workout app"|28.4x|28%|High purchase intent|
|Watch comparison videos|21.8x|30%|Consideration stage|

{{< callout "highlight" >}} **YouTube analysis:**

**Strengths:**

- High reach (72%)
- **Very high intent content** (program reviews 16.2x, comparisons 21.8x, searches 28.4x)
- Used for research and learning, not just entertainment
- Audience in consideration stage when watching

**Weaknesses:**

- Competitive landscape (many fitness YouTubers)
- Longer content = harder to attribute

**Recommended use:**

- Pre-roll ads on high-intent searches ("best workout app," "workout tracker review")
- Sponsorships with form/technique channels (22.8x affinity)
- Comparison video placements

**Budget implication:** Increase from 15% to 25%. High-intent audience in research mode. {{< /callout >}}

#### TikTok (18% reach, 0.47x affinity)

**What the 18% who ARE on TikTok do:**

|Activity/Content Type|Affinity|Reach (of the 18%)|Interpretation|
|---|---|---|---|
|Fitness entertainment|4.2x|62%|Casual content|
|Gym fails/humor|6.8x|48%|Entertainment|
|Quick tips|5.4x|54%|Bite-sized info|
|**Workout programs**|**1.8x**|**12%**|**Very low intent**|

{{< callout "warning" >}} **TikTok analysis:**

**Critical insight:**

- Only 18% of PeakForm audience uses TikTok at all (0.47x - actively avoid)
- Those who do use it primarily for entertainment, not serious training content
- Workout program affinity is only 1.8x (very low)

**Why the mismatch:**

- PeakForm targets serious lifters (25-45, intermediate-advanced)
- TikTok fitness content skews younger (18-24), beginner, entertainment-focused
- Audience demographic mismatch

**Recommended use:** Eliminate entirely

**Budget implication:** Reallocate $70K from TikTok to higher-performing channels {{< /callout >}}

#### Reddit (48% reach, 2.18x affinity)

**What PeakForm audience does on Reddit:**

|Subreddit/Activity|Affinity|Reach|Interpretation|
|---|---|---|---|
|r/fitness|12.4x|34%|Core community|
|r/weightroom|28.6x|22%|Serious lifters|
|r/bodybuilding|18.2x|26%|Niche focus|
|r/homegym|24.8x|18%|Equipment focused|
|**Form check posts**|**32.4x**|**28%**|**High engagement**|
|**Program discussions**|**26.8x**|**32%**|**Research behavior**|
|Ask for app recommendations|38.2x|16%|Direct purchase intent|

**Behavior patterns:**

|Pattern|Affinity|Interpretation|
|---|---|---|
|Post questions, seek advice|28.4x|Active participation|
|Research before trying new programs|31.2x|Careful decision-makers|
|Trust community recommendations|34.6x|Peer influence high|
|Skeptical of ads|22.8x|Value authenticity|

{{< callout "highlight" >}} **Reddit analysis:**

**Strengths:**

- **Very high affinity** (2.18x overall, 28-38x for specific behaviors)
- **Extremely high intent:** Asking for recommendations (38.2x), researching programs (31.2x)
- Community trust is high (34.6x for peer recommendations)
- Half the audience (48%) actively uses Reddit

**Weaknesses:**

- Ad skepticism (22.8x)
- Requires authentic, non-promotional approach
- Community moderation varies by subreddit

**Recommended use:**

- NOT display ads (community is skeptical)
- Organic community engagement (answer questions, provide value)
- Strategic AMAs (Ask Me Anything) with trainers
- Sponsor community challenges
- User-generated testimonials and discussions

**Budget implication:** Allocate 15% of budget. Requires community management, not just ad spend. {{< /callout >}}

#### Podcasts (56% reach, 1.75x affinity)

**Which podcasts PeakForm audience listens to:**

|Podcast Type/Show|Affinity|Reach|Listener Intent|
|---|---|---|---|
|Strength training focused (Barbell Medicine, Stronger by Science)|42.8x|18%|Deep expertise|
|General fitness (Mind Pump, Ben Greenfield)|12.4x|24%|Broad wellness|
|Business/productivity (Tim Ferriss, Huberman Lab)|8.2x|32%|Optimization mindset|
|True crime / entertainment|2.1x|28%|Wrong intent|

**Podcast behavior:**

|Behavior|Affinity|Interpretation|
|---|---|---|
|Listen during workouts|24.2x|Captive attention|
|Listen during commute|18.6x|Focused listening|
|Trust host recommendations|28.4x|High influence|
|Use promo codes from ads|31.2x|**Direct conversion behavior**|

{{< callout "highlight" >}} **Podcast analysis:**

**Strengths:**

- Strong affinity (1.75x overall, 42.8x for niche shows)
- **Very high trust and conversion** (use promo codes 31.2x)
- Captive attention (24.2x listen during workouts)
- Host recommendation trust is very high (28.4x)

**Critical insight from past performance:**

- Previous podcast spend: $70K across 5 shows
- 1 show (Stronger by Science): 42.8x affinity, $18 CAC, 15x ROI
- 4 other shows (general fitness/entertainment): 2-8x affinity, $180-340 CAC, negative ROI

**Problem:** Didn't use affinity data to pick shows. Picked based on download numbers.

**Recommended use:**

- **Only sponsor high-affinity niche shows** (42.8x for Stronger by Science, Barbell Medicine)
- Avoid general fitness entertainment podcasts
- Build long-term partnerships (6-12 month integrations, not one-off ads)
- Host-read ads, not generic spots

**Budget implication:** Maintain 10% budget but reallocate entirely to high-affinity shows {{< /callout >}}

#### Google Ads (Search behavior)

**Search terms PeakForm audience uses:**

|Search Type|Affinity|Volume|Intent|
|---|---|---|---|
|"best workout tracking app"|38.4x|High|Direct intent|
|"stronglifts alternative"|42.2x|Medium|Switching intent|
|"workout app for powerlifting"|36.8x|Medium|Specific need|
|"free workout tracker"|8.2x|High|Price sensitive|
|"home workout app"|4.6x|Very high|Wrong audience|

**Search behavior patterns:**

|Pattern|Affinity|Interpretation|
|---|---|---|
|Compare specific apps|34.2x|Research-driven|
|Search for "program name + app"|28.6x|Looking for implementation|
|Read reviews before download|31.8x|Careful buyers|

{{< callout "tip" >}} **Google Ads analysis:**

**Strengths:**

- **Extremely high intent** (38-42x for specific searches)
- Direct conversion path
- Users actively seeking solutions

**Weaknesses:**

- Current budget only 5% ($35K)
- Under-invested in highest-intent channel

**Recommended use:**

- Focus on high-intent, specific searches (42.2x "stronglifts alternative")
- Avoid broad, low-intent terms (4.6x "home workout app")
- Retarget app comparison searchers

**Budget implication:** Increase from 5% to 20%. Highest intent channel, dramatically under-resourced. {{< /callout >}}

### Step 3: Channel Prioritization Scoring

**Comprehensive scoring:**

|Channel|Reach|Affinity|Intent Match|Content Fit|Competition|**Priority Score**|Recommended Budget|
|---|---|---|---|---|---|---|---|
|**Google Search**|0.65|38x|0.95|0.90|1.2|**18.5**|**25%** ($175K)|
|**YouTube**|0.72|22x|0.80|0.85|1.4|**9.8**|**25%** ($175K)|
|**Reddit**|0.48|32x|0.85|0.70|0.8|**9.2**|**15%** ($105K)|
|**Podcasts (niche)**|0.18|43x|0.90|0.95|0.6|**5.9**|**15%** ($105K)|
|**Instagram**|0.68|8x|0.30|0.75|1.8|**0.7**|**10%** ($70K)|
|**Facebook**|0.42|3x|0.25|0.60|1.6|**0.2**|**5%** ($35K)|
|**TikTok**|0.18|2x|0.15|0.40|1.4|**0.08**|**0%** ($0)|
|**LinkedIn**|0.52|4x|0.20|0.50|1.3|**0.3**|**5%** ($35K)|

**Buffer/Testing** | - | - | - | - | - | - | **5%** ($35K) |

{{< callout "highlight" >}} **New allocation vs. old:**

**Old (assumption-based):**

- Instagram: 40%
- Facebook: 20%
- YouTube: 15%
- TikTok: 10%

**New (affinity-based):**

- Google Search: 25% (+400% from 5%)
- YouTube: 25% (+67% from 15%)
- Reddit: 15% (new)
- Niche Podcasts: 15% (focused from 10%)
- Instagram: 10% (-75% from 40%)

**Eliminated:**

- TikTok: 0% (was 10%)
- Most of Facebook budget reallocated {{< /callout >}}

### Step 4: Channel-Specific Strategy

**Detailed implementation plan for each channel:**

#### Tier 1: High-Intent Conversion Channels (65% of budget)

<div style="border-left:5px solid #10B981; background:#F0FDF4; padding:1.5em; margin:1em 0;">

**Google Search (25% - $175K)**

**Target searches:**

- "best strength training app" (38.4x affinity)
- "[competitor name] alternative" (42.2x)
- "workout app for powerlifting" (36.8x)
- "5/3/1 app" (specific program names, 28.6x)

**Avoid:**

- "free workout app" (8.2x - price sensitive)
- "home workout app" (4.6x - wrong audience)
- Broad fitness terms

**Ad copy approach:**

- Emphasize serious lifting features
- Highlight program compatibility ("Built for 5/3/1, nSuns, GZCL")
- Lead with strength focus, not general fitness

**Expected CAC:** $22-28  
**Expected conversions:** 6,250 customers/year

</div> <div style="border-left:5px solid #3B82F6; background:#EFF6FF; padding:1.5em; margin:1em 0;">

**YouTube (25% - $175K)**

**Placement strategy:**

- Pre-roll on form check videos (22.8x affinity)
- Program review videos (16.2x)
- Sponsorships with technique-focused channels

**Specific channels/creators:**

- Stronger by Science (42.8x affinity)
- Jeff Nippard (form focus, 24.2x)
- Renaissance Periodization (science-based, 28.4x)

**Creative approach:**

- 15-second skippable pre-roll highlighting one key feature
- Longer sponsorship segments (60-90sec) demonstrating app
- Creator testimonials (not scripted ads)

**Expected CAC:** $32-38  
**Expected conversions:** 4,800 customers/year

</div> <div style="border-left:5px solid #8B5CF6; background:#F5F3FF; padding:1.5em; margin:1em 0;">

**Reddit (15% - $105K)**

**Strategy (organic + sponsored):**

**Organic (60% of budget - $63K):**

- Dedicated community manager
- Active in r/weightroom (28.6x), r/fitness (12.4x), r/homegym (24.8x)
- Answer questions, provide value
- Quarterly AMA with head coach
- User testimonials and organic discussions

**Sponsored (40% of budget - $42K):**

- Promoted posts in high-affinity subreddits
- "We built a lifting app. Here's what we learned" posts
- Avoid hard sells, focus on education

**Expected CAC:** $28-35  
**Expected conversions:** 3,200 customers/year

</div>

#### Tier 2: Targeted Awareness (30% of budget)

<div style="border-left:5px solid #F59E0B; background:#FFF7ED; padding:1.5em; margin:1em 0;">

**Niche Podcasts (15% - $105K)**

**Only sponsor high-affinity shows:**

- Stronger by Science (42.8x) - $4K/month, 12 months
- Barbell Medicine (38.2x) - $3K/month, 12 months
- Iron Culture (31.4x) - $2.5K/month, 12 months

**Integration approach:**

- Long-term partnerships (not one-off ads)
- Host-read, personalized to show
- Unique promo codes per show
- Mid-roll placement (highest attention)

**Expected CAC:** $18-24  
**Expected conversions:** 5,000 customers/year

</div> <div style="border-left:5px solid #EC4899; background:#FDF2F8; padding:1.5em; margin:1em 0;">

**Instagram (10% - $70K)**

**Use for retargeting and brand, NOT cold acquisition:**

**Content strategy:**

- User transformations and testimonials
- Form tips and technique content
- Workout highlights from app users

**Paid strategy:**

- Retarget website visitors (70% of budget)
- Lookalike audiences based on converters (20%)
- Minimal cold prospecting (10%)

**Expected CAC:** $45-60 (retargeting only)  
**Expected conversions:** 1,400 customers/year

</div>

#### Tier 3: Experimental/Testing (10% of budget)

<div style="border-left:5px solid #6B7280; background:#F9FAFB; padding:1.5em; margin:1em 0;">

**Buffer & Testing (10% - $70K)**

**Quarterly tests:**

- Q1: Twitter/X fitness community ($17.5K test)
- Q2: Fitness newsletter sponsorships ($17.5K test)
- Q3: Gym partnerships/referrals ($17.5K test)
- Q4: Best performer gets scaled ($17.5K + reallocate)

**Success criteria for scaling:**

- CAC < $40
- LTV:CAC ratio > 3:1
- 30-day retention > 70%

</div>

### Step 5: Expected Outcomes

**Projected performance with new allocation:**

|Metric|Old Strategy|New Strategy (Affinity-Based)|Improvement|
|---|---|---|---|
|**Total budget**|$700K|$700K|-|
|**New customers**|8,200|19,650|+140%|
|**Average CAC**|$85|$36|-58%|
|**Customers at target CAC (<$35)**|2,400 (29%)|14,800 (75%)|+517%|
|**Wasted spend**|$340K|$85K|-75%|
|**ROI**|1.8x|4.2x|+133%|

**Channel-by-channel impact:**

|Channel|Old CAC|New CAC|Old Volume|New Volume|Impact|
|---|---|---|---|---|---|
|**Google Search**|$48|$25|730|7,000|+859%|
|**YouTube**|$62|$35|1,690|5,000|+196%|
|**Reddit**|N/A|$32|0|3,280|New|
|**Podcasts (focused)**|$140 avg|$21|500|5,000|+900%|
|**Instagram**|$92|$52|3,040|1,350|Retargeting only|
|**TikTok**|$340|-|206|0|Eliminated|
|**Facebook**|$180|$75|778|467|Reduced|

---

## Common Pitfalls

### 1. Optimizing for Platform Size, Not Audience Fit

{{< callout "warning" >}} **The trap:** "TikTok has 1 billion users, we should advertise there"

**Why it fails:** Platform size doesn't matter if your audience isn't there or uses it differently

**Example from PeakForm:**

- TikTok: 1B+ users globally
- PeakForm audience on TikTok: 18% (below general population)
- Those who are there: Use for entertainment (6.8x gym fails), not training (1.8x programs)

**Result:** $70K spent, 206 customers, $340 CAC

**How to avoid:**

- Check YOUR audience's affinity for platform, not platform's total size
- If affinity < 1.0x, audience actively avoids it
- Even if present, check what they use it for {{< /callout >}}

### 2. Confusing Presence with Purchase Intent

{{< callout "warning" >}} **The trap:** "68% of our audience is on Instagram, so that's our priority"

**Why it fails:** Being on a platform ≠ buying through that platform

**Example from PeakForm:**

- Instagram: 68% reach (good!)
- But: Shopping behavior only 2.1x affinity
- Use for inspiration (12.4x transformations), not discovery
- Entertainment intent, not purchase intent

**Better interpretation:**

- Instagram: Awareness and retargeting
- Google Search: Purchase intent (38.4x for "best workout app")

**How to avoid:**

- Map platform usage to funnel stage (awareness vs. consideration vs. purchase)
- Check purchase behavior signals specifically
- Allocate budget by intent, not just presence {{< /callout >}}

### 3. Generic Implementation of Right Channel

{{< callout "warning" >}} **The trap:** "Podcasts work, so let's sponsor any fitness podcast"

**Why it fails:** Channel affinity varies wildly within channel category

**Example from PeakForm:**

- Podcasts overall: 1.75x affinity (good)
- But:
    - Stronger by Science: 42.8x affinity, $18 CAC ✅
    - General fitness podcast: 8.2x affinity, $180 CAC ❌
    - True crime (listened to by lifters): 2.1x affinity, $340 CAC ❌

**Critical insight:** Right channel + wrong show = failure

**How to avoid:**

- Get specific within channels
- For podcasts: Check affinity for individual shows
- For YouTube: Check affinity for specific creators
- For Reddit: Check affinity for specific subreddits
- Test small, scale what works {{< /callout >}}

### 4. Ignoring Anti-Affinity Signals

{{< callout "warning" >}} **The trap:** "Our competitor advertises on TikTok, so we should too"

**Why it fails:** Your audience might actively avoid platforms

**Example from PeakForm:**

- TikTok: 0.47x affinity
- Meaning: PeakForm audience uses TikTok LESS than general population
- They actively choose not to use it (or use minimally)

**Why competitors might still advertise there:**

- They don't know it's not working (vanity metrics)
- Different audience than yours (younger, beginner-focused)
- Misguided assumptions

**How to avoid:**

- If affinity < 1.0x, question whether to be there at all
- If affinity < 0.7x, strong signal to avoid
- Don't follow competitors blindly - they may be wrong {{< /callout >}}

---

## Complementary Approaches

### When Affinity Data Isn't Enough

{{< expand "Attribution Analysis" >}} **Method:**

- Track which channels drive customers with best LTV
- Not just first touch, but quality of customer

**Example from PeakForm:**

|Channel|CAC|6-Mo Retention|LTV|LTV:CAC|
|---|---|---|---|---|
|Google Search|$25|78%|$180|7.2x|
|Niche Podcasts|$21|84%|$220|10.5x|
|Instagram|$52|64%|$140|2.7x|

**Insight:** Niche podcasts not only have low CAC but highest-quality customers

**Implication:** Worth paying MORE for podcast slots because LTV justifies it {{< /expand >}}

{{< expand "Channel-Specific A/B Testing" >}} **Method:**

- Test different creative approaches by channel
- What works on YouTube ≠ what works on Reddit

**Example tests:**

**YouTube:**

- Test A: Product demo (15-sec)
- Test B: Transformation story (30-sec)
- Test C: Scientific explanation (45-sec)

**Reddit:**

- Test A: "We built an app" post
- Test B: AMA format
- Test C: User testimonial thread

**Value:** Optimize within channels, not just between channels {{< /expand >}}

{{< expand "Funnel Stage Mapping" >}} **Method:**

- Map each channel to funnel stage based on intent
- Allocate budget by stage needs

**PeakForm example:**

**Awareness (need: reach):**

- Instagram (retargeting of site visitors)
- YouTube (broad fitness content)

**Consideration (need: education):**

- YouTube (program reviews, comparisons)
- Reddit (community discussions)

**Purchase (need: direct intent):**

- Google Search (buying keywords)
- Niche Podcasts (trusted recommendations)

**Retention (need: community):**

- Reddit (ongoing engagement)
- Email (owned channel)

**Budget allocation by stage:**

- 20% awareness
- 30% consideration
- 40% purchase
- 10% retention

**Value:** Ensures balanced funnel, not over-investment in single stage {{< /expand >}}

---

## Actionable Takeaway

{{< callout "highlight" >}} **To prioritize marketing channels effectively:**

1. **Map audience presence AND behavior on each platform**
    - Don't just check if they're there
    - Check what they use the platform FOR
    - Calculate affinity, not just reach
2. **Match channel to purchase intent**
    - **High intent** (Google Search, comparison content): Conversion budget
    - **Medium intent** (YouTube reviews, Reddit discussions): Consideration budget
    - **Low intent** (Entertainment consumption): Awareness/retargeting only
3. **Get specific within channels**
    - Not "podcasts" but "which podcasts specifically"
    - Not "YouTube" but "which creators/video types"
    - Not "Reddit" but "which subreddits"
4. **Calculate true channel score:**

```
   Priority = (Reach × Affinity × Intent × Content Fit) ÷ Competition
```

5. **Reallocate ruthlessly**
    - Kill channels with <1.0x affinity (audience avoids them)
    - Reduce channels with low intent match
    - Invest in high-intent, high-affinity channels

**Red flags to reallocate budget:**

- "Everyone uses X platform" (but not YOUR audience)
- High spend on low affinity channels
- Following competitor moves without validation
- Optimizing tactics on wrong channels

**Next step:** Run affinity analysis on your current channel mix this week. Calculate affinity scores for each platform. You'll immediately see where you're over-invested (high spend, low affinity) and under-invested (low spend, high affinity). Reallocate 20-30% of budget based on findings. {{< /callout >}}

---

_Platform popularity doesn't predict performance. Your specific audience's behavior on each platform does. Affinity data reveals where your customers actually are, what they're doing there, and whether they're in buying mode._
