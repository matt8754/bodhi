=====
bodhi
=====

Synopsis
========

``bodhi`` COMMAND SUBCOMMAND [OPTIONS] [ARGS]...


Description
===========

``bodhi`` is the command line interface to bodhi, Fedora's update release management system. It can
be used to create or modify updates and overrides.


Options
=======

Most of the commands will accept these options:

``--help``

    Show help text and exit.

``--password <text>``

    A password to authenticate as the user given by ``--user``.

``--staging``

    Use the staging bodhi instance instead of the production instance.

``--url <url>``

    Use the Bodhi server at the given URL instead of the default server. This can also be set with
    the ``BODHI_URL`` environment variable. This is ignored if the ``--staging`` flag is set.

``--user <username>``

    Many commands accept this flag to specify a Fedora username to authenticate with. The
    username can also be provided via the ``USERNAME`` environment variable. Note that some read
    operations such as querying updates and overrides use this same flag, but as a search parameter
    instead of authentication (as authentication is not required for these operations). Those
    operations do not use the ``USERNAME`` environment variable.

``--version``

    Show version and exit. Not accepted by subcommands.


Commands
========

There are two commands, ``overrides`` and ``updates``. They are described in more detail in their
own sections below.

``bodhi overrides <subcommand> [options] [args]``

    Provides commands to aid in management of build overrides. Supports subcommands ``query`` and
    ``save``, described below.

``bodhi updates <subcommand> [options] [args]``

    Provides an interface to manage updates. Supports subcommands ``comment``, ``download``,
    ``new``, ``query``, and ``request``, described below.


Overrides
=========

The ``overrides`` command allows users to manage build overrides.

``bodhi overrides query [options]``

    The ``query`` subcommand provides an interface for users to query the bodhi server for existing
    overrides.  The ``query`` subcommand supports the following options:

    ``--mine``

        Show only your overrides.

    ``--active``

        Filter for only active overrides

    ``--expired``

        Filter for only expired overrides

    ``--packages <packagename>``

        Query for overrides related to the given packages, given as a comma-separated list.

    ``--releases <releases>``

        Query for overrides related to a list of releases, given as a comma-separated list.
        <releases> is the release shortname, for example: F26 or F26,F25

    ``--user <username>``

        Filter for overrides by the given username.


``bodhi overrides save [options] <nvr>``

    Save the build root given by ``<nvr>`` as a buildroot override. The ``save`` subcommand supports
    the following options:

    ``--duration <days>``

        The number of days the override should exist, given as an integer.

    ``--notes <text>``

        Notes on why this override is in place.

``bodhi overrides edit [options] <nvr>``

    Edit the build root given by ``<nvr>`` as a buildroot override. The ``edit`` subcommand supports
    the same options than the ``save`` command and also the following option:

    ``--expire``
        Force an override to the expired state.

Updates
=======

The ``updates`` command allows users to interact with bodhi updates.

``bodhi updates comment [options] <update> <text>``

    Leave the given text as a comment on a bodhi update. The ``comment`` subcommand
    supports the following options:

    ``--karma [+1 | 0 | -1]``

        The karma value you wish to contribute to the update.

``bodhi updates download [options]``

    Download update(s) given by CVE(s), ID(s), or NVR(s). One of ``--cves``, ``--updateid``, or
    ``builds`` is required. The download subcommand supports the following options:

    ``--cves <cves>``

        A comma-separated list of CVEs that identify updates you would like to download.

    ``--updateid <ids>``

        A comman-separated list of update IDs you would like to download.

    ``--builds <nvrs``

        A comma-separated list of NVRs that identify updates you would like to download.

``bodhi updates new [options] <builds>``

    Create a new bodhi update containing the builds, given as a comma separated list of NVRs. The
    ``new`` subcommand supports the following options:

    ``--type [security | bugfix | enhancement | newpackage]``

        The type of the new update.

    ``--notes <text>``

        The description of the update.

    ``--notes-file <path>``

        A path to a file containing a description of the update.

    ``--bugs <bugs>``

        A comma separated list of bugs to associate with this update.

    ``--close-bugs``

        If given, this flag will cause bodhi to close the referenced bugs automatically when the
        update reaches stable.

    ``--request [testing | stable | upush]``

        The repository requested for this update.

    ``--autokarma``

        Enable autokarma for this update.

    ``--stable-karma <integer>``

        Configure the stable karma threshold for the given value.

    ``--unstable-karma <integer>``

        Configure the unstable karma threshold for the given value.

    ``--suggest [logout | reboot]``

        Suggest that the user logout or reboot upon applying the update.

    ``--file <path>``

        A path to a file containing all the update details.

    ``--requirements <Taskotron tasks>``

        A comma or space-separated list of required Taskotron tasks that must pass for this update
        to reach stable.

