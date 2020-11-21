---
date: "2018-02-19T14:45:53+06:00"
title: "Configure phpMyAdmin to access multiple servers"
---

By default, phpMyAdmin allows us to connect to local MySQL server only. But we may need to access multiple database servers from our single phpMyAdmin. It's such an easy job. For each new server, we will just need to create a new config file (with .php extension) in `/etc/phpmyadmin/conf.d` directory.

lets create a new server

```
sudo nano /etc/phpmyadmin/conf.d/second-server.php
```

```
<?php 

$cfg['Servers'][2]['verbose']  = 'Database Server #2';
$cfg['Servers'][2]['host']     = 'DB_HOST';
$cfg['Servers'][2]['user']     = 'DB_USERNAME';
$cfg['Servers'][2]['password'] = 'DB_PASSWORD';
```

That's it! We should now be able to access this new server from phpMyAdmin.

Note that, the array index is 2, because 1 is for localhost. So if we want to add another new server, the config will be as follow :

```
<?php 

$cfg['Servers'][3]['verbose']  = 'Database Server #3';
$cfg['Servers'][3]['host']     = 'DB_HOST';
$cfg['Servers'][3]['user']     = 'DB_USERNAME';
$cfg['Servers'][3]['password'] = 'DB_PASSWORD';
```

We can also add multiple servers in one config file, for example :

```
$i=1;
$hosts = array (
    "foo.example.com",
    "bar.example.com",
    "baz.example.com",
    "quux.example.com",
);

foreach ($hosts as $host) {
    $i++;
    $cfg['Servers'][$i]['host']     = $host;
    $cfg['Servers'][$i]['port']     = '';
    $cfg['Servers'][$i]['socket']   = '';
    $cfg['Servers'][$i]['connect_type']     = 'tcp';
    $cfg['Servers'][$i]['extension']        = 'mysql';
    $cfg['Servers'][$i]['compress'] = FALSE;
    $cfg['Servers'][$i]['controluser']      = 'pma';
    $cfg['Servers'][$i]['controlpass']      = 'pmapass';
    $cfg['Servers'][$i]['auth_type']        = 'cookie';
    $cfg['Servers'][$i]['user']     = '';
    $cfg['Servers'][$i]['password'] = '';
    $cfg['Servers'][$i]['only_db']  = '';
    $cfg['Servers'][$i]['verbose']  = '';
    $cfg['Servers'][$i]['pmadb']    = 'phpmyadmin';
    $cfg['Servers'][$i]['bookmarktable']    = 'pma_bookmark';
    $cfg['Servers'][$i]['relation'] = 'pma_relation';
    $cfg['Servers'][$i]['table_info']       = 'pma_table_info';
    $cfg['Servers'][$i]['table_coords']     = 'pma_table_coords';
    $cfg['Servers'][$i]['pdf_pages']        = 'pma_pdf_pages';
    $cfg['Servers'][$i]['column_info']      = 'pma_column_info';
    $cfg['Servers'][$i]['history']  = 'pma_history';
    $cfg['Servers'][$i]['designer_coords'] = 'pma_designer_coords';
}
```
