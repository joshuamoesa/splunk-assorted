The dashboard refers to two reports:
- esb_daily_report_all_events_hosts
- esb_daily_report_non_recoverable_errors

The esb_daily_report_all_events_hosts search query:
```
| tstats count  
where 
index=applications_esb_p_apl6169
earliest=-8d@d latest=@d

`flow_all_hosts` 

BY host  _time  span=1d

| stats sum(count) AS count
by _time host
```

The esb_daily_report_non_recoverable_errors search query:

```
index=applications_esb_p_apl6169 host="/ecs/pnlp-esb-*" non_recoverable_error
earliest=-8d@d latest=@d
|timechart count by host
```
