## Create the try block and create any code inside.
try { 
	## Create the FTP script file using a here string (https://devblogs.microsoft.com/scripting/powertip-use-here-strings-with-powershell/)
	## If Out-File creates the FTP script, it then invokes ftp.exe to execute
	## the script file.	
	$Script = @"
	open localhost
	username
	password
	BINARY
	CD remotefolder
	LCD C:\folder
	GET remote.file
	BYE
"@
	$Script | Out-File "C:\Folder\ftp.txt" -Encoding ASCII

	ftp -s:C:\folder\ftp.txt
} catch {
	## If, at any time, for any code inside of the try block, returns a hard-terminating error
	## PowerShell will divert the code to the catch block which writes to the console
	## and exits the PowerShell console with a 1 exit code.
	Write-Host "Error: $($_.Exception.Message)"
	exit 1
} finally {
	## Regardless if the catch block caught an exception, remove the FTP script file
	Remove-Item -Path "C:\folder\ftp.txt"
}

## When the code inside of the try/catch/finally blocks completes (error or not),
## exit the PowerShell session with an exit code of 0
exit 0
