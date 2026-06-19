# 📝 Investigation Notes

## Summary

This lab investigated the execution of **certutil.exe** as a potential **Living Off The Land Binary (LOLBin)**.

The following command was executed:

```cmd
certutil -urlcache -split -f http://localhost:8000/test.txt test.txt
```

The command returned **Access is denied**, preventing the file from being downloaded.

Despite the failed download, the execution generated **Sysmon Event ID 1**, providing valuable telemetry for investigation.

---

## Key Observations

- Process: `certutil.exe`
- Parent Process: `cmd.exe`
- Event ID: **Sysmon Event ID 1**
- URL Accessed: `http://localhost:8000/test.txt`
- Download Status: Failed (Access Denied)

---

## Why This Is Suspicious

Attackers frequently abuse **certutil.exe** to download malware or additional payloads while bypassing application controls.

The presence of `-urlcache`, `-split`, and `-f` in the command line is uncommon during normal user activity and should be investigated.

---

## MITRE ATT&CK

- **T1218** – System Binary Proxy Execution
- **T1105** – Ingress Tool Transfer

---

## Detection Opportunities

Look for:

- `certutil.exe` execution
- `-urlcache` in the command line
- `-split` in the command line
- `-f` in the command line
- HTTP or HTTPS URLs

---

## Analyst Conclusion

Although the payload download failed, the attempted use of **certutil.exe** generated sufficient evidence for detection and investigation. Attempted LOLBin abuse should be treated as suspicious activity and analyzed further.
