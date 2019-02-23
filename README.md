# PowerBIemail
A power bi template file, that allows to connect to an o365 email account and uses Power BI techniques and Azure Cognitive Services to find insights that are buried in your inbox.

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
Here you can provide the appKey to the textAnalytics part of the Cognitive Services. If you are not that much experienced with Cognitive Services especially with the pricing, I recommend that you pause a moment and start reading here:
#### endpointTextAnalyticsKeyPhrases
#### o365Account
#### 0365InboxPath
