# pythonlab3
## Product info
Here is browser page of my example product
<img width="1225" height="685" alt="Screenshot 2025-12-18 231359" src="https://github.com/user-attachments/assets/6c6bc5f0-1a4b-467f-a7b7-40ebc83c79c8" />
and its links are - https://www.amazon.com/Batman-Special-Figures-Anniversary-Collectible/dp/B0CSYH7K31/ref=pd_rhf_gw_s_pd_sbs_rvi_d_sccl_1_14/144-4722195-4305801?pd_rd_w=vwXzn&content-id=amzn1.sym.6640a844-ab24-4352-ac9b-78899e683a5e&pf_rd_p=6640a844-ab24-4352-ac9b-78899e683a5e&pf_rd_r=1ZXX2BTQSAXVDZ3VS6RX&pd_rd_wg=JV2ft&pd_rd_r=5d231db7-49fa-46f4-b378-642db036280f&pd_rd_i=B0CSYH7K31&psc=1
or https://www.amazon.com/dp/B0CSYH7K31
## Code (script.py)
```
import requests
from bs4 import BeautifulSoup

url = "https://www.amazon.com/dp/B0CSYH7K31"

headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36",
    "Accept-Language": "en-US,en;q=0.9",
    "Accept-Encoding": "gzip, deflate, br",
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
    "DNT": "1",
    "Connection": "keep-alive",
    "Upgrade-Insecure-Requests": "1"
}

try:
    r = requests.get(url, headers=headers)
    r.raise_for_status()  # Check for HTTP errors

    soup = BeautifulSoup(r.content, "html.parser")

    # Try different selectors for Amazon
    title_tag = soup.find("span", id="productTitle")
    if not title_tag:
        title_tag = soup.find("h1", id="title")

    price_tag = soup.find("span", class_="a-offscreen")
    if not price_tag:
        price_tag = soup.find("span", class_="a-price-whole")

    if title_tag:
        title = title_tag.text.strip()
        print("Product:", title)
    else:
        print("Title not found")

    if price_tag:
        price = price_tag.text.strip()
        print("Price:", price)
    else:
        print("Price not found - Amazon may have blocked the request")

except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
```
## Terminal
<img width="1565" height="139" alt="Screenshot 2025-12-18 232215" src="https://github.com/user-attachments/assets/b0d52b6d-5af5-4b75-a394-555cc8efa7d2" />

