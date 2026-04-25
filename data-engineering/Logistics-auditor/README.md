## A. Executive Summary

Veridi Logistics is experiencing a measurable delivery promise reliability issue with clear regional concentration rather than a uniform nationwide failure. After joining orders, reviews, and customer location data, we found that approximately 8.11% of analyzed deliveries were late, including 4.37% that were super late (more than 5 days late). States such as AL, MA, PI, CE, and SE show disproportionately high late-delivery rates, while on-time deliveries remain the majority overall. Sentiment analysis confirms logistics impact: late deliveries are associated with lower customer review scores versus on-time deliveries. The bonus Promise Accuracy Risk Monitor identified a priority intervention cluster where high late rates and weaker review scores overlap, enabling targeted operational recovery.
Category translation analysis (Portuguese to English) showed that Electronics/Tech categories had a slightly higher late-delivery rate than Furniture/Home in this dataset (8.23% vs 7.80%), while Furniture/Home had marginally lower average review scores.

## B. Project Links

- Notebook Link: [https://deepnote.com/workspace/Data-Engineering-66bfe4bc-84d1-4127-a348-f77d93af8741/project/Logistics-70856a3f-44f4-4d1e-923d-8838411dc434/notebook/Notebook-1-84b9e32fc2474b3d8ca54455231aab42?secondary-sidebar-autoopen=true&secondary-sidebar=agent]
- Dashboard Link: [https://public.tableau.com/app/profile/raymond.igabineza/viz/VeridiLogistics/Dashboard1?publish=yes]
- Presentation Link (Slides): [https://gamma.app/docs/Veridi-Logistics-Last-Mile-Delivery-Performance-Audit-j63mkhm6nm8bvds]

## C. Technical Explanation

### Data Cleaning
- Loaded relational Olist CSV tables using relative file paths.
- Joined reviews to orders on order_id and customers to orders on customer_id.
- Prevented row multiplication by deduplicating reviews to one row per order_id (kept latest review timestamp).
- Excluded canceled and unavailable orders, plus rows missing delivered date, from delivery delay analysis.
- Computed Days_Difference as order_estimated_delivery_date - order_delivered_customer_date.
- Classified deliveries as:
  - On Time: Days_Difference >= 0
  - Late: -5 <= Days_Difference < 0
  - Super Late: Days_Difference < -5

### Candidate's Choice Addition
- Added a Promise Accuracy Risk Monitor by state using late rate, average delay bias, average review score, and order volume.
- Built a state risk matrix to prioritize intervention where logistics risk and customer dissatisfaction intersect.
- Business Value: This moves decision-making from reactive reporting to proactive promise calibration and regional operations targeting.

### Translation Challenge (Portuguese to English Categories)
- Loaded `product_category_name_translation.csv` and mapped `product_category_name` to English category labels.
- Joined order items to products and translated categories, then linked item-level categories to delivery outcomes.
- Built an English-category performance table (late %, average delay, average review) and added category-level visuals to the dashboard.
- Furniture vs Electronics finding: Electronics/Tech late delivery rate was 8.23% versus 7.80% for Furniture/Home.
