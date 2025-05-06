README wmhdplop

---


REQUIREMENTS
============

* `hddtemp`: (optional)  Show hdd temperature/status.


NOTES
=====

Temperature Status
------------------

As mentioned in REQUIREMENTS, to show hdd temperature/status, you need to install
`hddtemp` package and run it as a daemon.  `hddtemp` already ships the `rc.d`
service script, so all you need to do is:

    sudo pkgman install --deps --group hddtemp
    sudo /etc/rc.d/hddtemp start

Check the status manually:

    sudo hddtemp

The output should look something like:

    /dev/sda: TOSHIBA SERNO: 32°C

Start `wmhdplop` with the `-t` option:

    wmhdplop -t -d /dev/sda


---

End of file.
