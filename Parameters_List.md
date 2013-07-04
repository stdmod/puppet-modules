## Naming Standards for parameters - List
DRAFT v. 0.0.1

This is a proposal to discuss for a list of parameter names that
can be used both in classes and defines in a module.

A Standard Module is not required to have all of them, with if some parameters
are provided that offer the same function, they should be called like these.

Please comment:
- If the parameter make sense for you
- Your suggested name

+1 for the choices you agree with

If you want to provide a totally alternative list of names, submit it (on separated file) as a PR.

## A list of parameter names based on the managed resource Types

This naming pattern has names that reflect the resource type managed by the class or define and the relevant parameters.

Generally no special prefix is needed for a class or define main configuration file, package or service.

For additional resources a prefix is used. For common alternative resources naming standard are set too.

The are some exceptions to the plain [prefix_]resource_parameter pattern that should be evaluated with care.

```
## General parameters
ensure (enable?)
audit
noop
version (package_version?)

## Package and installation management
package
package_provider
package_*

other_package
other_package_*

client_package
client_package_*

## Services management
service
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


## Configuration files management
file
file_source
file_template
file_content
file_*
file_options_hash

dir
dir_source
dir_recurse
dir_purge
dir_*

## Reference to common directories
home_dir
home_dir_*
data_dir
log_dir
log_dir
bin_dir
lib_dir
tmp_dir
confd_dir

## Reference to common files
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

## Reference to module specific files
other_file
other_file_source
other_file_template
other_file_options_hash
other_file_*
hba_file
hba_file_template
hba_file_*

## Reference to internal classes that can be substituted
class_dependency
class_my
class_monitor
class_firewall

resources_hash

## Installations methods
install_mode
install_url
install_source
install_destination
install_pre_command
install_post_command

install_script_file
install_script_file_*
install_response_file
install_response_file_*


## Monitoring
monitor
monitor_tool
monitor_host
monitor_port
monitor_protocol
monitor_url
monitor_process
monitor_service
monitor_config_hash

## Firewalling
class_firewall
firewall
firewall_src
firewall_dst
firewall_port
firewall_protocol


## Exec parameters (for defines)
exec (exec_command?)
exec_environment
exec_path
exec_*
exec_options_hash


## Generic parameters to manage users creation and attributes
user
user_uid
user_gid
user_*

user_create
```
