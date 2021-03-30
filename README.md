Zwift Activity Monitor
======================

## The Power is Within You

![main_form](https://github.com/ruffk/ZwiftActivityMonitor/raw/master/ZwiftActivityMonitor/images/MainForm.png)

This project allows Zwift riders to monitor their power and heartrate averages in real-time.

## How It Works

Zwift Activity Montitor (or ZAM for short), monitors outgoing network packets generated by the Zwift application and
aggregates the data into statistical moving averages.

## Using Zwift Activity Monitor

The network packets that ZAM consumes contain some important statistics.  Some of them are:
<ol>
	<li>Current power output</li>
	<li>Current heartrate (if wearing an HRM)</li>
	<li>Distance travelled</li>
	<li>Time spent riding</li>
</ol>



### Configuration

ZAM is easily configured via a set of configuration tab pages in the <b>Options</b> dialog.

#### Options -> System Configuration Tab

ZAM first and foremost needs to know what network you use when running Zwift.  It's usually pretty simple as most
computers are either Wi-Fi or direct Ethernet cabled.  Within ZAM there is a packet monitoring system which MUST be started
in order to use ZAM.  This can either be done manually each time you run ZAM (by clicking the Start button), or by checking Auto-Start.
<ol>
	<li>Default User - The user profile that will be used each time ZAM starts.</li>
	<li>Network - The network in your computer you use when running Zwift.</li>
	<li>Window Position - Once you find where you like the ZAM window to sit, enter those coordinates and it will open there each time.</li>
</ol>

![system_options](https://github.com/ruffk/ZwiftActivityMonitor/raw/master/ZwiftActivityMonitor/images/SystemOptions.png)


<p>

ZAM is highly configurable and has the ability to save multiple rider profiles. A rider profile consists of: 

<ol>
	<li>Rider name</li>
	<li>Weight, in Kilos or Pounds</li>
	<li>FTP</li>
	<li>Default moving average collector selection</li>
</ol>

![user_profiles](https://github.com/ruffk/ZwiftActivityMonitor/raw/master/ZwiftActivityMonitor/images/UserProfiles.png)
</p>

ZAM extracts this data into moving average collectors and presents then on the screen in real-time.
Furthermore, you'll get to see the following overall statistics:

<ol>
	<li>Average power output</li>
	<li>Normalized power output</li>
	<li>Intensity factor (IF)</li>
	<li>Average speed</li>
</ol>


## Prerequisites

Before you begin, ensure you have met the following requirements:
* You have installed the latest version of Npcap: Packet capture library for Windows. (https://nmap.org/npcap/#download)

## Installing Zwift Activity Monitor

To install Zwift Activity Monitor, follow these steps:

Windows:

<ol>
	<li>Make sure you've installed the latest version of Npcap from the link above in Prerequisites.</li>
	<li>Download the latest Setup-ZAM.exe release from this GitHub repository.  You may get some weird messages from your Anti-Virus software.</li>
	<li>Run the installation.  Again, you may get some messages from your Anti-Virus software.</li>
</ol>

## Using Zwift Activity Monitor

<p><b>Steps for preparing to use Zwift Activity Monitor:</b></p>

<ol>
    <li>Find the name of your network adapter</li>
    <ol type="i">
        <li>Open a command prompt by opening the Windows start menu and entering the command "cmd".</li> 
        <li>In the command prompt window, enter the command "ipconfig /all"</li>
        <li>Scroll through the results to find your network adapter name.  You're looking for the adapter with an IP addressed assigned.  It must be the same network that you run Zwift on.</li>
    </ol>
    <br>Examples:
    <ul>
        <li>Ethernet adapter Ethernet: (in this case the name is "Ethernet")</li>
        <li>Wireless Lan adapter Wi-Fi: (in this case the name is "Wi-Fi")</li>
        <li>There may be some others in the list.</li>
    </ul><br>
    <li>Using a text editor (like notepad.exe) find and open the file appsettings.Production.json.  It will be in the same directory as the executable files,
	which by default is <b>C:\Program Files (x86)\Zwift Activity Monitor</b></li>
	<ol type="i">
    	<li>Section ZwiftPacketMonitor</li>
    	<ul>
        	<li>Modify the value associated with the "Network" key to the network name you found in step one.</li>
    	</ul>
    	<li>Section ZwiftActivityMonitor</li>
    	<ol type="a">
        <li>Modify the value associated with the "Weight" key to your weight.  You can enter it in pounds (ie. 175) or kilograms (75.4).</li>
        <li>Modify the value associated with the "UnitOfMeasure" key to be either lbs or kgs, according to the units you entered your weight in.</li>
        <li>Modify the value associated with the "ThresholdPower" key to your threshold power number (in watts).  This is not your FTP, this is the value you would multiply by .95 to get your FTP.  It is used to calculate IF (intensity factor).</li>
        </ol>
    </ol><br>
	<li>Select default Moving Average collectors.  This is optional as 1 min, 5 min, and 20 min collectors are already setup for you.</li>
    <ol type="i">
    	<li>Determine the three collectors you would like to see on application start-up. (5 sec, 1 min, 5 min, etc.)</li>
    	<li>Modify the value associated with the "Display" key to be either true (if you'd like to see it) or false (if you don't).</li>
    	<li>Optionally, you can change how units for average power, maximum power, and FTP are displayed.  This can be either in watts or wkg.  You can even specify none if you don't want to see a value.</li>
    </ol><br>
<li>Save the configuration file.</li>
</ol>

<p><b>Steps for running the Zwift Activity Monitor:</b></p>

<ol>
	<li>Launch the application from the desktop icon or start menu</li>
	<li>When the Advanced Options dialog appears, click Start</li>
	<ul>
		<li>The Manual Operation Status should switch to Running.  If so, click Close and you're ready to monitor!</li>
		<li>If you get an error regarding your network, verify that you've setup the ZwiftPacketMonitor:Network key correctly using the steps above. </li>
	</ul>
	<li>Launch the Zwift application if not already running.</li>
</ol>

<p><b>Quick start guidance to get monitoring:</b></p>

<p>
	The Zwift Activity Monitor main window is transparent and is designed to be moved on top of the Zwift main window.
	Because it is transparent, you will still be able to see Zwift screen activities behind it.  If you have chosen (up to three)
	default collectors in the setup procedure above, you should see those items on the main window.
</p>

<ol>
	<li>Analyze menu</li>
	<ul>
		<li>Start - This will start collecting power and heartrate from Zwift as you ride.  Those results will be displayed on the main window.</li>
		<li>Stop - This will stop collection but will leave the latest values on the screen for your analysis.</li>
		<li>Timer</li>
		<ul type="i">
			<li>Setup Timer dialog - The timer is handy when waiting in the pen for an event to start.  You can syncronize the time remaining to the Zwift
			event clock and click Start.  On the main window you will see the countdown occur and when it hits zero the monitor will automatically begin.
			This is also useful for TTTs with a delayed start.  If you will have a four minute delay after banner drop, add four minutes to the Zwift event clock
			and set the timer.  Now you will know exactly when to Go! Go! Go!</li>
			<li>Stop Timer - Stops a running timer</li>
		</ul>
	</ul>
</ol>

## Contributing to <project_name>

1. Fork this repository.
2. Create a branch: `git checkout -b <branch_name>`.
3. Make your changes and commit them: `git commit -m '<commit_message>'`
4. Push to the original branch: `git push origin <project_name>/<location>`
5. Create the pull request.

Alternatively see the GitHub documentation on [creating a pull request] (https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request).

## Credits

Brad Walker for development of the ZwiftPacketMonitor library (https://github.com/braddwalker/ZwiftPacketMonitor) and giving me great ideas.

<div>Icons made by <a href="" title="photo3idea_studio">photo3idea_studio</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a></div>

## Contact

If you want to contact me you can reach me at <mailto:ruff.kevin@outlook.com>.

## License

This project uses the following license: [MIT License] (https://github.com/ruffk/ZwiftActivityMonitor/blob/master/LICENSE).