``bodhi updates edit [options] <update>``

    Edit an existing bodhi update, given an update id or an update title. The
    ``edit`` subcommand supports the following options:

    ``--type [security | bugfix | enhancement | newpackage]``

        The type of the new update.

    ``--notes <text>``

        The description of the update.

    ``--notes-file <path>``

        A path to a file containing a description of the update.

    ``--bugs <bugs>``

        A comma separated list of bugs to associate with this update.

    ``--close-bugs``

        If given, this flag will cause bodhi to close the referenced bugs automatically when the
        update reaches stable.

    ``--request [testing | stable | upush]``

        The repository requested for this update.

    ``--autokarma``

        Enable autokarma for this update.

    ``--stable-karma <integer>``

        Configure the stable karma threshold for the given value.

    ``--unstable-karma <integer>``

        Configure the unstable karma threshold for the given value.

    ``--suggest [logout | reboot]``

        Suggest that the user logout or reboot upon applying the update.

    ``--requirements <Taskotron tasks>``

        A comma or space-separated list of required Taskotron tasks that must pass for this update
        to reach stable.

``bodhi updates query [options]``

    Query the bodhi server for updates. The ``query`` subcommand supports the following options:

    ``--updateid <id>``

        Query for the update given by id.

    ``--approved-since <timestamp>``

        Query for updates approved after the given timestamp.

    ``--modified-since <timestamp>``

        Query for updates modified after the given timestamp.

    ``--builds <builds>``

        Query for updates containing the given builds, given as a comma-separated list.

    ``--bugs <bugs>``

        Query for updates related to the given bugs, given as a comma-separated list.

    ``--content-type <content_type>``

        Query for updates of a given content type: either rpm, module, or (in the future) container.

    ``--critpath``

        Query for updates submitted for the critical path.

    ``--cves <cves>``

        Query for updates related to the given CVEs, given as a comma-separated list.

    ``--mine``

        Show only your updates.

    ``--packages <packages>``

        Query for updates related to the given packages, given as a comma-separated list.

    ``--pushed``

        Query for updates that have been pushed.

    ``--pushed-since <timestamp>``

        Query for updates that have been pushed after the given timestamp.

    ``--releases <releases>``

        Query for updates related to a list of releases, given as a comma-separated list.

    ``--locked``

        Query for updates that are currently locked.

    ``--request [testing | stable | unpush]``

        Query for updates marked with the given request type.

    ``--submitted-since <timestamp>``

        Query for updates that were submitted since the given timestamp.

    ``--status [pending | testing | stable | obsolete | unpushed | processing]``

        Filter by status.

    ``--suggest [logout | reboot]``

        Filter for updates that suggest logout or reboot to the user.

    ``--type [newpackage | security | bugfix | enhancement]``

        Filter by update type.

    ``--user <username>``

        Filter for updates by the given username.

``bodhi updates request [options] <update> <state>``

    Request that the given update be changed to the given state. ``update`` should be given by
    update id, and ``state`` should be one of testing, stable, unpush, obsolete, or revoke.


Examples
========

Create a new update with multiple builds::

    $ bodhi updates new --user bowlofeggs --type bugfix --notes "Fix permission issues during startup." --bugs 1393587 --close-bugs --request testing --autokarma --stable-karma 3 --unstable-karma -3 ejabberd-16.09-2.fc25,erlang-esip-1.0.8-1.fc25,erlang-fast_tls-1.0.7-1.fc25,erlang-fast_yaml-1.0.6-1.fc25,erlang-fast_xml-1.1.15-1.fc25,erlang-iconv-1.0.2-1.fc25,erlang-stringprep-1.0.6-1.fc25,erlang-stun-1.0.7-1.fc25


Help
====

If you find bugs in bodhi (or in the man page), please feel free to file a bug report or a pull
request::

    https://github.com/fedora-infra/bodhi

Bodhi's documentation is available online: https://bodhi.fedoraproject.org/docs
