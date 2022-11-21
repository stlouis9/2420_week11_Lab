# 2420 Week 11 Lab Readme
<p>Justin Tan 
Robert St. Louis</p>

## Usage
<p>To setup the backup script a config file is necessary</p>

### Config File
<p>
    Place your <code>backup.cfg</code> file in <code>$HOME/bin</code>
</p>
<p>
    Your config file should look like this :
</p>
<pre><code>DIRS="$HOME/bin $HOME/test1"
IP=157.230.17.142</code></pre>

<p>
To add additional directories to backup, add a directory with a space to deliniate to the <code>DIRS</code> variable. 
</p>

### backup-script
<p>
    Place the backup script in <code>/opt/backup-script/</code>
    use <code>chmod +x backup-script</code> to make the file executable
</p>

### backup.service and backup.timer
<p>
    Your <code>backups.service</code> file should look like this:
</p>

<pre><code>[Unit]
Description=use rsync to backup files every Friday at 01:00

[Service]
Type=oneshot
ExecStart=/opt/backups/backups

[Install]
WantedBy=multi-user.target</code></pre>

<p>
    Your <code>backups.timer</code> file should look like this:
</p>

<pre><code>[Unit]
Description=Timer to start the backups script every Friday at 01:00

[Timer]
OnCalendar=Fri *-*-* 01:00:00
Persistent=True
RandomizedDelaySec=120

[Install]
WantedBy=timers.target</code></pre>
<p>
    Place the backup.service and backup.timer files in <code>/etc/systemd/system</code> then make the service executable with <code>chmod +x</code> 

Now run the commands: 

    
<code>sudo systemctl enable --now backup.service</code>
    
<code>sudo systemctl enable --now backup.timer</code>
    
<code>sudo systemctl daemon-reload</code>
    


Do this to enable and start the service and timers.

Once they have been enabled check the status with <code>systemctl status backup.service</code> and <code>systemctl status backup.timer</code> if its successful it will look like:

![backup service](/images-directory/service.png)

![backup service](/images-directory/timer.png)
respectfully.
</p>
