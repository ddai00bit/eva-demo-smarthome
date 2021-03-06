EVA ICS demo: smart home
************************

Live demo
=========

@ https://demo-smarthome.eva-ics.com/

Layout
======

This demo deploys single `EVA ICS <https://www.eva-ics.com/>`_ node.

Logic
=====

Unit *light/hall* is configured to automatically turn off in 20 seconds.

If sensor *security/motion1* gets value 1 (motion detected), light in hall is
automatically turned on.

If alarm is on (lvar *security/alarm*), motion event handler macro additionally
close all windows, turn on all lights and start CCTV recording.

In real life, motion event handler should also send a message or place a call
to owner or security service, but in demo configuration this is not realized.

Timer *lvar:timers/hall_timer* is reset every time when hall light is turned
on. It doesn't do any functions on set / on expire, as hall light is configured
to turn off in 20 seconds with *auto_off* unit feature, used only for demo
purposes.

Network and containers
======================

* **eva_smarthome_server** 10.27.14.199

Deployment
==========

Requirements: `Docker <https://www.docker.com/>`_, `docker-compose
<https://docs.docker.com/compose/>`_.

This demo depends on EVA HMI `Block UI
<https://github.com/alttch/eva-hmi-block_ui>`_ app, so clone it recursively.

* Clone UI: *git submodule update --init --recursive*

* Execute *docker-compose up* to deploy containers and demo configuration

Management
==========

API
---

Default master key is: *demo123*

http://10.27.14.199:8828 - SFA API/primary operator interface

Components:

* http://10.27.14.199:8812 - UC API/EI
* http://10.27.14.199:8817 - LM PLC API/EI

The port **8828** is also mapped to main host.

UI
--

http://10.27.14.199:8828

SFA user credentials:

* **login** *operator*
* **password** *123*

CLI
---

CLI management:
    
    *docker exec -it eva_smarthome_server eva-shell*

Event simulation
----------------

Simulate motion sensor event:

    ./simulate_motion.py

