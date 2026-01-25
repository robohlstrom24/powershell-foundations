## Archive Files by Age 

This shell demo shows how to archive files older than a defined retention period using PowerShell.  
The example moves files older than 30 days from a user’s **Downloads** directory into a scoped archive folder.

---

### Scenario

User-facing directories often accumulate stale files over time. This demo illustrates a safe, repeatable cleanup operation using time-based filtering and basic PowerShell pipelines.

---

### Demo Code

```powershell
$source  = "$env:USERPROFILE\Downloads"
$archive = Join-Path $source "DemoArchiveByAge\Archive"
$cutoff  = (Get-Date).AddDays(-30)

New-Item -ItemType Directory -Path $archive -Force | Out-Null

Get-ChildItem -Path $source -File |
  Where-Object { $_.LastWriteTime -lt $cutoff } |
  Move-Item -Destination $archive

