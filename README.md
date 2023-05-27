# aam1
import requests
from bs4 import BeautifulSoup
import pandas as pd
import csv

#assign the URL to the variable url

url = 'https://www.census.gov/programs-surveys/popest.html'

#assign the result of a request of the page to the variable page with the request.get() method.

page = requests.get(url)
page
#parse html and creat BS object

page.text

soup = BeautifulSoup(page.text, 'html.parser')
#display parsed HTML and

print(soup.prettify())
#use for loop to search through HTML tags to find links and display

for link in soup('a', href=True):

    print(link.get('href'))

#name the displayed links

all_links = []

for link in soup('a', href=True):

    all_links.append(link.get('href'))

#send to csv - pandas
df = pd.DataFrame(all_links, columns=["Web Links"])
df.to_csv('Yanasheski_AAM1Task1.csv', index=False)
