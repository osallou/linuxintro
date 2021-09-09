# Systemd

We talk previously of systemd, which manage services startup and status (basically)

Services description are usually located in /lib/systemd/system and /etc/systemd/system.

A service can be started or stopped manually via

    service myservice start
    service myservice stop

It is possible to check service status (on/off) via

    service myservice status

When a new service description is added, it must be loaded by the system a first time

    systemctl daemon-reload

For a service to start at boot:

    systemctl enable myservice

And to remove from boot list

    systemctl disable myservice
