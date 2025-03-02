# Web Scraping with BeautifulSoup

## 📌 Overview
This project demonstrates how to scrape websites using **BeautifulSoup** in Python. It extracts data such as text, links, and images from web pages and saves them for further analysis.

## ⚡ Features
- Extracts text content from webpages
- Retrieves all links on a webpage
- Downloads images from a website
- Handles relative and absolute URLs
- Supports custom headers for bypassing basic blocks

## 🛠 Technologies Used
- **Python 3**
- **BeautifulSoup 4**
- **Requests**
- **OS (for file handling)**

## 🚀 Installation & Setup
```bash
# Clone the Repository
git clone https://github.com/your-username/web-scraping-bs4.git
cd web-scraping-bs4

# Install Dependencies
pip install beautifulsoup4 requests
```

## 🔍 Usage
### Extract Text & Links
```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
headers = {"User-Agent": "Mozilla/5.0"}
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

# Extract page title
print("Title:", soup.title.text)

# Extract all links
for link in soup.find_all("a"):
    print(link.get("href"))
```

### Download Images
```python
import os
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
headers = {"User-Agent": "Mozilla/5.0"}
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

# Create a folder for images
os.makedirs("images", exist_ok=True)

img_tags = soup.find_all("img")
for img in img_tags:
    img_url = img.get("src")
    if img_url.startswith("http"):
        full_url = img_url
    else:
        full_url = url + img_url
    
    img_data = requests.get(full_url).content
    img_name = os.path.join("images", full_url.split("/")[-1])
    with open(img_name, "wb") as f:
        f.write(img_data)
        print(f"Downloaded {img_name}")
```

## 📂 Project Structure
```plaintext
web-scraping-bs4/
│── images/               # Folder for downloaded images
│── scraper.py            # Main script for scraping
│── requirements.txt      # Dependencies
│── README.md             # Documentation
```

## ⚠️ Legal & Ethical Considerations
- **Respect robots.txt**: Always check a website's `robots.txt` file before scraping.
- **Avoid Overloading Servers**: Use request delays to prevent excessive load.
- **Use for Educational Purposes**: Ensure compliance with website terms of service.

## 🤝 Contributing
Pull requests are welcome! Please open an issue to discuss any improvements or bug fixes.

## �� License
This project is licensed under the **MIT License**.

---
🚀 **Happy Scraping!**


