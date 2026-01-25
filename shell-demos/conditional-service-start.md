## Conditional Service Start 

This shell demo shows a safe, repeatable method for verifying the status of core background services and starting only those that are not running. The example targets BITS, Windows Update (wuauserv), and Windows Time (W32Time), which commonly impact software installs, update delivery, and system reliability when stopped. 

## Troubleshooting Scenario

This method would be used when users report Windows Updates failing to progress, often caused by background services stopping unexpectedly after a reboot. The status of related services is verified and only those not running are started to restore normal system behavior while minimizing unnecessary changes. 


```powershell

foreach ($name in 'BITS','wuauserv','W32Time') {
    $svc = Get-Service $name
    if ($svc.Status -ne 'Running') {
        Start-Service $name
    }
}
```

(see: [Troubleshooting Journal Repository T-0006](https://github.com/robohlstrom24/troubleshooting-journal))
