- 👋 Hi, I’m @yonash20
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
yonash20/yonash20 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import requests
from bs4 import BeautifulSoup

def search_vinted(query, max_price=None):
    url = "https://www.vinted.fr/vetements"
    params = {
        "search_text": query
    }
    if max_price:
        params["price_to"] = max_price

    response = requests.get(url, params=params)
    soup = BeautifulSoup(response.text, 'html.parser')

    items = []
    for item in soup.select('.item-box'):
        title = item.select_one('.item-box__title').text.strip()
        price = item.select_one('.item-box__price').text.strip()
        link = item.select_one('.item-box__image a')['href']
        items.append({
            'title': title,
            'price': price,
            'link': f"https://www.vinted.fr{link}"
        })
    
    return items

# Exemple d'utilisation
items = search_vinted("jeans", max_price=20)
for item in items:
    print(f"Title: {item['title']}, Price: {item['price']}, Link: {item['link']}")

