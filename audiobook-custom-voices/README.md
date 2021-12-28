A distributed processing system for users to upload text files for books and generate an audiobook recording using custom voices for individual characters/narrator. 


=== Architecture ===
Users will upload a text of a book to a S3 bucket. After the uploaded is complete a notification will be sent from S3 -> SQS, Simple Queueing Service

SQS will push to lambda function, 
**lambda function will lable the text file for the current speaker
**This lambda function will need to lable the speaker using sentence structure/clues (e.g. Johnny said, "ipsum lorem". He then said, "lorem ipsum". The "He" would be referring to "Johnny")

After the lambda function finishes processing it will then send a processing complete notification and insert into a processed-text S3 bucket

Output will be pulled from the processed-text bucket and sent to Amazon Polly for transcribing text to speech. (since multiple types of Polly voices are being used, it may need to be sent in pieces and then stitched together)

completed audio file is sent back to the customer, can use a SNS notification that it is complete