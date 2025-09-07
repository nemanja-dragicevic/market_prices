# Market Analytics 

**Market Analytics** is an intelligent shopping assistant built with LangChain and LangGraph.
It helps users discover discounted products across multiple markets, categorizes them, and provides smart recommendations — from recipes to price-based suggestions — all delivered in a clean Excel report or directly via an agentic chat interface.

# Features 

**Data Collection & Categorization** 

The application pulls product discounts from  multiple markets via their public API. Retrieved products are then categorized in 2 stages: 

1. Uses previously saved product categorizations from the database and categorize using product name keywords + cosine similarity
2. Sends remaining uncategorized items to an LLM agent, which infers categories using website-provided labels

**Excel Report Generation**

Once all the products are categorized, an Excel file is generated with a separate sheet for each product category. Each sheet lists the products in that category to make browsing easier. The report is then automatically sent via email.

**🤖 Agentic Assistant**

The system includes an LLM-powered agent that answers user queries, divided into 3 categories:

1. product_nutrients 🥦 - Get detailed product information such as nutrients, vitamins, and characteristics.
2. recipes 🍳 - Generate personalized recipe recommendations based on discounted products and user requests.
3. recommendation ⭐
    - Recommends products that the user previously bought but are **now cheaper**.
    - Suggests **Top 3 products** per category among all discounted products.

**Example output**

1. Email Attachment: discounted_products.xlsx
    - Sheet: Voće i povrće → apples, bananas, oranges
    - Sheet: Meso → chicken breast, pork ribs
2. Agent Query Examples
    - Daj mi 5 recepata za dorucak → Jaja na oko sa povrćem, Zobena kaša sa voćem, Tost sa avokadom
    - Koji proizvodi imaju najvise vitamina C? → Voće i povrće, Sokovi, Zdrava hrana
    - Koje proizvode bi trebao da kupim trenutno na akciji?
         * 🛒 Products you already bought: The product "Zdravo mleko 2% 1l" is currently priced at 99.99 in Idea, which is cheaper than the previous price of 109.99 at Maxi. The price difference is 10.00, making it a better deal now at Idea.
         * 💡 Recommended products to buy: The product "Aza med lipov 700g staklo aza" is currently priced at 500.0, reduced from 917.62. It is cheaper at the market "Idea" with a price difference of 417.62.

# 🛠️ Tech Stack

- LangChain – for LLM orchestration.
- LangGraph – for state management and agent logic.
- Pandas – for product data processing.
- Scikit-learn – for cosine similarity categorization.
- SMTP – for sending reports via email.
- Excel (pandas + openpyxl) – for structured product reports.
