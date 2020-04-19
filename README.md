# Serverless Data Engineering Pipeline
By Ana B. Barcenas

This project reproduces a serverless data engineering project architecture that looks like this:

![Test_image_1](pipeline_architechture.png)

The pipeline above resembles the following steps:
1. A producer lambda is created via AWS Cloud9.
2. It is triggered by an Amazon CloudWatch Timer every minute to access a DynamoDB table.
3. Takes the entries from DynamoDB (in this case, the entries are names of companies) and put these names into Amazon Simple Queue Service (SQS).
4. SQS is triggered every time it receives a message and it will invoke a consumer lambda function.
5. The consumer lambda function will extract the first line of the Wikipedia result of each company name provided by SQS.
6. Once the text is taken from Wikipedia, the consumer lambda function performs named entity recognition and sentiment analysis on it via Amazon Comprehend.
7. Finally, the resulting entity recognition and sentiment analysis will be put as files within a table in an Amazon S3 bucket. It is possible to download the files in .csv form.
8. This pipeline will run every minute and it will scale instantaneously if there are new entries in the DynamoDB table. 

Sources: 
* https://www.youtube.com/watch?v=zXxdbtamoa4
* https://github.com/noahgift/awslambda
