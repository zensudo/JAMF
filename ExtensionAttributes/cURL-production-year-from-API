# NAME: JAMF API - cUrl year of production by serialnumber
# AUTHOR: https://github.com/zensudo
# VERSION: 1.0
# DESCRIPTION: Script calls JAMF-API to get the year of production from device informations.

# Define API User Credentials
API_User=$(echo 'USER:PASSWORD')

# Get the Serialnumber of the macOS Device
Mac_Serial=$(system_profiler SPHardwareDataType | awk '/Serial/ {print $4}')

# Get url from JAMF MDM Server
MDM_url=$(defaults read /Library/Preferences/com.jamfsoftware.jamf.plist jss_url)

# User JAMF-API to get the year of device production
API_curl=$(curl -u "$API_User" -X GET ""$MDM_url"JSSResource/computers/serialnumber/$Mac_Serial" -H  "accept: application/xml"| grep -Eo '<model> |, 20[0-9][0-9]' |  sed 's/^,//' | cut -c 2- )

# Create a result to use as extension attribute
echo "<result>"$API_curl"</result>"
