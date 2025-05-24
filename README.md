# Product Recommender: Technical Documentation

## Prediction Results - 
## User Liked Products

| Product ID | Category | Color  | Style Tags               | Brand    | Tag List                     | Style Tags List          |
|------------|----------|--------|--------------------------|----------|------------------------------|--------------------------|
| P0001      | Shoes    | Green  | Boho                    | H&M      | [boho]                       | [boho]                   |
| P0003      | Shoes    | Gray   | Casual                  | Unknown  | [casual]                     | [casual]                 |
| P0006      | Shoes    | Yellow | Sporty, Streetwear, Boho| Levis    | [sporty, streetwear, boho]   | [sporty, streetwear, boho]|

## Recommendations

| Product ID | Category | Color  | Style Tags             | Brand    | Similarity Score |
|------------|----------|--------|------------------------|----------|------------------|
| P0012      | Shoes    | Red    | Boho, Formal, Casual  | Unknown  | 0.655745         |
| P0037      | Shoes    | Beige  | Boho, Streetwear      | Levis    | 0.634389         |
| P0317      | Shoes    | Beige  | Boho, Casual          | Zara     | 0.623191         |
| P0329      | Shoes    | Gray   | Boho, Casual          | Levis    | 0.582173         |
| P0339      | Shoes    | Gray   | Boho                  | Zara     | 0.542532         |

---
## Data Handling & Feature Engineering

### Data Preprocessing
- **Missing Value Handling**  
  Replaces missing brand values with 'Unknown' to maintain data completeness and prevent bias.
  
- **Style Tags Parsing**  
  Tokenizes comma-separated style tags into individual tags for granular analysis.

- **Feature Extraction**  
  - **Categorical Features**: One-hot encodes category, color, and brand attributes into numerical representations.  
  - **Style Tags**: Converts text-based tags into binary feature vectors using vectorization.

---

### Feature Engineering Techniques
- **Weighted Feature Combination**  
  Assigns weights to features based on style relevance:  
  - Style tags: **3.0** (highest weight)  
  - Category: **2.0** (moderate)  
  - Color: **1.0** (lower)  
  - Brand: **0.5** (lowest).

- **Cross-Feature Analysis**  
  Analyzes relationships between:  
  - Brand ↔ Style tags  
  - Category ↔ Style tags  
  - Color ↔ Style associations.

- **Feature Vectorization**  
  Combines all features into a unified vector for multi-dimensional style representation.

---

## Recommendation Logic & Evaluation Approach

### Recommendation Algorithm
- Computes **cosine similarity** between product feature vectors.  
- Identifies nearest neighbors in feature space for each liked product.  
- Combines similarity scores across multiple liked products for personalized output.

### Recommendation Flow
1. **Input**: List of user-liked product IDs.  
2. **Process**:  
   - Calculate average similarity scores across the catalog.  
   - Rank items by weighted similarity.  
3. **Output**: Top 5–10 stylistically similar products not previously liked.

---

### Evaluation Methodology
- **Metrics**:  
  - **Category Overlap**: Match between recommended and liked product categories.  
  - **Style Tags Overlap**: Alignment of style attributes.  
  - **Overall Similarity**: Average similarity score of recommendations.  

- **Process**:  
  - Compare feature distributions of recommendations vs. liked products.  
  - Measure recommendation diversity.  
  - Analyze preservation of style preferences with novel suggestions.

---

## Assumptions & Limitations

### Key Assumptions
- Style similarity is captured via metadata (no visual data required).  
- Feature weights reflect their contribution to style perception.  
- User preferences derive solely from liked product history.

### Limitations
- **Cold Start Problem**: Limited personalization for new users/products.  
- **Limited Feature Space**: Excludes visual analysis for enhanced matching.  
- **Static Preferences**: No adaptation to evolving user tastes.  
- **Scalability Challenges**: Performance issues with large catalogs.  
- **Data Sparsity**: Inconsistent/style tags impact recommendation quality.  
