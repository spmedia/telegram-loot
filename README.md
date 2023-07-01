# Telegram Loot

tl;dr - this script is a Telegram wizard 🧙🏽‍♂️ that hunts for intel. It saves the alerts and uploads the file and an alert to a Slack channel.

A fork of Telegram Trends by Tom Jarvis.

This is an analysis tool to explore and monitor sus cybercrime channels/groups on the Telegram chat platform. Please use this tool with caution as it does not have content moderation or filtering. You are responsible for the content that may be exported.

In short, this tool allows you to search all the channels you follow with a list of keywords/phrases and returns all matching results in various formats with graph visualisations. It also optionally downloads the media and thus can be used as a media search engine (currently some bugs with this feature - do not use as exhaustive media search tool).

I've just been modifying this for my own specific usage so sorry if it sucks. I think its a neat tool for CTI. My code is 🍝 and bad so beware.

###### Screenshot of tool in action
[![ss](https://i.imgur.com/xxEKkvl.png "Example result exploring hate speech during the Russian full-scale invasion of Ukraine")](https://i.imgur.com/xxEKkvl.png "asdffa")



##### Key Features
- This tool is designed to work with sockpuppets that follow many channels covering a particular topic.
- You can change your API details to use different accounts by editing the **api_values.txt** file.
- The tool is designed to work like Google Trends showing daily volume of key terms and map over time.
- Date filtering allows you to narrow a search into a shorter time period. If left blank, it automatically scales to the maximum range of the data.
- The tool uses Telegram search which means it is particularly good for Russian language searches and generally handles word endings well.
- Generates individual graphs for each key term.
- Generates aggregated graph showing all key terms in a search on the same graph for comparison.
- Compiles a report PDF that shows the graphs and prints the full code for auditing of data and validation of evidence.
- Outputs a TXT file summary including all the main stats, e.g, date run, channels searched, and relative volume per channel.
- Optional media download for results (this massively (like really massively) prolongs the time needed to run the tool)
- Downloaded media has filename channelid_postid so it is easy to find the original.



This script searches messages containing specified search terms in Telegram channels the user is a member of. It exports the search results in HTML/JSON/CSV formats, generates a report, and plots the message count per day.

It is designed to monitor trends of search terms in much the same way that Google Trends does. This can be very useful for identifying the emergence of hatespeech or discussion/narratives following certain events.

This current version does not do any significant adjustment to the data, for example, the graph does not display incidence of terms adjusted to the incidence of all messages. This means further analysis should be conducted to ensure that a sharp spike in terms is not confounded by a sharp spike in general activity. For this reason, the graph output should be treated as indicative of need for further research and statistical analysis.

This tool has been tested on English and Russian language search terms.

**WARNING:** This tool uses your list of followed groups as the list it searches from. It may include personal chats/groups. For the sake of OPSEC, it is recommended to use a burner account and follow only investigation-specific chats.

# Installation
Clone the tg-keyword-trends repository by running the following command in your terminal or command prompt:

```git clone https://github.com/spmedia/telegram-loot```

Navigate into the tg-keyword-trends directory:

```cd tg-keyword-trends```

Install the required Python dependencies using pip:

```pip install -r requirements.txt```

# Features
- Graph adjusts scale to oldest and newest posts.
- CSV generated for further processing.
- JSON output
- HTML file generated for opening links.
- Generates report documenting the key details of the scrape (date, channels accessed, etc) for auditability of findings.
- Media download

# Usage:

1. Add the search terms, one per line, into a .txt file. You will be prompted to enter the file location shortly.
2. Make sure you have your Telegram API details ready [https://my.telegram.org/auth]
3. The script will search through all the channels the user is a member of.
4. The search results will be exported as HTML and CSV files in a timestamped output folder.
5. The script will generate a report containing the search results for each channel.
6. The script will plot the message count per day for each search term in a graph and save it as an image.


# Functions:

- **retrieve_api_details**: Read API details from 'api_details.txt'.
- **check_search_terms_file**: Read search terms from 'search_terms.txt' or prompt the user to enter search terms.
- **create_output_directory**: Create a timestamped directory for storing output files.
- **print_colored**: Print text in specified color using the colorama module.
- **render_url**: Generate HTML code for a hyperlink using a URL and message text.
- **generate_report**: Generate a report containing search results for each channel.
- **plot_keyword_frequency**: Plot the message count per day for each search term in a graph.

# Tips:
- Due to the date filtering feature, this tool also works well as a Telegram search engine that allows date-filtered results. Simply run the search in the date window needed and open up the output html file for a list of messages that match and their links.
- The tool handles timezones automatically and adjusts for them. Be particularly careful when editing any section of the code relating to time and date formats as this was difficult to debug. 
- It is recommended that you create a dedicated Telegram account for each subject matter. This will allow you to target only relevant channels and removes noise. 
- You don't need to search singular and plural nouns separately as this is handled by Telegram's search, (generally speaking, for English and Russian language).

[![Demonstration of graph](https://user-images.githubusercontent.com/118008765/232030941-aa506853-48ba-4433-8abf-1ee454ea1e5b.png "Demonstration of graph")](https://user-images.githubusercontent.com/118008765/232030941-aa506853-48ba-4433-8abf-1ee454ea1e5b.png "Demonstration of graph")
*This image shows the useage of the various placenames for "Bakmut", including the old Soviet names. One use of this tool could be for validating the search terms used in OSINT research. As can be seen here, one may limit their collection potential if they only use the official current name for the city rather than past and controversial names too. *

# Dependencies:

- pandas~=2.0.0
- matplotlib~=3.7.1
- Telethon~=1.28.2
- colorama~=0.4.6
- Pillow~=9.5.0
- reportlab~=3.6.12
- numpy~=1.24.2
- pytz~=2023.3
- tqdm~=4.65.0

Python Version: Python 3.11 or higher
