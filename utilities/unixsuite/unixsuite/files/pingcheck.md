Description: The pingcheck script does three pings of the guardian server, 
one every minute, so that if a power outage or other interruption of the 
internet, the VMs will do a safe shutdown. The UPSs have about a 10 minute 
time before the main systems are shut down so three minutes should be 
sufficient

If you're using it, change the PINGCHECK variable at the beginning of 
the file to make sure you're checking the correct remote server.

