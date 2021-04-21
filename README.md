# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Required data availability in CSV file( Includes readings and recorded timestamp)
3. Availability of CSV file on server
4. Permission to read available CSV file on server


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This is part of software being developed( Includes logic for converting data into PDF file
Counting the breaches       | Yes           | This is part of the software being developed (Assuming data is available in file then reading data and finding breaches)
Detecting trends            | Yes           | This is part of the software being developed (Assuming data is available in file with valid format then reading data and finding trends)
Notification utility        | Yes           | This is a one of the feature of software being developed

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "No Data Found" to the PDF when the CSV doesnt conatin any data
4. Write Count of Breaches to the PDF when the CSV have some reading which are crossing threshold
5. Write 0 as Breach Count when the CSV didnt having any reading which are crossing threshold
6. Write TimeStamp(Date & Time) Details when the CSV readings are increasing continuously.
7. Write "Not Available" in trends when there is no continuous reading increase available in CSV File.
8. Write "Success" for file stored when the generated file is stored in specified location of server every week.
9. Write "True" for notification sent when report is available and accordingly notifcation is triggered.



### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input                                  | Output                                                 | Faked/mocked part
|--------------------------|----------------------------------------|--------------------------------------------------------|---
Read input from server     | csv file                               | internal data-structure                                | Fake the server store
Validate input             | csv data                               | valid / invalid                                        | None - it's a pure function
Notify report availability | PDF File availabilty check             | Notification Message Sent                              | fake the notification call
Report inaccessible server | Server Path For CSV File               | Unable to access req. file                             | Fake the File access call of server
Find minimum and maximum   | CSV File                               | Minimum & Maximum Reading                              | None - it's a pure function
Detect trend               | CSV File                               | Trend TimeStamp Details                                | None - it's a pure function
Write to PDF               | Readings which needs to record in file | PDF file with recorded reading inside it               | Fake the PDF write call with fake path
