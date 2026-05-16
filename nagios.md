## Nagios

Set up Nagios on a Raspberry Pi, to monitor the local network
as well as some of my websites.

I followed the instructions at
<https://pimylefeup.com/raspberry-pi-nagios/>

My configurations are on
[github](https://github.com/karlduino/nagios_cfg)

I wanted to include a test of internet speed, and to be able to track
internet speed over time, but things seemed to be constantly changing
and break. But see <https://github.com/jonwitts/nagios-speedtest>

### Installation

- Start with [my general set
  up](https://github.com/kbroman/ProgrammingNotes/blob/main/raspberry_pi.md#general-set-up),
  including installation of mg, git, neofetch, and tmux.

- install a bunch more stuff including apache and php

  ```shell
  sudo apt install -y autoconf build-essential wget unzip apache2 apache2-utils libapache2-mod-php php \
       libgd-dev snmp libnet-snmp-perl gettext libssl-dev bc gawk dc libmcrypt-dev speedtest-cli
  ```

- download, build, and install nagios

  ```shell
  cd /tmp
  wget -O nagios.tar.gz https://github.com/NagiosEnterprises/nagioscore/archive/nagios-4.5.12.tar.gz
  tar xzvf nagios.tar.gz
  cd nagioscore-nagios-4.5.12
  ./configure --with-httpd-conf=/etc/apache2/sites-enabled
  make all
  ```

- Set up nagios

  ```shell
  sudo make install-groups-users
  sudo usermod -a -G nagios www-data
  sudo make install
  sudo make install-daemoninit
  sudo make install-commandmode
  sudo make install-config
  sudo make install-webconf
  sudo a2enmod rewrite
  sudo a2enmod cgi
  sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
  ```

  In the last line, it will ask you to create a new password for `nagiosadmin`


- Start nagios

  ```shell
  sudo systemctl restart apache2
  sudo systemctl enable nagios
  sudo systemctl start nagios
  sudo systemctl status nagios
  ```

- Install nagios plugins

  ```shell
  cd /tmp
  wget -O nagios-plugins.tar.gz https://github.com/nagios-plugins/nagios-plugins/releases/download/release-2.5/nagios-plugins-2.5.tar.gz
  tar xzvf nagios-plugins.tar.gz
  cd /tmp/nagios-plugins-2.5
  ./configure
  make
  sudo make install
  sudo systemctl restart nagios
  ```

- Connect to the nagios web interface at <http://nagiospi.local/nagios>
  (or whatever IP address you've got)

  Actually, I prefer the page
  <http://nagiospi.local/nagios/cgi-bin/status.cgi?hostgroup=all&style=detail>

- Set up git, by copying over `~/.gitignore_global` and `~/.gitconfig`

- Add my configurations

  ```shell
  cd
  git clone git@github.com:karlduino/nagios_cfg
  sudo cp nagios_cfg/*.cfg /usr/local/nagios/etc/
  sudo cp -r nagios_cfg/objects/* /usr/local/nagios/etc/objects/
  sudo cp nagios_cfg/libexec/* /usr/local/nagios/libexec/
  ```

- Test configuration

  ```shell
  sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
  ```

- Restart nagios

  ```shell
  sudo /usr/local/nagios/bin/nagios -d /usr/local/nagios/etc/nagios.cfg
  ```

- Reboot the machine with `sudo reboot`

- Clone the code to capture speed and status:

  ```
  git clone git@github.com:karlduino/grab_speed
  git clone git@github.com:karlduino/light_on_nagios
  ```

- Move the scripts to the home directory:

  ```
  cp grab_speed/grab_speed.py .
  cp light_on_nagios/subset_status.sh .
  ```

- Set the scripts to run periodically:

  ```
  crontab -e
  ```

  Use the following (`subset_status.sh` every minute; `grab_speed.py`
  every hour at 59th minute; see <https://crotab.guru>)

  ```
  * * * * * /usr/local/bin/subset_status.sh
  59 * * * * /usr/local/bin/grab_speed.py
  ```
