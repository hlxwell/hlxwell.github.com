---
layout: post
title: "how to stop run apache at startup"
category: 
tags: []
---
{% include JB/setup %}

{{% highlight shell %}}
$ sudo update-rc.d apache2 disable
update-rc.d: warning: apache2 start runlevel arguments (none) do not match LSB Default-Start values (2 3 4 5)
update-rc.d: warning: apache2 stop runlevel arguments (none) do not match LSB Default-Stop values (0 1 6)
 Disabling system startup links for /etc/init.d/apache2 ...
 Removing any system startup links for /etc/init.d/apache2 ...
   /etc/rc0.d/K09apache2
   /etc/rc1.d/K09apache2
   /etc/rc2.d/S91apache2
   /etc/rc3.d/S91apache2
   /etc/rc4.d/S91apache2
   /etc/rc5.d/S91apache2
   /etc/rc6.d/K09apache2
 Adding system startup for /etc/init.d/apache2 ...
   /etc/rc0.d/K09apache2 -> ../init.d/apache2
   /etc/rc1.d/K09apache2 -> ../init.d/apache2
   /etc/rc6.d/K09apache2 -> ../init.d/apache2
   /etc/rc2.d/K09apache2 -> ../init.d/apache2
   /etc/rc3.d/K09apache2 -> ../init.d/apache2
   /etc/rc4.d/K09apache2 -> ../init.d/apache2
   /etc/rc5.d/K09apache2 -> ../init.d/apache2
{{% endhighlight %}}