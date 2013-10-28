# Modules Naming Standards
DRAFT v. 0.0.3

This document sums up and proposes naming conventions for Puppet modules.

They are not supposed to enforce any module's design logic, so alternative options and common patterns are outlined for different modules' structure and functionallity.
 
A Standard Module is not required to have all of the names and variables proposed here, but if some parameters and class names are provided that offer the same function, they should be called as proposed in these conventions.

## Modules names and structure
A module has the **name of the managed application**, system function or resource it manages.

Using the **package name** as module name is not a good practice as package names differ among distributions, so a **common name** should be preferred instead.

Example:

Bad naming:

```puppet
bind9::params
postgresql-8::service
mysql5::install
```
Good naming:

```puppet
bind::params
postgresql::service
mysql::install
```
In case of doubt, already established namings and common sense are the rule.

Resources can be managed in the main class and/or in subclasses.

When a module has subclasses current standard de-facto names apply:

**class::params** - (May) contain modules internal parameters and defaults

**class::client** - Manages only the client

**class::server** - Manages the server installation.

**class::install** - Manages only the installation of 'class'

**class::service** - Manages only the service of 'class'

**class::config** - Manages the configuration of 'class'

**class::repo** - Manages eventual extra repos needed for the class

Examples:

```puppet
postfix::params
openssh::client
openssh::server
elasticsearch::install
postfix::service
postfix::config
mongodb::repo
```
In the cases that 'class' has different sub-applications that can be configured separatedly or different daemons for each of its parts, subdirectories and subclass might be used to represent each part.

Example:

```puppet
bacula::params
bacula::config
```
For the server application (bacula-director):

```puppet
bacula::server
bacula::server::install
bacula::server::service
bacula::server::config
```
or

```puppet
bacula::director
bacula::director::install
bacula::director::service
bacula::director::config
```
being the latter the preferred naming option:

```puppet
bacula::director::install
bacula::client::service
bacula::storage::config
bacula::console::install
```

### Common defines
The following defines are reserved for common use cases:
module::conf     # Define to manage secondary configuration files for the module
module::instance # Define that manages single different instances of the module's application

Example:
```puppet
tomcat::instance
memcached::instance
postfix::conf
```


## Parameters for classes and defines
A module may have many different parameters, related to the specific application it manages, but in order to comply with *stdmod* guides, some parameters should have a common naming among modules.

Here are considered **only common parameters** that might be used in any module.

The general **[prefix_]resource_attribute** pattern is followed, to map consistently class parameters with resources attributes.

The use of a prefix should be avoided for classes or defines that manage a single resource main configuration file, package or service (ie: **package_ensure** is preferred instead of main_package_ensure).

For additional resources a prefix is used denoting the resource itself (ie: **client_package**, **server_package**).

If there are parameters as the ones defined before in subclasses or defines, omonimous resource names are removed.

For example, a module can expose parameters in the main class like :

```puppet
class openssh (
  $service_ensure = disabled,
  $service_enable = false,
  ) { … }

```
or/and have them in short form, without resource name, in the relevant subclass: 

```puppet
class openssh::service (
  $ensure = disabled,
  $enable = false,
  ) { … }
```

More generally, in defines, the shorter version is preferred (for the single or the main resource managed by the define, for other resources standard names with prefixes apply).

### Variables validation and sanitation

Variables should be validated and sanitized whenever possible, taking in account these guide lines:

* If a variable has a finite number of possible values, the passed value should be checked against
  this list, or an error should be raised.
* The sanitized value should be stored in a variabled prefixed with *bool_* plus the name
  of the original variable when sanitizing booleans. Ie.:

```puppet
$bool_listen = any2bool($listen)
```

* The sanitized value should be stored in a variabled prefixed with *real_* plus the name
  of the original variable when sanitizing variables with any number of known options. Ie:


```puppet
$real_version = $postgresql::version ? {
  '' => $postgresql::bool_use_postgresql_repo ? {
    true  => '9.2',
    false => $::operatingsystem ? {
...

```

* The sanitized value should be stored in a variabled prefixed with *manage_* plus the name
  of the original variable when sanitizing variables affecting control of resources. Ie:


```puppet
$manage_package = $postgresql::bool_absent ? {
  true  => 'absent',
  false => 'present',
}

```

### Package and installation management
```
package_name
package_ensure
package_provider
package_*

other_package
other_package_*

client_package
client_package_*

server_package
server_package_*
```

### Services management
```
service_name
service_ensure
service_enable
service_subscribe
service_*

other_service
other_service_*

init_script_file
init_script_file_template
init_script_file_options_hash

init_options_file
init_options_file_template
init_options_file_options_hash
```

### Configuration files management
```
config_file_name
config_file_source
config_file_template
config_file_content
config_file_*
config_file_options_hash

config_dir_path
config_dir_source
config_dir_recurse
config_dir_purge
config_dir_*
```

### Reference to common directories
```
home_dir
home_dir_*
data_dir
data_dir_*
log_dir
log_dir_*
bin_dir
bin_dir_*
lib_dir
lib_dir_*
tmp_dir
tmp_dir_*
confd_dir
confd_dir_*
```

### Reference to common files
```
log_file
log_file_owner
log_file_mode
log_file_*

pid_file
pid_file_owner
pid_file_mode
pid_file_*

init_script_file
init_script_file_*
init_config_file
init_config_file_*
```


### Reference to internal classes that can be substituted

```
dependency_class
user_class
install_class
my_class
monitor_class
firewall_class
repo_class
```

### Hash of resources to pass to create_resource
```
resources_hash
```

### Installations methods
```
install
install_url
install_base_url
install_source
install_destination
install_pre_exec
install_pre_exec_*
install_pre_tmpdir
install_post_exec
install_post_exec_*


install_script_file
install_script_file_*
install_response_file
install_response_file_*
```


### Reference to common resources for monitoring / firewalling
```
tcp_port
udp_port
process_name
process_user
process_group
```


### Monitoring
Monitoring can be managed with a custom $monitor_class. 
A default a local module::monitor class may be provided but should be disabled by default.

```
monitor_class
monitor_options_hash
```

### Firewalling
Firewalling can be managed with a custom $monitor_class.
A default a local module::firewall class may be provided but should be disabled by default.

```
firewall_class
firewall_options_hash
```


### Exec parameters (for defines)
```
exec_command
exec_environment
exec_path
exec_*

exec_options_hash
```

### File parameters (for conf define)
```
path
source
template
content
mode
owner
```

### Parameters for instance define 
```
config_file_template
init_file_template
user
```


### Users management
When a module requires a dedicated user, a module .

```
user_name
user_uid
user_gid
user_*

```
