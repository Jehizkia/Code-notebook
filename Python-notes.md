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
