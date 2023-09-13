

```
index=web categoryId=* | dedup categoryId | stats list categoryId)
```
```
index=web  | stats count by referer_domain, action | stats sum (count) by referer_domain
```

```
index-security stats values (user) as "Login Name", count (user) as "Attempts" by src fillnull value="no data available"
```
```
index=security stats lalues (user) as "Login Name" count (user) as 'Attempts" by sre
```
```
index=security | stats count by sr, user, action
```
￼

### Transaction commands

Group into associated fields

maxspan : Max time between all related events Ex: maxspan=15m

maxpause : Max time between each individual event Ex: maxpause=1m

startswith & endswith : Set your variables Windows EventIDs Ex: startswith=4624 endswith=4647


```
index=web
transaction clientip maxspan=10m maxpause=3s endswith-purchase
eval duration =tostring (duration, "duration")
table clientip, duration, action
```

```
index= internal
eval epoch_time = strptime (_time, "%s")
eval human_readable_time = strftime(epoch_time, "%m/%d/%y")
table _time, epoch_time, human_readable_time
```

```
eval epoch_time = strptime(_time, "%s".
eval human_readable_time = strftime(epoch_time, "%m/%d/%y %H: %M")
table _time, epoch_time, human_readable_time
```

```
index=_internal I eval DayofTheYear =strftime(_time, "%j") search DayofTheYear=206
```

```
index=web | eval status_codes =
case(
  (status ==404), "not found", 
  (status ==400), "bad request response"
)
stats count by status, status_codes
```
###  where 
```
index=security
table src, user, action
where src="64.66.0.20"
```
###   where   search like
```
index=security
table src, user, action
where like(src, "64.%")
search user=inet
```
###  inputlookup, lookup stats, where sort timechart 

```
inputlookup peopleinfo.csv   index=web action=purchase
lookup productinfo. cv productId OUTPUT description
stats count by productId description
where isnotnull(productId)
sort - count  index=web
where isnotnull(action)
timechart count by action 
```
```
index=web
lookup productinfo. cv productId OUTPUT description
where isnotnull(productId)

chart count over host by description
```

```
index=security eventtype=failed_login
timechart count by user useother=f usenull=f limit=5
```
```
index=_internal sourcetype=splunkd | timechart count I trendline sma5 (count) as "Our Moving Average of Total Events"
```
```
inputlookup peopleinfo.csv | iplocation ip_address
```
```
inputlookup peopleinfo.csv | geostats latfield=lat longfield=long globallimit=10 count by email
```
# Adding  Totals  and labels

```
index=web action=purchase
| iplocation src
| geostats count by action
| addtotals row=f col=t label="Total Purchases" labelfield=longitude purchase

```

### What are reports?
 
	A saved search : Anything that is a search can be saved as a report

	Live results : Re-run a report, or set it to run on a schedule

	Sharable Knowledge Object
		Let anyone view your reports, or add them to a dashboard for people to reference Ex: Audit_Report_LicenseUsage
 

###  Drilldown Functionality
	Actions
		-Link to search
		-Link to dashboard
		-Link to report

	$tokens$ : Tokens play a key role in passing variables from panel to panel

	Export : Export as a PDF, print, or include in a report

```
index=_internal log_level=* | eval Date=strftime (_time, "%m/%d/%Y")
| where isnotnull(reason)
| table log_level, reason, Date
| dedup reason
| sort Date
```

Add Inputs, Edit Dashboards 
Edit Drill down Editor
What are alerts
 
	Saved searches : -Run on schedule -Run real-time
	Content matches : Fire when a condition is matched
	Create trigger actions : -Log -Send email -Webhook -Custom action
	Create trigger conditions : Per-result ,# of results ,# of sources ,Custom ,Throttle



### What is a tag
	Quick reminder : What was I trying to see again?
	Aid for reading data : Create as many tags as you want
	Case sensitive : Typing matters when searching

### What are event types?

	Highlighter : Make them colors, mark events with similar criteria
	Like a report, but not : Save searches as specific event types, sort into categories, no time range Ex: status=404 can be
  saved as "Not Found"
	More specific : Set strings, field values, and tags


```
index=* tag=login Account_Name=hailie
timechart count span=1d
```


### Macros
	
	Shortcuts : Fast, saved off searches to run by name
	Repeatable : The macro never changes,unless you edit it
	Expandable : Ctrl-Shift-E for Windows/Command-Shift-E for Mac
	'macroname' : Run with the use of backticks, not single quotes

Navigate to Settings > Advanced search > Search macros Click Add new to create one


###  Workflow Actions

Assess Actions : Depending on use case,there are three available workflow actions which provide different functionalities
Create Workflow Action : Using Spunk Web, create a new Workflow Action to either push, pull or search data
Configure Workflow Action : Within the Web GUI,configure the previously determined action type with a 3rd party source
Validation : Check to see if data is being pushed, pulled or searched for after configuration


GET : Create HTML links to interact with sites Ex: Google searches, querying WHOIS databases
POST : Generate HTTP POST request to specified URI Ex: Create entries in management systems, forums
Search : launch secondary searches using field values Ex: Occurrences of IP addresses over events


Field aliases :Normalize your data Apply multiple fields to the same field alias Make searching easier amongst users
Think CIM *The original field name is not affected post field alias implementation

Calculated fields :Like a macro, but for a fields Save off quick math to output fields using the eval command, then use it in a
search

Navigate to Settings > Fields > Field Aliases Click New Field Alias to create one
Navigate to Settings > Fields > Calculated Fields Click New Calculated Field to create one

Job inspector
Allows you to troubleshoot your search efficiency, or reason for failing
Gives you information about how the search completed, and time it took to run
If you are using a KO wrong, it will suggest how to correct your search


https://www.mediafire.com/file/rlv4d9t89j908cj/Splunk_Video_Course_Downloads.zip/file 
https://docs.google.com/document/d/1PiHcXLJ93zOmeY-1BToRr-X0Az4vt7UWMN1rQBw7luI/edit#heading=h.6fxiynwr0aa5
https://docs.google.com/document/d/137z48GMwp4okkvAZhxUD-TXaS9z93N-FaqyUq7IB6uQ/edit?usp=sharing
https://docs.google.com/document/d/1MwNqij-7PsEhopvmFwyB2s2PThpUczz4Uas0VZ3Gpm0/edit?usp=sharing
https://docs.google.com/document/d/1b8oVRsss4g7eDyhn1QegX9n2OtVuBmk5L3vGrs6og9Q/edit?usp=sharing
https://docs.google.com/document/d/1JTjzjY3UiGr8xCsjkxI6UPhy6d3-KwParM04MHEZX-4/edit?usp=sharing
https://docs.google.com/document/d/1kDuvq0XVtWtXt7WlmVO8S8Q07LOBupaW8JziACGGXu8/edit?usp=sharing
https://docs.google.com/document/d/1U1dxnzchvnBVwvk_GYfSEsFcX4wvrB1_hcZCKgd952g/edit?usp=sharing
https://docs.google.com/document/d/1iCe8PqIRsYdEwjZbqlQD471K6WC6GbcjoVYpwwQFmps/edit?usp=sharing
https://docs.google.com/document/d/1ybWYM6M65gWmB6UmYaVoHHCakDoM5DY3fUK4o3tn7ic/edit?usp=sharing
https://docs.google.com/document/d/1AUVWkx2ONTuRTc7yAJsiW1H10jwy1B0Ss-4AQCGxzJg/edit?usp=sharing


 





