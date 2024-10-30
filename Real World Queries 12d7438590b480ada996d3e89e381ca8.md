# Real World Queries

---

```
index=* EventCode=4624
| stats count as "Login Attempts", range(_time) as "Time Range" by Account_Name
| where 'Time Range' <= 600  // Filtering for 10 minutes (600 seconds)
| sort - "Login Attempts"
| head 1
| rename Account_Name as "Account Name"
```

```lua
index="main" 
Image=*cmd.exe ParentImage!="*msiexec.exe" 
ParentImage!="*explorer.exe" 
CommandLine!=*splunk*
| eval len=len(CommandLine) 
| table User, len, CommandLine,ParentImage,Image 
| sort - len
```

```
index="main" sourcetype="WinEventLog:Sysmon" EventCode=8 
| bin _time span=1h 
| stats count as thread_injections by _time, SourceImage

//if you want to detect the time of created processes in few minutes (suspicious)

index="main" sourcetype="WinEventLog:Sysmon" EventCode=8 
| bin _time span=1h 
| stats count as thread_injections by _time, SourceImage 
| eventstats avg(thread_injections) as avg_injections, stdev(thread_injections) as stdev_injections 
| eval upper_limit = avg_injections + (2 * stdev_injections) 
| where thread_injections > upper_limit 
| table _time, SourceImage, thread_injections, avg_injections, stdev_injections, upper_limit 
| sort -thread_injections
```