# PowerBIemail
Here you will find a power bi template file, that allows to connect to an o365 email account and uses Power BI techniques and Azure Cognitive Services to find insights that are buried in your inbox.

Please be aware that I provide this Power BI template file as it is. Due to the course of this year I will add new analytical capabilities in preparation of my speakings. 

As I'm using this template for public talks about Power BI and natural language processing I will add to this template during the year. My next talk will be at Data Grillen in June 2019, so there will be some enhancements to this template with new analytical capabilities or architectural changes like changing the pipeline and start using all things Azure.

I'm using Key Phrase extraction, one of the functions provided by the text analytics capabilities of the Cognitive Services. If you might want to read more about this "concept". Here you will find an introduction with some Python code:

http://bdewilde.github.io/blog/2014/09/23/intro-to-automatic-keyphrase-extraction/

and of course what Microsoft is saying: 
https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-keyword-extraction


Don't miss a general introduction to the capabilities of Azure Cognitive Services, this can be found here https://azure.microsoft.com/en-us/services/cognitive-services/, and you should also get familiar with the pricing: https://azure.microsoft.com/en-us/pricing/details/cognitive-services/text-analytics/

Please be aware that Key Phrase extraction is just a part of this solution, if you don't want to use it, you can carve this out and use the template without using this.

This tutorial https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/tutorials/tutorial-power-bi-key-phrases explains in great detail how to integrate Cognitive Services with Power BI.

# Things to prepare in advance
As this PBIX reads its data from different sources, the emails from somewhere in the cloud, the stopwords from your local c drive, and mixes all this data to a fun melange, please be aware that you have to adjust privacy settings of the data sources. If you are not familiar with these settings, I strongly recommend that you pause for a while and start reading about the privacy settings of Power BI data sources. Be assured that I'm not reading your eamil content :-)

Some parameters are used, that will help to "adapt" this Power BI template to your needs.

## pathStopWords
This parameter points to the file Stopwords.txt.
The value of this paraemter may look like this:
C:\@Stopwords\Stopwords.txt
Please be aware that this is a simplified solution. This solution just considers english stopwords. If you are dealing with multiple languages you have to consider multiple stopwords files and also cultural nuances can become important.
## appKeyTextAnalytics
Here you have to place the application key. This key can be found on the overview page of your Azure text analytics page. For the beginning I recommend that you omit this Parameter, and ignore all the errors. This will help to safe money, even if the usage of the Cognitive Services is worth all of it (but this is just my personal point of view).

If you omit this and/or the next parameter. The custom function will not work (of course, but there will also no costs :-)

## endpointTextAnalyticsKeyPhrases
This points to the endpoint of the Key Phrases api and may look like this:
https://northeurope.api.cognitive.microsoft.com/text/analytics/v2.0/keyPhrases

If you are going to publish your solution to Power BI service, make sure you create the Cognitive Services resource in the same region where your Power BI service is located.
## o365Account
This is just the email account you want to use. Please be aware that this solution relies on the following: the email account is a o365 account.
## 0365InboxPath
This provides an initial filter to one of your folders in your inbox and may look like this "\inbox\just a few emails\" (without the quotation marks). This helps a lot to get familiar with the solution.
# Things you might find interesting
## Removal of Stopwords
The Mail query contains a step "Remove stopWords from textBody", this step leverages the M function List.RemoveMatchingItems to remove the entries inside a list (the stopwords) from another list (the email body). The column that contained the email body has been duplicated and then the values have been transformed into a list by using the "Split column by ..." transformation.
## Finding words of interests
The step "Remove stopWords from textBody" uses the function "List.Accumulate" (one of the more mysterious M functions) to create a comma separated string from the words of the table "_whitewords" that are contained in the list of words of the email body. Basically you can imagine the function List.Accumulate as an iterator function that adds something to a list if a given condition is met.
## Multivalue fields and relationship modeling
As there are many multivalue fields inside the fact table, it's necessary (at least from my point of view) to treat these fields in a special way. I create intermediate tables for each multivalue fiels by using the function Table.SelectColumns() as a source, then I remove all the duplicate values. I call these tables "bridge ...". These tables should be hidden from the report view. As another step I create another step that references the bridge table, duplicate the column, rename this column properly and split this column by delimiter (,) into new rows.
## Invoking a custom function to extract Key Phrases
There is a custom function that calls the Key Phrases endpoint from the Azure Cognitive Services. This function is used inside the Mail query. You might find the function, the function usage, and also the try/otherwise exception handling if the function returns an error, due to missing or incorrect parameters.