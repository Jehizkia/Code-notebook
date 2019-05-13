# Python Notes

### Logging template
```py
import logging
import sys

LOG_FORMAT = '%(levelname)s %(asctime)s - %(message)s'
logging.basicConfig(filename='../recsys.log', level=logging.DEBUG, format=LOG_FORMAT)
logging.getLogger().addHandler(logging.StreamHandler())
logger = logging.getLogger(__name__)

handler = logging.StreamHandler(sys.stdout)
handler.setLevel(logging.DEBUG)
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
handler.setFormatter(formatter)
logger.addHandler(handler)
```

### Scraping method
```py
import requests
from bs4 import BeautifulSoup

def retrieve_page(self, url: str):
    page_response = requests.get(f'{url}{self.parameter}', cookies=self.cookies)
    return BeautifulSoup(page_response.content, "html.parser")

```

Usage in other file
```py
import logging

logger = logging.getLogger(__name__)

logging.info('Your log message')
```

### Single line if else
```py
'Yes' if fruit == 'Apple' else 'No'
```
