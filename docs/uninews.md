# UniNews Documentation

## 1. Introduction

UniNews is a desktop application designed to aggregate news, announcements, and updates from universities into a single interface.

University information is often distributed across multiple sources, including RSS feeds, departmental websites, faculty announcements, and institution-wide news portals. As a result, students, researchers, and staff must frequently navigate several websites to remain informed.

UniNews addresses this problem by collecting content from multiple sources and presenting it through a unified desktop application.

The application is developed in Python using PyQt6 and follows a modular architecture that supports both RSS feeds and custom website scrapers.

---

## 2. Objectives

The primary objectives of UniNews are:

* Centralize university-related news.
* Reduce the effort required to monitor multiple websites.
* Provide a clean and modern desktop experience.
* Support extensibility through community-contributed scrapers.
* Enable offline access to previously retrieved articles.
* Provide configurable notifications for new content.

---

## 3. System Architecture

The system consists of five major components:

### User Interface Layer

Responsible for:

* Displaying articles
* Searching articles
* Filtering content
* Managing settings
* Presenting notifications

Implemented using:

* PyQt6

### Data Acquisition Layer

Responsible for collecting news from external sources.

Supports:

* RSS feeds
* Custom HTML scrapers

Implemented using:

* feedparser
* requests
* BeautifulSoup

### Scraper Framework

Provides a standardized mechanism for integrating new content sources.

Each scraper inherits from a common base class and returns articles in a unified format.

### Persistence Layer

Responsible for:

* Storing articles
* Storing settings
* Preventing duplicate entries

Implemented using:

* SQLite

### Notification Layer

Responsible for desktop notifications whenever new articles are discovered.

Implemented using:

* Plyer

---

## 4. Article Data Model

All sources are normalized into a common structure.

```python
{
    "university": str,
    "source": str,
    "title": str,
    "summary": str,
    "link": str,
    "published": str,
    "fetched_at": str,
    "image_url": str
}
```

This allows RSS feeds and HTML scrapers to be handled identically by the application.

---

## 5. RSS Feed Support

RSS feeds are defined in:

```text
data/feeds.json
```

Example:

```json
{
  "name": "MIT News",
  "type": "rss",
  "url": "https://news.mit.edu/rss/feed"
}
```

The RSS service retrieves entries and converts them into the internal article format.

---

## 6. Scraper Framework

Scrapers are located inside:

```text
scrapers/
```

Each scraper extends the abstract BaseScraper class.

Example:

```python
class ExampleScraper(BaseScraper):

    def scrape(self):
        return []
```

Scrapers are registered through:

```python
SCRAPER_REGISTRY
```

This design allows contributors to add support for new universities without modifying the rest of the system.

---

## 7. University of Macedonia Integration

The initial scraper implementation targets the University of Macedonia.

Supported sources include:

* Main university news
* Departmental announcements
* Faculty-specific news pages

The scraper supports multiple subpages and categorizes articles by source.

Examples:

* UoM Main News
* UoM Applied Informatics
* UoM Economics
* UoM Business Administration

This categorization enables filtering directly from the application interface.

---

## 8. Local Storage

UniNews stores information locally within:

```text
local_data/
```

Contents include:

### SQLite Database

Stores:

* Articles
* Sources
* Metadata

### Settings File

Stores:

* Theme preferences
* Refresh intervals
* Notification preferences
* Cache limits

---

## 9. Search and Filtering

The application provides:

### Global Search

Allows users to search:

* Article titles
* Article summaries
* Source names

### Source Filtering

Users may filter content by:

* University
* Department
* Individual source

This functionality is exposed through the sidebar navigation panel.

---

## 10. Notifications

The notification subsystem supports:

* Desktop notifications
* Keyword-based filtering
* Optional startup refreshes
* Periodic automatic refreshes

Users may define keywords that trigger notifications when matched within article content.

---

## 11. User Interface

The application follows a card-based design.

Key interface components include:

### Header

Displays:

* Application title
* Refresh controls

### Sidebar

Provides:

* University filtering
* Department filtering
* Search functionality

### Article View

Displays:

* Article image
* Title
* Source
* Publication date
* Summary

### Settings Dialog

Allows users to configure:

* Theme
* Refresh interval
* Notification preferences
* Cache settings

---

## 12. Extensibility

UniNews has been designed with extensibility as a primary goal.

New universities can be integrated through:

### RSS Feed Integration

Adding a new entry to:

```text
feeds.json
```

### Scraper Integration

Implementing:

```python
BaseScraper
```

and registering it within:

```python
SCRAPER_REGISTRY
```

No modifications to the user interface or database layer are required.

---

## 13. Future Work

Planned enhancements include:

* Additional university integrations
* Improved image caching
* Pagination support
* Plugin-based scraper loading
* OPML feed import/export
* Article bookmarking
* Automatic update checks
* Native Linux package distribution
* Cross-platform installers

---

## 14. License

UniNews is released under the GNU General Public License v3.0 (GPL-3.0).

The project is maintained as an open-source initiative and welcomes community contributions.

## Contributors

<a href="https://github.com/open-source-uom/UniNews/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=open-source-uom/UniNews" />
</a>
