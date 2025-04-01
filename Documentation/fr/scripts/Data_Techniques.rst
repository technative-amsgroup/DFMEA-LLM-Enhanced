Data Collection Techniques used in this project
====================================
- :doc:`webscraping`
- Surveys and questionnaires
- Interviews
- Observations
- Focus groups
- Experimentation
- Sensor data collection
- Social media monitoring

. **HTTP Requests**: Web scraping starts with sending HTTP requests to the target website. This can be done using libraries like `requests` in Python.

2. **HTML Parsing**: Once the web page is fetched, the HTML content needs to be parsed to extract the relevant data. Libraries like `Beautiful Soup` or `lxml` can be used for this purpose.

3. **Locating Elements**: Web scraping often requires locating specific elements within the HTML structure, such as tags, classes, or IDs. CSS selectors or XPath expressions can be used to identify these elements.

4. **Data Extraction**: After locating the desired elements, the data can be extracted using various methods. This may involve extracting text, attributes, or even navigating through nested elements.

5. **Handling Dynamic Content**: Some websites use JavaScript to load content dynamically. To scrape such websites, you may need to use tools like `Selenium` or `Scrapy` that can interact with JavaScript-driven pages.