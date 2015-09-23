# SwapManager
The purpose of this project is to monitor RAM usage and automatically create a swap file if the usage surpasses a set
threshold. SwapManager will handle the creation and SwapRemover will handle the removal of the swap file upon a shutdown, reboot or halt event. To implement this SwapRemover should be called by a one-shot service like:

[Unit]
Description=Removes swap file on shutdown.
DefaultDependencies=no
Before=shutdown.target reboot.target halt.target

[Service]
Type=oneshot
RemainAfterExit=true
ExecStart=/usr/bin/SwapRemover

[Install]
WantedBy=multi-user.target

SwapManager can be fired at the launch of an interactive profile by adding it to .profile or .bashrc. Both scripts require sudo permissions so adding 

username ALL = (ALL) NOPASSWD: /path/to/SwapManager, /path/to/SwapRemover

to the sudoers file (visudo) is required.
