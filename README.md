# Asynchronous-Web-Scraping-with-aiohttp-and- beautiful soup
import aiohttp
import asyncio
from bs4 import BeautifulSoup

async def fetch(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main(urls):
    async with aiohttp.ClientSession() as session:
        tasks = [fetch(session, url) for url in urls]
        htmls = await asyncio.gather(*tasks)
        for html in htmls:
            soup = BeautifulSoup(html, 'html.parser')
            print(soup.title.string)

urls = [
    'https://example.com',
    'https://example.org',
    'https://example.net'
]

asyncio.run(main(urls))
