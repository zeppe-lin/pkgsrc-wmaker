README wmhdplop

---


REQUIREMENTS
============

* `hddtemp`: (optional)  Show hdd temperature/status.


TEMPERATURE STATUS
==================

As mention above, to show hdd temperature/status, you need to install `hddtemp`
package and run it as a daemon.  `hddtemp` already ships the `rc.d` file, so
all you need to do is:

```sh
sudo pkgman install --deps --group hddtemp
sudo /etc/rc.d/hddtemp start
```

Check the status manually:

```sh
sudo hddtemp
```

The output should look something like:

```
/dev/sda: TOSHIBA SERNO: 32°C
```

Now, you can start `wmhdplop` with `-t` option, like the following:

```sh
wmhdplop -t -d /dev/sda
```

---

End of file.
