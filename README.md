# YouTube Trending Videos Analysis

This project explores YouTube trending-video data using Excel and Power BI. It includes exploratory data analysis and data cleaning by Excel. PowerBI was used to build two dashboards that display the formatted data.

## Project contents

| Path                           | Description                                                       |
| ------------------------------ | ----------------------------------------------------------------- |
| `youtube views dataset/`       | Original CSV data packs, with CAvideos being the data source used |
| `youtube views.xlsx`           | Excel workbook with exploratory analysis and summary tables.      |
| `youtube views dashboard.pbix` | Interactive, two-page Power BI report.                            |
| `images/`                      | Screenshots of the Excel EDA and Power BI report pages.           |

## Data fields

The regional CSVs share the same 16 fields:

| Field                    | Description                                                                                  |
| ------------------------ | -------------------------------------------------------------------------------------------- |
| `video_id`               | YouTube video identifier.                                                                    |
| `trending_date`          | Date the video appeared in the trending data.                                                |
| `title`                  | Video title.                                                                                 |
| `channel_title`          | Channel name.                                                                                |
| `category_id`            | Region-specific category identifier; use the matching JSON file to look up category details. |
| `publish_time`           | Video publication timestamp.                                                                 |
| `tags`                   | Video tags.                                                                                  |
| `views`                  | Recorded view count.                                                                         |
| `likes`                  | Recorded like count.                                                                         |
| `dislikes`               | Recorded dislike count.                                                                      |
| `comment_count`          | Recorded comment count.                                                                      |
| `thumbnail_link`         | Thumbnail URL.                                                                               |
| `comments_disabled`      | Whether comments were disabled.                                                              |
| `ratings_disabled`       | Whether ratings were disabled.                                                               |
| `video_error_or_removed` | Whether the video was unavailable or removed.                                                |
| `description`            | Video description.                                                                           |

## Processing done in Excel

There were also added multiple columns by using PowerQuery inside Excel:

- `like_rate` : made from dividing likes by views
- `dislike_rate` : made from dividing dislikes by views
- `comment_rate` : made from dividing comment count by views
- `engagement_rate` : made from the sum of like count and comments count, divided by views

The original CSVs only included the category id, without the category title. The category title was added using a MERGE LEFT JOIN query on the processed table, with the values from the json file.

## Excel EDA

The workbook contains an exploratory analysis of video performance and interaction counts. The EDA was done only on the `CAvideos` csv / table. The analysis includes:

- Unique-video and comment-availability counts.
- Mean and median like, dislike, comment, and engagement rates.
- Total views by category.
- Descriptive statistics for views, likes, dislikes, and comments, including quartiles, interquartile range, skewness, and minimum/maximum values.
- Charts comparing average and median interaction rates and summarizing the distributions of interaction counts.

![Excel EDA charts](images/graphs%20eda%20excel.png)

![Excel EDA summary table](images/table%201%20eda%20excel.png)

![Excel interaction-count tables](images/table%202%20eda%20excel.png)

## Power BI dashboard

Open `youtube views dashboard.pbix` in Power BI Desktop to use the interactive report. The report has two pages:

1. **YouTube Video Analytics** — KPI cards for video count, total views, and average like, comment, and engagement rates. Filters include trending date, category, channel, and whether comments are disabled. Charts compare views and engagement over time, show category distribution and category engagement, and rank channels by views.
2. **Video details and publishing patterns** — a top-10-by-views table with channel, category, and interaction rates; a views-versus-engagement scatter plot; and a heatmap of trending-video counts by publish weekday and hour.

![Power BI overview page](images/page%201%20dashboard%20powerbi.png)

![Power BI video detail page](images/page%202%20dashboard%20powerbi.png)

## Engagement measures

The interaction rates explored in the project are:

- **Like rate** = likes / views
- **Dislike rate** = dislikes / views
- **Comment rate** = comment count / views
- **Engagement rate** = (likes + comment count) / views

These are interactions relative to recorded views; they are not rates based on impressions or unique viewers. The workbook and report may summarize row-level rates differently from a rate calculated from aggregate totals.
