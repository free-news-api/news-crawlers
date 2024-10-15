# Open Source News Crawlers - A Comparative Review

This document provides an overview and detailed comparison of several open-source news crawlers, each offering unique functionalities for news scraping, extraction, and analysis.

## Overview

We will be reviewing the following open-source news crawlers:

- [newspaper4k (AndyTheFactory/newspaper4k)](#newspaper4k-news-crawler)
- [news-crawl (commoncrawl/news-crawl)](#commoncrawl-news-crawl)
- [news-please (fhamborg/news-please)](#news-please)
- [fundus (flairNLP/fundus)](#fundus-news-crawler)
- [news-crawler (LuChang-CS/news-crawler)](#luchang-cs-news-crawler)
  


---

## Full Reviews


# [Newspaper4k News Crawler](https://github.com/AndyTheFactory/newspaper4k) 

## Overview:
Newspaper4k is a Python-based news scraper and article extractor, serving as a continuation of the Newspaper3k project, which ceased updates in 2020. It improves on its predecessor by adding new features and fixing numerous issues. Newspaper4k provides tools for scraping individual articles or entire news sources, handling metadata like authors, publish dates, top images, and more. Additionally, it supports multiple languages, multithreading, and even Google News integration, making it a versatile and updated option for web scraping.

## Key Features:
1. **Multithreading for Faster Article Downloading:** Utilizes Python's ThreadPoolExecutor for faster downloading of articles from news sources.
2. **Command-Line Interface (CLI) Support:** Allows users to easily scrape articles via the command line.
3. **Python API for Flexibility:** Includes a robust Python API for scraping single or multiple articles, with simple calls to fetch metadata, article text, images, etc.
4. **Multilanguage Support:** Supports over 80 languages with auto-detection, allowing for seamless scraping from global news websites.
5. **Google News Integration:** Supports Google News scraping, enhancing its coverage of news sources.
6. **NLP Integration:** Automatically extracts keywords and generates article summaries.
7. **Wide Output Format Support:** Offers output in various formats such as JSON, CSV, and text files, making the data easy to process.

## Evaluation:
Newspaper4k has demonstrated significant improvements over its predecessor, particularly in accuracy and performance, as shown in various benchmarks like the Scraperhub and Newspaper Article Extraction Benchmark.

## Benchmarks:
| **Version**        | **Corpus BLEU Score** | **Corpus Precision Score** | **Corpus Recall Score** | **Corpus F1 Score** |
|--------------------|-----------------------|----------------------------|-------------------------|---------------------|
| **Newspaper3k 0.2.8** | 0.8660                | 0.9128                     | 0.9071                  | 0.9100              |
| **Newspaper4k 0.9.0** | 0.9212                | 0.8992                     | 0.9336                  | 0.9161              |
| **Newspaper4k 0.9.3** | 0.9531                | 0.9585                     | 0.9339                  | 0.9460              |

## Pros:
- **Highly Accurate:** Based on its benchmarks, Newspaper4k performs exceptionally well in article extraction accuracy.
- **Easy Transition from Newspaper3k:** The project maintains backward compatibility with Newspaper3k, making migration seamless for existing users.
- **Comprehensive Feature Set:** Supports article metadata extraction, summaries, and even top image extraction from the HTML.
- **Community Support & Development:** It is actively maintained, with contributions from multiple developers and community members.

## Cons:
- **Complexity in Setting Up:** Requires installation of several dependencies such as Python dev tools, libxml2, and Pillow, which might be cumbersome for non-expert users.
- **Long Download Times for Large Sources:** Downloading many articles from a large source (like CNN) can take a significant amount of time, and IP blocking by the news site could occur.
- **Still Some Open Issues:** Despite improvements, there are still over 180 issues to be addressed.

## Conclusion:
Newspaper4k is a powerful and highly customizable news crawler. Its multithreading, multilanguage support, and integration with NLP for article summarization and keyword extraction make it stand out. It’s a suitable tool for users who need to scrape large volumes of news articles and organize them with metadata. However, users must be prepared to install dependencies and face potential challenges when scraping large websites.



## Findings Table:

| **Aspect**                    | **Findings**                                                                                                                                                                  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Backward Compatibility**     | Fully compatible with Newspaper3k's API, allowing for easy transition from the older version.                                                                                 |
| **Multithreading Support**     | Utilizes Python's ThreadPoolExecutor for faster article downloads, configurable with custom thread counts.                                                                     |
| **Language Support**           | Supports over 80 languages with auto-detection capabilities, essential for accurate scraping of non-English news sources.                                                      |
| **Google News Integration**    | Special integration for scraping articles from Google News using the GoogleNewsSource class.                                                                                  |
| **NLP Capabilities**           | Includes keyword extraction and automatic article summaries using natural language processing.                                                                                |
| **CLI and Python API**         | Offers both command-line interface (CLI) and Python API for flexible usage.                                                                                                   |
| **Benchmark Performance**      | Shows significant improvement in BLEU, Precision, Recall, and F1 scores in various benchmarks over Newspaper3k.                                                               |
| **Dependencies**               | Requires several system packages like libxml2, libxslt, and Pillow for image extraction, which could make setup complex for beginners.                                         |
| **Drawbacks**                  | Potential for long download times and IP blocking when scraping large websites; also, 180+ issues still open for verification.                                                 |
| **Use Cases**                  | Ideal for large-scale article scraping, metadata extraction, and multi-language news sources. Works well for media monitoring, content curation, and academic research.       |

---

# [CommonCrawl News-Crawl](https://github.com/commoncrawl/news-crawl)

## Overview
**CommonCrawl's News-Crawl** is an open-source, distributed web crawler built using **StormCrawler**. It is designed to gather news articles from various websites by utilizing **RSS/Atom feeds** and **news sitemaps**. The crawler stores the fetched content in **WARC (Web ARChive)** format, which is part of the **Common Crawl dataset**. This data can be accessed through the AWS Open Data Set. 

## Key Features

- **Distributed Architecture**: Built on **StormCrawler**, providing scalability for large-scale news crawling.
- **Customizable Crawling**: Configure the crawler via `crawler-conf.yaml` to set user agents and other HTTP header properties. News feeds and sitemaps are specified in the seed files.
- **Elasticsearch Integration**: The crawler uses **Elasticsearch** to track URL status and provides APIs for adding, removing, or re-fetching URLs.
- **Real-time Monitoring**: Integration with **Kibana** allows real-time monitoring of the crawling process using dashboards. Additionally, command-line utilities provide detailed status reports.
- **Flexible Deployment**: Run locally or inside Docker containers. Supports easy monitoring and management of Elasticsearch indices.
- **WARC Output**: Stores the output as **WARC files**, a standard format for web archiving, which can be accessed for long-term research and analysis.

## Technical Requirements

- **Java 8**
- **Elasticsearch 7.5.0**
- **Apache Storm 1.2.4**
- **Kibana** (optional, for monitoring)

## Setup Instructions

1. **Install Dependencies**:
   - Install **Java 8**, **Elasticsearch 7.5.0**, and **Apache Storm 1.2.4**.
   - Optionally, install **Kibana** for monitoring the crawler process.
   
2. **Build and Run**:
   - Build the crawler's JAR file:
     ```bash
     mvn clean package
     ```
   - Launch the crawler:
     ```bash
     storm jar target/crawler-1.18.1.jar org.commoncrawl.stormcrawler.news.CrawlTopology -conf $PWD/conf/es-conf.yaml -conf $PWD/conf/crawler-conf.yaml $PWD/seeds/feeds.txt
     ```
   - The crawler will begin fetching news articles based on the seed URLs and generate WARC files in the specified directory.

3. **Docker Deployment**:
   - Build the Docker image:
     ```bash
     docker build -t newscrawler:1.18.1 .
     ```
   - Run the Docker container:
     ```bash
     docker run --net=host \
       -v $PWD/data/elasticsearch:/data/elasticsearch \
       -v $PWD/data/warc:/data/warc \
       --rm --name newscrawler -i -t newscrawler:1.18.1 /bin/bash
     ```

4. **Monitoring**:
   - You can monitor the crawling process in real-time using Kibana dashboards or by checking the URL status at `http://localhost:9200/status/_search?pretty`.
   - Use the provided command-line utility to get status counts:
     ```bash
     bin/es_status aggregate_status
     ```

## Configuration

- The default configuration works out of the box. However, you can customize the crawler by editing the `crawler-conf.yaml` file:
   - **User Agent**: Set the `http.agent.name` and other HTTP headers.
   - **Seed Files**: Modify the `feeds.txt` file to point to your desired news feeds and sitemaps.

## Monitoring and Control

- **Kibana Dashboards**: Set up dashboards to monitor crawling progress.
- **Elasticsearch API**: Use Elasticsearch to manage URLs, fetch counts, and control crawling status.
- **Command-line tools**: Use the `es_status` script to manage URLs and view status reports directly from the command line.

## Caveats

- **Site Support**: The crawler relies on RSS/Atom feeds and sitemaps. Adding support for sites without these features remains a challenge.
- **Port Conflicts**: Ensure that **Elasticsearch** port `9200` is not already in use by another instance to avoid conflicts.

## License

This project is licensed under the **Apache 2.0 License**. See the [LICENSE](LICENSE) file for more details.

## Summary Table

| **Category**           | **Details**                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------|
| **Primary Function**    | Crawling news articles and storing them as WARC files using RSS/Atom feeds and sitemaps         |
| **Technology Stack**    | Java 8, Elasticsearch 7.5.0, Apache Storm 1.2.4, Docker, StormCrawler                           |
| **Customization**       | Configurable via `crawler-conf.yaml`, seed files, and user agent properties                     |
| **Monitoring Tools**    | Kibana dashboards, Elasticsearch API, command-line utilities (`es_status`)                      |
| **Output Format**       | WARC files, stored in a user-defined directory                                                  |
| **Advantages**          | Distributed, scalable, easy to customize, real-time monitoring                                  |
| **Challenges**          | Limited support for sites without RSS/Atom feeds or sitemaps, manual configuration required     |
| **Deployment Options**  | Local installation or Docker container                                                          |
| **License**             | Apache 2.0                                                                                     |

## Contributors

- **Sebastian Nagel** ([@sebastian-nagel](https://github.com/sebastian-nagel))
- **Julien Nioche** ([@jnioche](https://github.com/jnioche))


---

# [News-please](https://github.com/fhamborg/news-please)

news-please is an open-source news crawler designed to extract structured information from a variety of news websites. It is versatile, user-friendly, and supports different modes of use, making it suitable for various use cases, including news archiving, sentiment analysis, and event extraction.

## Features and Functionality

| **Feature**                          | **Details**                                                                                                                                                                                                                                                |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Installation**                     | Simple installation using `pip` with support for Python 3.8+                                                                                                                                                                                              |
| **Supported Modes**                  | CLI mode for full website extraction and library mode for custom Python programs                                                                                                                                                                           |
| **Extraction Sources**               | Supports direct URLs, RSS feeds, internal hyperlinks, CommonCrawl archives                                                                                                                                                                                 |
| **Extracted Information**            | Extracts the headline, lead paragraph, main text, main image, author name(s), publication date, and language from articles                                                                                                                                 |
| **Storage Options**                  | JSON files, PostgreSQL, ElasticSearch, Redis                                                                                                                                                                                                               |
| **Article Versioning**               | Enables versioning to track changes when crawling articles multiple times                                                                                                                                                                                  |
| **Custom Configurations**            | Extensive configurations available via `config.cfg`, supports ElasticSearch, PostgreSQL, and Redis with custom authentication                                                                                                                              |
| **CommonCrawl Integration**          | Offers easy integration with CommonCrawl’s news archive, allowing filtered crawling by publisher or date                                                                                                                                                    |
| **Library Mode**                     | Allows integration within Python code, enabling customized article extraction with blocking functionality to wait until all URLs are processed                                                                                                              |
| **Export to JSON**                   | Articles can be exported to JSON format, providing a structured and usable data format for further processing                                                                                                                                            |
| **Use Cases**                        | News website crawling, archiving news articles, sentiment classification, event extraction, and more                                                                                                                                                        |
| **Documentation**                    | Extensive documentation available on GitHub, with contributions welcomed from the community                                                                                                                                                                |
| **Support and Contributions**        | Open for community contributions, bug reports, and GitHub discussions; individual support is available for a fee                                                                                                                                            |
| **Licensing**                        | Licensed under Apache 2.0, with clear terms for contributions and usage                                                                                                                                                                                    |

## Strengths

- **Versatility**: Supports various modes of use (CLI and library) and offers storage options with versioning.
- **CommonCrawl Integration**: The ability to extract from CommonCrawl’s extensive news archive is a valuable feature for accessing both small and large publishers.
- **Ease of Use**: Simple installation via `pip` and straightforward configuration files.
- **Comprehensive Data Extraction**: Extracts a broad set of attributes from news articles, which can be useful for various applications such as content analysis or archiving.
- **Customizability**: Provides extensive configuration options and allows users to store crawled data in different formats, such as JSON, PostgreSQL, ElasticSearch, or Redis.
- **Active Community**: Encourages contributions and collaboration through GitHub.

## Limitations

- **No Pre-built Releases**: Users must configure the system manually and set up crawlers, which may require technical expertise.
- **Resource Intensity**: Depending on the size of the news website and crawl depth, it may consume significant computational resources.
- **Limited Support**: While public discussions are encouraged, private support is available only for a fee.

## Use Cases

- **News Archiving**: Collect and store articles from any news website for future reference.
- **Sentiment Analysis**: Extract articles for further processing in sentiment classification or natural language processing tasks.
- **Event Extraction**: Useful for tasks like event detection by extracting essential elements such as who, what, when, where, why, and how.
- **Data Analytics**: Researchers can use the extracted data for analysis, including metadata like publication date and author information.

## Conclusion

news-please is a highly customizable and powerful news crawler that suits developers and organizations looking for flexible, structured news article extraction. Its ability to work with CommonCrawl, export data in multiple formats, and adapt to various storage solutions makes it ideal for large-scale news data collection and processing tasks.

## License

Licensed under the Apache 2.0 License. See the `LICENSE` file for more information.

---

# [Fundus News Crawler](https://github.com/flairNLP/fundus) 

Fundus is an open-source Python package developed at Humboldt University of Berlin, designed to facilitate the process of crawling news articles with minimal effort. It is especially useful for those looking to access online news articles, whether from live websites or archived datasets such as the CC-NEWS dataset.

## Key Features
- **Simplicity**: The design philosophy of Fundus is simplicity. With just a few lines of code, users can initiate crawls of English-language news articles from supported publishers or datasets like CC-NEWS.
  
- **Wide Coverage**: It allows users to crawl multiple publishers and news sources, and has a particular strength in crawling U.S. and U.K.-based news sites.
  
- **Static Crawler**: Fundus doesn't offer real-time dynamic crawling, but it works effectively with static sites, offering the flexibility to crawl large datasets with minimal setup.
  
- **CommonCrawl Integration**: For large-scale corpus creation, Fundus relies on CommonCrawl’s CC-NEWS dataset, which supports crawling vast amounts of articles quickly. The crawler supports optimizations like setting the number of processes for high performance.

- **Efficient**: With the ability to utilize multiple CPU cores and optimized bandwidth usage, Fundus allows users to perform intensive crawling tasks more efficiently than other tools in this space.

- **Benchmarking**: The benchmark data included in the documentation shows that Fundus achieves high levels of precision and recall when extracting text from articles, with an F1-score of 97.69%, outperforming other tools like Trafilatura, Boilerpipe, and jusText.

- **Customization**: Developers can easily add new publishers, and the project encourages community contributions to further extend its capabilities.

- **Licensing and Community**: Fundus is licensed under MIT, and there is a growing community around it, evidenced by active contributions, issues, and pull requests on its GitHub page.

## Performance Comparison Table

| **Crawler**     | **Precision** | **Recall**     | **F1-Score**    | **Version** |
|-----------------|---------------|----------------|-----------------|-------------|
| **Fundus**      | 99.89±0.57    | 96.75±12.75    | 97.69±9.75      | 0.4.1       |
| Trafilatura     | 93.91±12.89   | 96.85±15.69    | 93.62±16.73     | 1.12.0      |
| news-please     | 97.95±10.08   | 91.89±16.15    | 93.39±14.52     | 1.6.13      |
| BTE             | 81.09±19.41   | 98.23±8.61     | 87.14±15.48     | N/A         |
| jusText         | 86.51±18.92   | 90.23±20.61    | 86.96±19.76     | 3.0.1       |
| BoilerNet       | 85.96±18.55   | 91.21±19.15    | 86.52±18.03     | N/A         |
| Boilerpipe      | 82.89±20.65   | 82.11±29.99    | 79.90±25.86     | 1.3.0       |

## Strengths
- **High Performance**: Fundus scores higher in precision, recall, and F1 metrics compared to many other news scrapers, ensuring high-quality text extraction.
- **Ease of Use**: With quick start examples and detailed documentation, it's user-friendly even for those with minimal Python experience.
- **Community-driven**: Encourages open-source contributions, making it a dynamic and evolving tool.
  
## Weaknesses
- **Static Crawler**: While efficient for static sites, Fundus doesn't support real-time dynamic crawling, limiting its ability to handle highly dynamic or interactive content.
- **Limited Real-time Support**: Since it focuses on static crawling, it may not be suitable for applications needing real-time news updates.

## Conclusion
Fundus is an excellent choice for researchers or developers looking for a simple, efficient, and highly accurate tool to crawl news articles at scale. It is particularly well-suited for large dataset creation and works seamlessly with the CommonCrawl archive. However, those needing real-time crawling or dynamic site handling may need to look for other solutions.

---

# [LuChang-CS News Crawler](https://github.com/LuChang-CS/news-crawler) 

## Overview

The **LuChang-CS news crawler** is a Python-based tool designed to crawl news articles from major sources such as BBC News, Reuters, and The New York Times. Below is a structured review of the repository, including a summary of its strengths and areas of improvement.

## Strengths

1. **Simplicity**: The tool provides an easy way to scrape articles using Python with straightforward configuration files for each news source. This makes it approachable for developers familiar with Python.
2. **Modular Architecture**: The use of separate configuration and link extraction files for each news source allows easy customization and extension to other news outlets. Developers can add new sources by creating files that follow the repository's structure.
3. **Active Documentation**: The README file is clear, offering detailed information about the usage, requirements, and architecture of the crawler. It also provides links to external archives (e.g., BBC News archives), making it easy for users to access the relevant data.
4. **Extensibility**: The repository encourages extensibility by offering guidelines on adding new news sources, which adds to the potential longevity and flexibility of the tool.
5. **Resilient Crawler**: Includes retry mechanisms (e.g., network retries) to handle failures during crawling, improving the robustness of the tool.

## Areas for Improvement

1. **Outdated Code**: The last commit to the repository was three years ago, meaning that the code has not been actively maintained. For example, Reuters has discontinued their original archive, and the crawler has not been updated to reflect this. An updated approach to handling new site structures or archives is needed.
2. **Limited News Sources**: Although it supports three major news outlets, the list could be expanded. The modular structure makes this easy to do, but the repository doesn’t come with a broader range of pre-built news sources.
3. **No Automated Releases**: There are no releases or package versions available, making it harder to track changes or integrate this tool into automated workflows.
4. **Dependency on External Archives**: The BBC News archive, for example, is handled by an external party (@dracos), meaning the crawler relies on third-party data management, which could be a potential risk if those services stop functioning.
5. **Lack of Data Storage Flexibility**: The storage path and configurations are relatively simple but could benefit from integration with cloud-based storage solutions like AWS or Google Cloud for better scalability.

## Findings Table

| **Aspect**                  | **Rating**          | **Details**                                                                                  |
|-----------------------------|---------------------|----------------------------------------------------------------------------------------------|
| **Ease of Use**              | 8/10                | Clear instructions and straightforward configuration, suitable for Python developers.         |
| **Modularity**               | 9/10                | Excellent modularity with separate components for different news sources, easy to extend.      |
| **Maintenance**              | 4/10                | Last commit was 3 years ago, with no active releases. Several sites have not been updated.     |
| **Supported News Sources**   | 6/10                | Supports BBC, Reuters, and The New York Times, but could include more news sources.            |
| **Extensibility**            | 9/10                | Clear guidelines for adding more news sources.                                                |
| **Error Handling**           | 7/10                | Includes retry mechanisms but could be more robust in dealing with site structure changes.     |
| **Documentation**            | 8/10                | Detailed and well-organized README, but lacks documentation for potential integration methods. |
| **Scalability**              | 5/10                | Limited scalability; adding cloud integration for storage and crawling would improve it.       |
| **Community Support**        | 3/10                | Only 109 stars and 40 forks, indicating a small community of contributors.                    |
| **License**                  | Not specified       | No explicit information regarding licensing was found.                                        |

## Conclusion

The LuChang-CS news crawler is a solid foundation for a Python-based web scraping tool but is in need of updates to ensure compatibility with changing web structures and to expand its support for more news sources. Its modular design and extensibility are key strengths, but it could benefit from modernization, such as cloud storage integration, more frequent updates, and improved community engagement.

