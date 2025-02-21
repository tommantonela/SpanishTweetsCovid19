# SpanishTweetsCovid19
Companion repository for the data collection ["SpanishTweetsCOVID-19: A Social Media Enriched Covid-19 Twitter Spanish Dataset"](https://data.mendeley.com/datasets/nv8k69y59d/1).

This repository contains:
- *code*.
	- ``01-db-extraction``. Assuming that the tweets were rehydrated using ``Faking it!`` are now in a ``mongo`` db, the notebook provides the code to extract the information from the db and create the data collection files.
	- ``02-stats-computation``. Given the data collection files, the notebook provides the code to compute different statistics.
	- ``03-text-processing``. Given the tweets' text, the notebook provides the code to extract the ``Empath`` categories and ``SentiSense`` emotions.
	- ``04-chart-creation``. Given the files corresponding to the ``Empath`` categories and the emotions, create heatmaps and boxplots showing the prevalence of the categories across different timeframes.
- *heatmaps*. Heatmaps showing the daily prevalence of each included category. Darker colors indicate higher prevalence of the category. Heatmaps are organized by mental health (anxiety, depression, stress), emotions and crisis (all, preparedness, response, recovery, mitigation). Heatmaps are presented for different time spans: march-june (june was a breakpoing in Argentina's lockdown), march-october, monthly, and bi/tri-monthly.
- *boxplots*. Boxplots show the distribution of prevalence across months per involved category/emotion. Boxplots are organized by mental health (anxiety, depression, stress), emotions and crisis (all, preparedness, response, recovery, mitigation).
