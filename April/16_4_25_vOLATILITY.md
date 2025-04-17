Task 10 Practical Investigations

1: What is the build version of the host machine in Case 001?

 we will enter vol -f /Scenarios/Investigations/Investigation-1.vmem windows.info again in order to get the build information.


Answer: 2600.xpsp.080413–2111

2: At what time was the memory file acquired in Case 001?


Answer: 2012–07–22 02:45:08

3: What process can be considered suspicious in Case 001?


Answer: reader_sl.exe

4: What is the parent process of the suspicious process in Case 001?

 vol -f /Scenarios/Investigations/Investigation-1.vmem windows.pstree 


Answer: explorer.exe

5: What is the PID of the suspicious process in Case 001?


Answer: 1640

6: What is the parent process PID in Case 001?


Answer: 1484

7: What user-agent was employed by the adversary in Case 001?

Answer: Mozilla/5.0 (Windows; U; MSIE 7.0; Windows NT 6.0; en-US)

8: Was Chase Bank one of the suspicious bank domains found in Case 001? (Y/N)

Answer: Y

9: What suspicious process is running at PID 740 in Case 002?
Answer: @WanaDecryptor@

10: What is the full path of the suspicious binary in PID 740 in Case 002?


Answer: C:\Intel\ivecuqmanpnirkt615\@WanaDecryptor@.exe

11: What is the suspicious parent process PID connected to the decryptor in Case 002?


Answer: tasksche.exe

12: What is the suspicious parent process PID connected to the decryptor in Case 002?

Answer: 1940

13: From our current information, what malware is present on the system in Case 002?

Answer: Wannacry

14: What DLL is loaded by the decryptor used for socket creation in Case 002?


WS2_32.dll can be used by trojans for network connections, so it may be a backdoor.

Answer: WS2_32.dll

15: What mutex can be found that is a known indicator of the malware in question in Case 002?

Answer: MsWinZonesCacheCounterMutexA

16: What plugin could be used to identify all files loaded from the malware working directory in Case 002?
Answer: windows.filescan
