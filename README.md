Blah (name TBD) is an experiment to see if https://miek.nl/2022/november/15/provisioning-services/
is actually a sane way of doing thing.

The mind says 'yes', reality says '...' ?

## Notes

## metrics

gitopper_service_hash{hash="...", service="...", machine="...."} 1

## Features

Noop feature

## depth

-depth 1 is useless;
we want all systems have the same history, and if the repo becomes big *all* clients will see that
pressure at the same time, not in the ordering in which they came up and received their first pull.

## first commit

There can be 'no commit' which is ok.

~~~
git df HEAD^ HEAD -- grafana
fatal: bad revision 'HEAD^'
~~~

## wipe a repo

We may want to wipe a repo and let the automation reclone in an emergency.

### config

~~~
grafana.atoom.net {
        package grafana
        action reload grafana-server
        repo {
            url git@gitlab.com/sys/data
            mountpoint /mnt/grafana
        }
        # define the directories for the sparse checkout and how to bind mount them
        /etc/grafana -> grafana/etc
        /var/lib/grafana/dashboards -> grafana/dashboards
}
~~~

~~~ txt
{
    # global options
    url git@github.com/miekg/blah-origin
}

grafana.atoom.net {
        package grafana
        action reload grafana-server
        mountpoint /mnt/grafana
        directories grafana

        # define the directories for the sparse checkout and how to bind mount them
        /etc/grafana -> grafana/etc
        /var/lib/grafana/dashboards -> grafana/dashboards
}
~~~

## Code

Do we need plugins for this things? Maybe other type of remotes, like mercurial or something?

## Remote Interface

- list all machines - from the config file?
- list all services, and a machine
- free a service -- need name. We need extra field to identify service.
- get status of services, check also upstream repo
