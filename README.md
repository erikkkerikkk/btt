# btt

for kkbox mac

on isRunning(theAppName)
	tell application "System Events" to (name of processes) contains theAppName
end isRunning
if isRunning("KKBOX") then
	set theContentNames to {}
	tell application "System Events"
		tell process "NotificationCenter"
			repeat with theWindow in windows
				set theContents to entire contents of theWindow
				repeat with theContent in theContents
					if class of theContent is static text then
						set end of theContentNames to name of theContent
					end if
				end repeat
			end repeat
		end tell
	end tell
	if length of theContentNames is 3 then
		if item 2 of theContentNames is equal to missing value then
			set theResult to (item 1 of theContentNames) & (item 3 of theContentNames)
			do shell script "echo \"" & theResult & "\" > ~/btt_kkbox"
		end if
	else
		set theResult to do shell script "cat ~/btt_kkbox"
	end if
	return theResult
else
	return "KKBOX"
end if
