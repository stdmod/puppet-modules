# Modules Naming Standards
DRAFT v. 0.0.2

This document sumups and proposes naming conventions for Puppet modules.

They are not supposed to enforce any module's design logic, so alternative options and common patterns are outlined for different modules' structure and functions.
 
A Standard Module is not required to have all of the proposed names, but if some parameters and class names are provided that offer the same function, they should be called like the one proposed by these conventions.

## Modules names and structure
A module has the **name of the managed application**, system function or resource.

In case of doubt, established namings and common sense are rule.

When a module has subclasses, current standard de-facto names apply:

**class::params** - (May) contain modules internal parameters and defaults

**class::client** - Manages only the client

**class::server** - Manages the server installation.

**class::install** (*class::package?*) - Manages only the installation of 'class' 

**class::service** - Manages only the service of 'class'

**class::config** - Manages the configuration of 'class'

## Parameters for classes and defines 
A module may have many different parameters, related to the specific application it manages.

Here are considered **only common parameters** that might be used in any module.

The general **[prefix_]resource_attribute** pattern is followed, to map consistently class parameters with resources attributes.

Generally no special prefix is needed for a class or define main configuration file, package or service (ie: **package_ensure** not main_package_ensure).

For additional resources a prefix is used. (ie: **client_package**, **server_package**)

If there are parameters in subclasses (as the ones defined before) omonimous resource names are removed.
For example, a module can expose parameters in the main class like :

```
class openssh (
  $service_ensure = disabled,
  $service_enable = false,
  ) { … }

```
or/and have them in short form, without resource name, in the relevant subclass: 

```
class openssh::service (
  $ensure = disabled,
  $enable = false,
  ) { … }
```

More generally, in defines, the shorter version is preferred (for the single or the main resource managed by the define, for other resources standard names with prefixes apply).

### General parameters
```
ensure (enable?) 
audit (audits? - Is this needed?)
noop (noops? - needed?)
version (package_version?)
```

### Package and installation management
```
package (package_name?) (1)
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
service (service_name?) (1)
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
file (file_path?) (1)
file_source
file_template
file_content
file_*
file_options_hash

dir (dir_path?)
dir_source
dir_recurse
dir_purge
dir_*
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
install_post_exec
install_post_exec_*

install_script_file
install_script_file_*
install_response_file
install_response_file_*
```


### Monitoring
Monitoring can be managed with a custom $monitor_class. 
A default a local module::monitor class may be provided but should be disabled by default.
To enable set: monitor => true 

```
monitor
monitor_tool
monitor_host
monitor_port
monitor_protocol
monitor_url
monitor_process
monitor_service
monitor_config_hash
```

### Firewalling
Firewalling can be managed with a custom $monitor_class. 
A default a local module::firewall class may be provided but should be disabled by default.
To enable set: firewall => true

 ```
firewall
firewall_src
firewall_dst
firewall_port
firewall_protocol
```


### Exec parameters (for defines)
```
exec (exec_command?) (1)
exec_environment
exec_path
exec_*

exec_options_hash
```


### Users management
When a module requires a dedicated user, a module .

```
user (user_name?) (1)
user_uid
user_gid
user_*

```


#### Notes
(1) - For the parameter that apply to the namevar attribute of the relative resource there are 2 (both sensible) alternatives:

  a) Use the short form (ie: package, service, [config_]file…)

  b) Use the normal expanded form (ie: package_name, service_name, [config_]file_path, exec_command …)

Which one?

