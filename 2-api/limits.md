[Back to Conversation AI Overview](https://conversationai.github.io/) | [Back to Perspective API documentation](https://github.com/conversationai/perspectiveapi/blob/master/README.md)

# Limits and errors

## Quota limit

By default, we set the quota to 1 QPS for all Perspective projects.

Check your quota limits by going to [your google cloud project's Perspective API page](https://console.cloud.google.com/apis/api/commentanalyzer.googleapis.com/quotas), and check your project's quota usage at
[the cloud console quota usage page](https://console.cloud.google.com/iam-admin/quotas).

Visit the Perspective API Support page to [request a quota increase](https://support.perspectiveapi.com/s/request-quota-increase).

## Character limit for requests

The maximum text size per request is 3000 bytes.


## Error messages
When using Outline, you might see a variety of error messages. This article details what each of those error messages might mean. 
 
Error message: “It seems like your access key is not valid. If this happens again, please contact your server admin.”
If you receive this message, it likely means that the access key you’re using to try and connect to the Outline server isn’t valid any more. If you set up the server on your own, try generating a new key for yourself. Otherwise, please contact your server administrator—usually the person who gave you your original invitation—for a new invitation.
 
Error message: “We can’t seem to connect to your server. Please check that you are connected to the internet and try again.”
There may be a few reasons for this that you can troubleshoot on your own.
 
What could be happening
How to test it
Things you can try
Your device is disconnected from the internet.
 
Sometimes your device will experience a break in network connection and it may take a moment for it to update the network icons. It’s also possible that your device is connected to the local network, but that the internet is down.
Turn off Outline and see if your connection to the internet is restored.
If yes, see more troubleshooting options below.
If not, then wait a few moments to see if your connection settings update themselves.
Get your device back online:
Check another device to see if it can connect to the same network. If other devices cannot get online, the network may be down and you will need to wait for it to return or troubleshoot it.
If other devices can get on the same network, you can try one or more of the followin g to get it back online:
Put the device in airplane mode (mobile)
Restart the device
Shut down the device, wait 2 minutes, turn the device back on
Your network firewall is blocking access to your Outline server, if you’re connected via WiFi or a wired connection.
 
This is very common if you’re on a school, work, or free wireless network.
Disconnect from your current WiFi or wired network.
Connect to a different network, like a cellular one
Try to reconnect to Outline
 
If you are able to connect while on the other network, then this is your issue.
Please contact the network administrator and request them to allow access to your server or continue using the other network instead.
Your device has a firewall or antivirus software that is blocking access to your Outline server.
Try connecting to Outline from another device. 
Remember that you’d need an access key and the Outline app to use Outline on the other device.
Check your firewall or antivirus software settings to make sure they are set to allow VPN and Outline traffic through.
Your server administrator may have destroyed the server or your ISP may be blocking your request.
If you have access to more than one server, try connecting to the other one. 
Contact your server administrator to see if the server has been destroyed. If you set up the server, try connecting to it through the Outline Manager or another method such as SSH. If that doesn’t work, you can try checking the cloud provider console, if any, to see if the server is still online.
 
Error message: “Sorry, it looks like Outline is not properly installed. Please try installing it again. If that doesn't work, please submit feedback through the app.” (Windows devices only)
If you’re using Outline on Windows, occasionally, you may run into an unexpected error. In most cases, the Outline TAP adapter (driver) needs to be deleted and Outline should be reinstalled.
 
The steps may vary based on your Windows operating system version, but we’ve provided general steps for how to uninstall the TAP adapter and Outline and then reinstall Outline.
Uninstall the TAP adapter for Outline
Go to “Device Managers”, then look under “Network Adapters”
Find the “TAP-Windows Adapter V9” file or the TAP adapter associated with Outline
Uninstall or delete this adapter. Keep in mind that this could affect other VPN apps that you have installed. 
Uninstall Outline
Go into “Programs & Features”, then go to “Uninstall Program”
Find the Outline app and uninstall Outline
Download the latest version of Outline from getoutline.org and re-install it on your Windows device. The new installation should install a new TAP adapter for you.
 
If you’re still having trouble, you can also contact support by submitting feedback through the Outline app. This gives us some information about your environment that lets us better isolate the issue.

