## Naming Standards for parameters - List
DRAFT v. 0.0.1

This is a proposal to discuss for a list of parameter names that
can be used both in classes and defines in a module.

A Standard Module is not required to have all of them, but if some parameters
are provided that offer the same function, they should be called like these.

Please comment:
- +1 if the parameter makes sense for you
- Eventually an alternative name

If you want to provide a totally alternative list of names, submit it (on separated file) as a PR.

## A list based on the managed resource Types

This naming pattern has names that reflect the resource type managed by the class or define and the relevant parameters.

Generally no special prefix is needed for a class or define main configuration file, package or service.

For additional resources a prefix is used. For common alternative resources naming standard are set too.

There are some exceptions to the plain [prefix_]resource_parameter pattern that have to be defined with care.

```
## General parameters
ensure (enable?)
audit (audits? - Is this needed?)
noop (noops? - needed?)
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
dependency_class
my_class
monitor_class
firewall_class

## Hash of resources to pass to create_resource
resources_hash

## Installations methods
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
