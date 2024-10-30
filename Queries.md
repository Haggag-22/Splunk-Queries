# Queries

---

[Real World Queries](https://www.notion.so/Real-World-Queries-12d7438590b480ada996d3e89e381ca8?pvs=21)

[**Windows Registry**](https://www.notion.so/Windows-Registry-1017438590b4803c8a47e1aad5cb692d?pvs=21) 

- `fields`- extracts new fields and use + and - to add and remove fields
- `search` - search for keywords
- `dedup` - remove the duplicates and type next to command the field name
- `rename`- renames the field
- `table` - creates a table and write next to the command the fieldname
- `head` - returns the top 10 events entries by default using time instead if you specify a value
- `tail`- opposite of head
- `sort` - allows us to order the fields in ascending or descending order
- `reverse`- reverses the sorting
- `top` - returns frequent values for the top 10 events by count
- `top limit = 3` - return the top 3 values by count
- `rare` - opposite of top, we also can use limit
- `highlight` - shows the results in raw events mode with fields highlighted
- `stats avg(field)`- calculate the average of the given field
- `stats max(field)` -  return the maximum value from the specific field
- `stats min(field)` -  return the minimum value from the specific field
- `stats sum(field)` - return the sum of the fields in a specific value
- `stats count(field)` -  returns the number of data occurrences
- `chart count by User` - makes a chart and counts user
- `timechart function <fiekdname>` - returns the time series chart covering the field
- **`User:\s([\w\s]+)` - regex pattern to capture usernames**
- `stats count by signature |stats sum(count) as total_alerts`  - counts the sum signatures
- `dc(field)` - counts how many values are in a field
- `stats values(field)`- makes a list for values in a field
- `stats count by field | stats sum(count) by field` - counts values in the field of every value
- `where isnotnull(field)` - remove empty rows (spaces with no data)
- `fillnull value=”no data”` - fills the empty parts with this string
- `table field | stats count by field` - makes a table of the field and their counts
- `transaction maxspan=15m` - max time between all related events
- `transaction maxpause` - max time between each individual events
- `transaction startswith & endswith` - specify values to with them so you can get what is between them
- `eval` - this command evaluates any function you need to read it in your way
- `eval readable_time = strptime (_time, “%m/%d/%y/ %H:%M”)` - creates human readable time format
- `eval status_code = case((status ==404), “not found”` - creates this string for the status code 404
- `stats count(eval(status ==404)) as “number of not founds”` - counts the status 404
- `eval hash=md5(file) | table  file, hash`- creates hash field with  the MD5 hash of the files then tables it
- `where` - same as search
- `where field = value`- searches the value with their field
- `rex` - that is for regex
- `erex` - helps regex
- `rex field=_raw (?<field name you want>”regex from ChatGPT”)` - use AI and extract fields easier
- `inputlookup` -  searches the content of a lookup table
- `inputlookup peopleinfo.csv` - searches for field in the file
- `inputlookup peopleinfo.csv | geostats latfield=field_in_file longfield=field_in_file globallimiy=10 couny by email` - this will create a map that displays email sent from the specific longitude and latitude and count the emails, but all of this is based from the csv file and the file has to be added to Splunk from the lookup settings
- `outputlookup` - write information into a CSV file or KV-STORE database table
- `lookup productionfo.csv field OUTPUT description` - this will lookup the csv file and get the field from Splunk and then outputs the field description which is in the csv file, but we have to add the lookup file first from the lookup settings
- `iplocation field`  - add location from ip
- `geostats` - calculate functions to display on a cluster map
- `addtotals row=f col=t label=”Total Purchase” labelfield=longitude purchase` - this will create a box with this string and count the column of the purchase field and them together and display the sum of the purchase next to the string box |
- `$field$` - creates a token which the user can input in a dashboard and gets the selected values based on the input

## Hints

---

- Create workflows to link (Virus Total) and (Who Is Lookup) to your searches and save time
- Download CIM and learn more about it
- Extract fields and name them to get more specific results by going to extract fields
- Use the Splunk add on builder easier and from their you can use data models too and create field aliases and anything else
- We can create fields using the field aliases and create calculate fields that has numbers such as megabytes
- Edit Tags for fields you extract for making reading easier such as giving tags for event codes
- Use data models to make queries easier. Learn More!
- We can also color specific fields we want such as purchase with colors by going to the event types setting and editing the event
- We can also create macros to save our search by going to advanced search and also we can create arguments to pass the macro in the search with the user choice to search for a specific result so we have to create a token when we create a macro
- Use Chat GPT and regex101 websites to get ready regex commands
- Instead of doing stats count by action=purchase, we can do action=purchase before the stats count and then do the stats count without adding any extras
- Use format setting under the search bar to see the total of the columns if you  need instead of typing commands