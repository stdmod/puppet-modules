
= Stmod params for file management defines (as conf.pp)

[*template*]
  String. Optional. Default: undef. Alternative to: source, content.
  Sets the module path of a custom template to use as content of
  the config file
  When defined, config file has: content => content($template),
  Example: template => 'site/<%= metadata.name %>/my.conf.erb',

[*content*]
  String. Optional. Default: undef. Alternative to: template, source.
  Sets directly the value of the file's content parameter
  When defined, config file has: content => $content,
  Example: content => "# File Managed by Puppet \n",

[*source*]
  String. Optional. Default: undef. Alternative to: template, content.
  Sets the value of the file's source parameter
  When defined, config file has: source => $source,
  Example: source => 'puppet:///site/<%= metadata.name %>/my.conf',

[*ensure*]
  String. Default: present
  Manages config file presence. Possible values:
  * 'present' - Create and manages the file.
  * 'absent' - Remove the file.

[*path*]
  String. Optional. Default: $config_dir/$title
  The path of the created config file. If not defined a file
  name like the  the name of the title a custom template to use as content of configfile
  If defined, configfile file has: content => content("$template")

[*mode*] [*owner*] [*group*] [*notify*] [*require*] [*replace*]
  String. Optional. Default: undef
  All these parameters map directly to the created file attributes.
  If not defined the module's defaults are used.
  If defined, config file file has, for example: mode => $mode

[*options_hash*]
  Hash. Default undef. Needs: 'template'.
  An hash of custom options to be used in templates to manage any key pairs of
  arbitrary settings.


