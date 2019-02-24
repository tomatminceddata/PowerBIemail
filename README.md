# PowerBIemail
A power bi template file, that allows to connect to an o365 email account and uses Power BI techniques and Azure Cognitive Services to find insights that are buried in your inbox.

Please be aware that I provide this Power BI template file as it is, it haas a reduced set of functionality in comparisone to the file I'm using. There is no dedicated plan to add new capabilities and new analysis. 

As I'm using this template for public talks about Power BI and natural language processing I will add to this template during the year. My next talk will be at Data Grillen in June 2019, so there is some to enhance this template with new analytical capabilities or add some architectural changes like changing the pipeline and start using all things Azure.

I'm using Key Phrase extraction, one of the functions provided by the text analytics capabilities of the Cognitive Services. If you might want to read more about this "concept". Here you will find an introduction with some Python code:

http://bdewilde.github.io/blog/2014/09/23/intro-to-automatic-keyphrase-extraction/

and of course what Microsoft is saying: 
https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-keyword-extraction


Don't miss a general introduction to the capabilities of Azure Cognitive Services, this can be found here https://azure.microsoft.com/en-us/services/cognitive-services/, and you should also get familiar with the pricing: https://azure.microsoft.com/en-us/pricing/details/cognitive-services/text-analytics/

Please be aware that Key Phrase extraction is just a part of the solution, so if you don't want to use it, you can carve this out and use the template without using Key Phrase extraction.
## Things to prepare in advance
As this PBIX reads its data from different sources, the emails from somewhere in the cloud, the stopwords from your local c drive, and mixes all this data to a fun melange, please be aware that you have to adjust privacy settings of the data sources. If you are not familiar with these settings, I strongly recommend that you pause for a while and start reading about the privacy settings of Power BI data sources. Be assured that I'm not reading your eamil content :-)

### Parameters
Some parameters are used, that will help to "adopt" this Power BI template to your needs.

#### pathStopWords
This parameter points to the file Stopwords.txt.
The value of this paraemter may look like this:
C:\@Stopwords\Stopwords.txt
Please be aware that this is a simplified solution. This solution just considers english stopwords. If you are dealing with multiple languages you have to consider multiple stopwords files and also cultural nuances can become important.
#### appKeyTextAnalytics
Here you have to place the application key. This key can be found on the overview page of your Azure text analytics page.  
#### endpointTextAnalyticsKeyPhrases

#### o365Account
#### 0365InboxPath
