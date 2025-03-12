+++
title = "Atelier 7"
weight = 177
draft = true
+++

# Solution des exercices


## YUM

### Paquet 01

<pre>
$ yum provides ifconfig
$ sudo yum install -y net-tools
</pre>

### Paquet 02

<pre>
$ yum search speak
$ sudo yum install -y kmouth
</pre>

### Paquet 03

<pre>
$ yum search go | grep -i lang
$ sudo yum install -y golang
</pre>

### Paquet 04

<pre>
$ yum provides ag
$ yum install -y the_silver_searcher
</pre>

### Paquet 05

<pre>
$ yum search disk usage
$ sudo yum install -y filelight
</pre>

### Paquet 06

<pre>
$ yum search music
$ sudo yum install -y juk
</pre>

### Paquet 07

<pre>
$ yum search game | grep -i memory
$ sudo yum install -y blinken
</pre>

### Paquet 08

<pre>
$ yum search office
$ sudo yum install -y libreoffice-writer libreoffice-math libreoffice-calc libreoffice-impress ...
</pre>

## Cron

Créez un script <code class="gr">/home/&lt;user&gt;/script.sh</code>

Dans le script :

{{< highlight bash "linenos=true,linenumbersintable=false"  >}}
wget --no-check-certificate https://gyoukou.ca/heure.brut
cat /home/axel/heure.brut >> /home/axel/heures.txt
rm /home/axel/heure.brut
{{< / highlight >}}

Ensuite, éditez la crontab :

<pre>
$ crontab -e
</pre>

Dans la crontab :

{{< highlight bash "linenos=true,linenumbersintable=false"  >}}
* * * * * bash /home/axel/script.sh
{{< / highlight >}}
