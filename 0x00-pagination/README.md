# 0x00. Pagination

## Resources
Read or watch:
- [REST API Design: Pagination](https://restfulapi.net/rest-api-design-pagination/)
- [HATEOAS](https://en.wikipedia.org/wiki/HATEOAS)

## Learning Objectives
At the end of this project, you are expected to be able to explain to anyone, without the help of Google:
- How to paginate a dataset with simple `page` and `page_size` parameters
- How to paginate a dataset with hypermedia metadata
- How to paginate in a deletion-resilient manner

## Requirements
- All your files will be interpreted/compiled on Ubuntu 18.04 LTS using `python3` (version 3.7)
- All your files should end with a new line
- The first line of all your files should be exactly `#!/usr/bin/env python3`
- A `README.md` file, at the root of the folder of the project, is mandatory
- Your code should use the `pycodestyle` style (version 2.5.*)
- The length of your files will be tested using `wc`
- All your modules should have documentation (python3 -c 'print(__import__("my_module").__doc__)')
- All your functions should have documentation (python3 -c 'print(__import__("my_module").my_function.__doc__)')
- A documentation is not a simple word, it’s a real sentence explaining what’s the purpose of the module, class, or method (the length of it will be verified)
- All your functions and coroutines must be type-annotated.

## Setup
Download the dataset `Popular_Baby_Names.csv` from [here](https://data.cityofnewyork.us/Health/Popular-Baby-Names/25th-nujf) and use it for your project.

## Tasks

### 0. Simple pagination
Create a function `index_range(page: int, page_size: int) -> Tuple[int, int]:`
- The function should return a tuple of size two containing a start index and an end index corresponding to the range of indexes to return in a list for those particular pagination parameters.
- Page numbers are 1-indexed, i.e. the first page is page 1.

### 1. Simple pagination (cont)
Create a class `Server` that:
- Is initialized with a dataset, which is a list of dictionaries
- Implements a method `get_page` that takes two integer arguments `page` with default value 1 and `page_size` with default value 10.
- This method should return a list of baby names for the corresponding page.

### 2. Hypermedia pagination
Modify the `get_page` method to return a dictionary with the following key-value pairs:
- `page_size`: the length of the returned dataset page
- `page`: the current page number
- `data`: the dataset page
- `next_page`: the number of the next page, or `None` if no next page
- `prev_page`: the number of the previous page, or `None` if no previous page
- `total_pages`: the total number of pages in the dataset as an integer

### 3. Deletion-resilient hypermedia pagination
Modify the `get_page` method to implement deletion-resilient pagination by maintaining an index in a separate file or a database table to track the starting points of pages.

### Example: `pagination_example.py`
```python
#!/usr/bin/env python3
"""
Example module demonstrating pagination
"""

from typing import List, Tuple, Dict
import csv

def index_range(page: int, page_size: int) -> Tuple[int, int]:
    """
    Return a tuple of size two containing a start index and an end index
    corresponding to the range of indexes to return in a list for those
    particular pagination parameters.
    """
    start = (page - 1) * page_size
    end = page * page_size
    return start, end

class Server:
    """Server class to paginate a dataset of popular baby names."""
    DATA_FILE = "Popular_Baby_Names.csv"

    def __init__(self):
        self.__dataset = None

    def dataset(self) -> List[Dict]:
        """Cached dataset"""
        if self.__dataset is None:
            with open(self.DATA_FILE) as f:
                reader = csv.DictReader(f)
                self.__dataset = [row for row in reader]
        return self.__dataset

    def get_page(self, page: int = 1, page_size: int = 10) -> Dict:
        """
        Return a page of the dataset.
        """
        assert isinstance(page, int) and page > 0
        assert isinstance(page_size, int) and page_size > 0

        dataset = self.dataset()
        start, end = index_range(page, page_size)
        data = dataset[start:end]

        total_pages = len(dataset) // page_size + (len(dataset) % page_size > 0)
        
        return {
            "page_size": len(data),
            "page": page,
            "data": data,
            "next_page": page + 1 if end < len(dataset) else None,
            "prev_page": page - 1 if start > 0 else None,
            "total_pages": total_pages
        }

if __name__ == "__main__":
    server = Server()

    # Simple pagination example
    print(server.get_page(1, 10))

    # Pagination with hypermedia metadata example
    print(server.get_page(2, 10))

