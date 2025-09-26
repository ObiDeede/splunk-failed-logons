# splunk-failed-logons
Documentation of Windows Event ID 4625 failed logons analyzed in Splunk
Documentation: Failed Logon Analysis in Splunk
1. Log Generation (Windows)
• Manually generated failed logons on my Windows system.
• Verified events in Event Viewer → Windows Logs → Security.
• Filtered by Event ID 4625 (Failed Logon Attempts).
• Exported logs as .evtx file (e.g., failed_logons_4625.evtx).
2. Import into Splunk
• Uploaded .evtx file via Add Data → Upload.
• Sourcetype automatically assigned: WinEventLog:Security.
• Data indexed into default index.
3. Search Queries Used
• Base search (all failed logons):
sourcetype="WinEventLog:Security" EventCode=4625
• Trend over time (line chart):
sourcetype="WinEventLog:Security" EventCode=4625
| timechart count
• Failed logons by failure reason:
sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Failure_Reason
• Failed logons by user:
sourcetype="WinEventLog:Security" EventCode=4625
| stats count by Account_Name
4. Dashboard Panels
• Panel 1 – Timechart: Trend of failed logon attempts → sharp spike Wed–Fri.
• Panel 2 – Bar/Table: Failed logons grouped by Failure_Reason (single bar since all logs had one reason).
• Panel 3 – Bar Chart: Failed logons grouped by Account_Name.
5. Observations
• Total failed logons = 29.
• All attempts originated from the same host (my machine).
• Same failure reason repeated, resulting in a single bar for that panel.

NOTE:
Event ID 4625 is a Windows Security Log event that records a failed logon attempt. It helps detect brute-force attacks, misconfigured accounts, or unauthorized access attempts.
